# Data & Persistence Architecture

Status: PROPOSED FOR FREEZE — HP-PLAN-008

## Principle
Canonical workflow state must be durable, queryable, backupable and recoverable. Caches and queues may accelerate the system, but must never become the only copy of project truth.

## Primary datastore
**PostgreSQL 18.x** is the primary V1 canonical datastore.

Reasons:
- mature ACID semantics;
- transactions for workflow/state transitions;
- JSONB for flexible structured artifacts;
- strong indexing and full-text capabilities;
- LISTEN/NOTIFY for wake-up assistance;
- reliable backup/migration tooling;
- pgvector extension for integrated vector retrieval;
- avoids an early multi-database operational burden.

PostgreSQL 19 remains pre-release during this planning round and must not be V1 production baseline until stable and evaluated.

## Domain storage separation
Use separate schemas/logical modules, not separate database servers by default:
- `core` — projects, manifests, checkpoints, decisions;
- `workflow` — increments, Work Orders, execution epochs, state machines;
- `event` — durable normalized EventSpine journal/outbox/effects;
- `review` — evidence metadata, findings, receipts, impact graph;
- `memory` — retrieval metadata, chunks, embeddings, failure/success memories;
- `agent` — registry runtime state, tasks, council messages, skills metadata;
- `telemetry` — compact operational aggregates and cost/accounting state.

Cross-domain writes that must be atomic may share a DB transaction, but domain service APIs remain explicit to prevent accidental coupling.

## Vector/RAG strategy
Default V1 candidate: **pgvector 0.8.6+** on PostgreSQL 18.

Rules:
- embeddings are derivative indexes, not source truth;
- every vector row references canonical source identity + fingerprint;
- stale fingerprints invalidate retrieval entries;
- HNSW/IVFFlat strategy is benchmark-selected by corpus size/filter behavior;
- exact/lexical/AST retrieval occurs before or alongside semantic retrieval;
- dedicated vector DB is an adapter option, not mandatory V1 infrastructure.

Qdrant or another dedicated engine may be TRIALed if actual workloads exceed pgvector's quality/latency/memory targets.

## Durable event/work queue
Preferred architecture:
1. canonical state transition written in PostgreSQL;
2. durable outbox/event row committed in same transaction;
3. worker wakes through polling/LISTEN-NOTIFY/job queue;
4. handler is idempotent;
5. EffectLedger records externally committed side effects.

### pg-boss
pg-boss is a strong TRIAL candidate because it provides PostgreSQL-backed durable jobs, retries, singleton policies, dependencies and LISTEN/NOTIFY wake-up support without adding a separate broker.

It must pass workload benchmarks and fault tests before ADOPT because queue maintenance/autovacuum behavior and high-cardinality workloads can matter.

Temporal is WATCH/FUTURE for cloud/multi-user/highly distributed workflow requirements; it is intentionally not mandatory for local V1.

## Redis policy
Redis is OPTIONAL in standalone V1.

Possible uses:
- hot result/cache layer;
- rate-limit/circuit-breaker counters;
- transient pub/sub acceleration;
- shared cache if multiple local processes justify it.

Redis may never hold the only copy of:
- Work Order state;
- review verdict;
- event journal;
- checkpoint;
- billing/cost accounting;
- approval/audit evidence.

When Hive V1 is integrated, its Redis infrastructure may be reused through an adapter where safe.

## Search/index persistence
RepoPulse stores lightweight metadata/content fingerprints in PostgreSQL or a content-addressed local index directory.

Search cascade remains replaceable:
- Git metadata;
- ripgrep/exact search;
- ast-grep structural map;
- tgrep TRIAL for large hot repositories;
- embeddings/vector retrieval;
- Feature Impact Graph expansion.

Generated indexes are rebuildable and therefore not canonical backup-critical data.

## Artifact/log storage
Large immutable artifacts, logs, screenshots, benchmark reports and downloaded evidence should not bloat core relational tables.

Use a local content-addressed artifact store:
```text
data/artifacts/sha256/<prefix>/<digest>
```

Database records hold:
- digest;
- media/type;
- producer/source;
- creation timestamp;
- Work Order/PR/evidence references;
- retention policy;
- sensitivity classification.

Later S3-compatible object storage can replace the filesystem adapter without changing domain contracts.

## Migrations
- forward-only versioned migrations;
- migrations committed with application code;
- schema version recorded;
- destructive migrations require backup + rollback/recovery plan;
- startup refuses unknown future schema versions;
- HIGH_ASSURANCE path for auth/security/canonical-data migrations;
- migration rehearsal in disposable DB before release.

Exact migration library is selected with the TypeScript SQL layer benchmark; candidates include Kysely-compatible migration tooling and Drizzle migrations.

## Backup / restore
Minimum V1 policy:
- manual one-click snapshot from cockpit;
- automatic snapshot before risky migrations/upgrades;
- scheduled local backup option;
- PostgreSQL logical backup + critical config/manifest export;
- artifact store manifest + incremental copy;
- checksums;
- restore verification, not only backup creation;
- documented disaster recovery procedure.

A backup that has never been restored is treated as unverified.

## Secret storage
Secrets are never stored in Git, RAG chunks, review artifacts or normal database columns in plaintext.

Introduce `SecretVault` abstraction with:
- local development provider;
- Windows/OS-protected provider where practical;
- encrypted-at-rest fallback outside repository;
- reference IDs in application tables;
- explicit redaction at logging/telemetry boundaries.

Exact Windows/Docker bridge is benchmarked during implementation bootstrap.

## Retention
Events/evidence remain durable according to policy. High-volume raw logs may compact into summaries after digest/provenance retention. Canonical decisions/checkpoints/review receipts are not silently TTL-deleted.

## Recovery objectives
V1 is local single-user, so initial RPO/RTO can be pragmatic, but the architecture must support explicit targets and cockpit health reporting.

Failure drills must include:
- process crash mid-review;
- duplicate event delivery;
- PostgreSQL restart;
- stale worker result;
- artifact missing/corrupt;
- backup restore;
- migration rollback/recovery;
- interrupted GitHub/API operation.
