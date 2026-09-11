# HP-PLAN-010 — MemoryProvider Contract

Status: PROPOSED

## Purpose
Keep Hive Plan independent from one memory backend while allowing HIVE to be the preferred high-capability provider.

## Providers
### `HIVE_PROVIDER`
Preferred when healthy and contract-compatible.

Capabilities expected from current HIVE direction include project isolation, checkpoint-first context, lexical/vector hybrid retrieval, memory lookup, provenance, restart recovery and read-only integration surfaces.

### `EMBEDDED_LOCAL_PROVIDER`
Required fallback for Hive Plan standalone mode.

It must provide the minimum semantic contract using Hive Plan PostgreSQL, local content-addressed artifacts and replaceable embedding/reranking adapters. Redis is optional.

## Required provider operations
- `health()`
- `capabilities()`
- `project_status(project_id)`
- `context_build(request)`
- `context_search(request)`
- `memory_search(request)`
- `memory_get(memory_id)`
- `checkpoint_read(project_id)`
- `source_get(source_ref)` where policy permits

Write/mutation APIs are explicitly outside the minimum provider contract. Canonical promotion remains controlled by Hive Plan/GitHub governance.

## Query envelope
Every query carries:
- project ID;
- task/increment/work-order ID when applicable;
- requested source classes;
- authority floor;
- freshness bound;
- compatibility filters;
- privacy class;
- token/context budget;
- required/optional evidence classes;
- query fingerprint.

## Result envelope
Every returned item includes:
- stable source/memory ID;
- project ID;
- source type;
- authority class;
- repository/path/commit or artifact provenance when available;
- content/chunk reference;
- fingerprint;
- created/validated/superseded metadata;
- compatibility metadata;
- retrieval channel and score;
- provider identity/version;
- redaction flags.

Semantic score alone never grants authority.

## HIVE adapter behavior
The adapter SHOULD prefer HIVE read-only surfaces and native project isolation. It MUST fail closed on contract/version mismatch, project ambiguity, stale checkpoint identity or provider health degradation that threatens correctness.

When HIVE is unavailable:
- do not fabricate cached current state;
- expose provider status truthfully;
- fall back only if the task is allowed to use the embedded provider;
- record provider degradation in response provenance.

## Embedded fallback
Minimum V1 fallback:
- PostgreSQL durable source/memory metadata;
- exact + lexical search;
- pgvector-compatible semantic retrieval when embeddings available;
- deterministic fusion;
- content-addressed cache;
- checkpoint/source hierarchy enforcement;
- operational failure/success memory records;
- rebuildable derived embeddings/indexes.

## Cache rules
Cache key includes provider, provider capability/version, project/source root, checkpoint/decision fingerprints, query fingerprint, retrieval profile and privacy class.

Cache authority never exceeds source authority. Any critical source fingerprint change invalidates dependent retrieval/context caches.

## Provider equivalence tests
A provider can be promoted only if golden retrieval scenarios prove:
- project isolation;
- no stale canonical promotion;
- checkpoint-first behavior;
- correct supersession handling;
- provenance completeness;
- compatible failure-memory retrieval;
- secret/redaction behavior;
- restart recovery;
- bounded latency/context size.

## No lock-in rule
HIVE-specific fields live under namespaced extensions. Hive Plan core code depends on the MemoryProvider contract, not HIVE database tables or internal implementation details.
