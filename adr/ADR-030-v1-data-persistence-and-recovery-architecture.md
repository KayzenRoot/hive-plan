# ADR-030 — V1 Data, Persistence and Recovery Architecture

Status: ACCEPTED  
Date: 2026-09-11  
Increment: HP-PLAN-008

## Context
Hive Plan needs durable workflow/project state, review/evidence history, RAG/vector retrieval, local artifacts, realtime projections and recovery guarantees without turning V1 into a distributed storage platform.

## Decision
Adopt a PostgreSQL-first canonical persistence architecture.

### Canonical relational state
- PostgreSQL 18 is the primary transactional datastore.
- canonical project/workflow/review/agent/cost/policy metadata lives in PostgreSQL.
- schema migrations are versioned and gated.
- canonical workflow state is never stored only in Redis, browser state or ephemeral queues.

### Vector/RAG
- pgvector is the default V1 vector extension behind a VectorStore adapter.
- vector indexes/embeddings are derived/rebuildable and carry model/profile/fingerprint metadata.
- dedicated vector DB remains a measured escape hatch when scale/latency/feature benchmarks justify it.

### Queue/work execution
- durable PostgreSQL-backed jobs/outbox are the default architectural direction.
- pg-boss is a strong TRIAL candidate, not an irreplaceable domain dependency.
- job claims/retries do not replace canonical workflow state.

### Redis
Redis is optional in standalone V1 for hot cache, ephemeral counters, rate limiting or transient pub/sub. It is non-canonical and loss must be recoverable from durable state.

### Artifacts
Large immutable evidence/log/screenshot/benchmark artifacts use a local content-addressed store keyed by digest. PostgreSQL stores metadata, ownership, sensitivity, provenance and references. Storage is adapter-ready for future S3/MinIO-compatible backends.

### Event/recovery model
- use durable workflow/event records where audit or recovery requires them;
- do not force product-wide event sourcing;
- derived cockpit projections are disposable/rebuildable;
- EffectLedger/idempotency protects externally visible effects;
- backup epochs pair PostgreSQL and artifact-store consistency metadata.

### Recovery
- backup automation before consequential migrations;
- scheduled backups configurable;
- RestoreProof validates recovered database, artifacts, fingerprints and critical workflows before READY;
- migration/recovery rehearsal is required for high-risk schema/storage changes;
- corruption or missing artifacts fail closed rather than silently rewriting identity.

## Consequences
Positive:
- one boring durable authority for most V1 state;
- transactional workflow semantics;
- less container/operational complexity;
- RAG can start without separate vector infrastructure;
- clear rebuildable/non-canonical boundaries;
- future adapters preserve an exit path.

Costs/risks:
- PostgreSQL can become overloaded if every telemetry/event use case is treated as canonical;
- queue and vector workloads require tuning/retention discipline;
- local artifact backups must be paired with database metadata.

Mitigations:
- bounded telemetry retention;
- derived indexes/projections;
- benchmark queue/vector workloads;
- explicit data authority classes;
- CAS reconciliation and RestoreProof.

## TRIAL / benchmark boundaries
- pg-boss versus a smaller explicit outbox/worker implementation;
- exact TypeScript SQL/query/migration library;
- HNSW/IVFFlat/exact vector thresholds;
- Redis activation threshold;
- dedicated vector-store threshold;
- local telemetry persistence details and retention values.

## Rejected defaults
- Redis as the only copy of durable workflow state;
- a dedicated vector database on day one without benchmark need;
- Kafka/RabbitMQ/Temporal as mandatory V1 infrastructure;
- storing large immutable evidence blobs directly in ordinary relational rows;
- backup success being inferred without restore verification.