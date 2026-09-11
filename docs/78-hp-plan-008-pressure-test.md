# HP-PLAN-008 Pressure Test — Frontend / Backend / Data

Status: PROPOSED FOR FREEZE

## Objective
Attack the proposed stack before implementation and add controls that preserve beauty, responsiveness, durability and debuggability under realistic local-first load.

## 1. Cockpit / 3D pressure test

### Failure risks
- main-thread stalls from 3D + charts + chat streaming + large diffs;
- WebGPU maturity differences and driver/browser quirks;
- VRAM competition with local AI/media workloads;
- glass blur/post-processing overdraw;
- 3D state becoming the only representation of critical information;
- too many realtime React renders;
- large project timelines/graphs exhausting DOM/GPU budget.

### Controls
#### RenderBudget Governor
A runtime controller owns budgets for:
- frame time;
- DPR;
- particle count;
- active animated nodes;
- shadow quality;
- texture resolution;
- post-processing passes;
- GPU memory estimates where observable;
- update frequency of non-critical visuals.

Profiles: CINEMATIC / BALANCED / EFFICIENT / REDUCED.

The governor may degrade presentation, never semantic information.

#### Frame-Time Circuit Breaker
If sustained frame time exceeds policy:
1. suspend decorative particles;
2. lower DPR;
3. disable expensive post effects;
4. reduce 3D update rate;
5. switch Hive Core to simplified geometry;
6. optionally fall back to 2D topology view.

#### Main-thread isolation
Use workers for heavy graph layout, parsing, aggregation and compatible canvas work. OffscreenCanvas is a benchmark candidate for moving selected rendering/visual preparation off the UI thread. Do not make worker rendering mandatory until React Three Fiber/Three integration is proven in our browser matrix.

#### 3D semantic mirror
Every critical 3D state has an accessible DOM/text equivalent. WebGPU/WebGL failure cannot hide blockers, CI state, cost or review verdicts.

#### Static scene bundling
Trial Three.js WebGPU Render Bundle/BundleGroup paths for mostly-static cockpit geometry. Promote only if measurable frame/CPU improvement exists.

#### TSL-first shader policy
Custom WebGPU visual effects should prefer Three Shading Language/node materials rather than legacy ShaderMaterial assumptions. WebGPURenderer remains TRIAL until our visual slice proves required features and fallback behavior.

### Frontend state architecture
Separate:
- canonical server state;
- realtime event projection;
- ephemeral UI state;
- graphics state.

Do not pipe the raw event firehose directly into React component state.

Introduce `CockpitProjectionStore`:
```text
EventSpine/SSE
   ↓
Projection Reducer
   ↓
coalesced domain snapshots
   ├─ React UI selectors
   ├─ charts
   └─ 3D scene selectors
```

High-frequency telemetry is sampled/coalesced separately from decision-critical events.

## 2. Realtime/backend pressure test

### Failure risks
- reconnect storm after API restart;
- duplicated SSE events;
- slow client backpressure;
- background jobs publishing partial state;
- race between Git polling, CI updates and review state;
- one long LLM/review request tying up API process;
- worker crash after external side effect but before local acknowledgement.

### Controls
#### Durable Projection Boundary
Canonical workflow transition is committed to PostgreSQL before UI notification. Realtime transport is a projection/notification channel, not state authority.

#### Reconnect cursor
SSE messages have durable monotonic/project event IDs. Client reconnects with last processed identity and requests replay/window reconciliation where supported.

#### Coalescing classes
- NEVER_COALESCE: verdict, blocker, checkpoint, PR head, security finding;
- COALESCE_SAFE: token counters, utilization, progress samples;
- SNAPSHOT_ONLY: high-frequency GPU/CPU visual gauges.

#### Worker isolation
Long retrieval, indexing, review, model calls and GitHub orchestration run outside the latency-sensitive API request path. API owns command validation + durable enqueue/state; workers own bounded execution.

#### Transactional outbox/effect ledger
Database transitions and outbound effects use durable intent/outbox patterns. Duplicate delivery must be harmless. This aligns with EventSpine EffectLedger and ReviewLease design.

#### Graceful degradation
If optional services fail:
- Redis loss → rebuild/non-canonical cache miss;
- semantic retrieval failure → truthful lexical fallback;
- 3D failure → full 2D cockpit;
- model-provider outage → ProviderSentinel/fallback or governed block;
- GitHub unavailable → preserve local durable state, show stale/external dependency state, never invent remote success.

## 3. PostgreSQL/data pressure test

### Why PostgreSQL 18 remains strong
PostgreSQL 18 adds asynchronous I/O for sequential scans, bitmap heap scans and vacuum plus skip-scan and other improvements. These are useful but not assumed to magically solve schema/query design. Windows/Docker environment must benchmark actual `io_method` behavior.

### Failure risks
- event/journal tables growing without retention/partition strategy;
- pgvector index memory pressure;
- job queue/vacuum contention;
- artifact metadata DB and filesystem drifting apart;
- backup captures DB and CAS at inconsistent points;
- migration partially applied;
- telemetry overwhelming transactional tables.

### Controls
#### Authority classes
Each data family declares:
- CANONICAL;
- DERIVED_REBUILDABLE;
- CACHE_DISPOSABLE;
- ARTIFACT_IMMUTABLE;
- TELEMETRY_RETENTION_BOUND.

#### Write-path separation
Keep canonical project/workflow records logically separate from high-volume telemetry/event samples. Partition or roll up high-volume streams when thresholds are crossed.

#### CAS reconciliation
Artifact store + DB references get periodic deterministic reconciliation:
- referenced but missing;
- present but unreferenced;
- digest mismatch;
- size mismatch;
- retention eligibility.
No automatic destructive GC before a quarantine period and policy check.

#### Paired backup epoch
Backup manifest binds:
- PostgreSQL backup/snapshot identity;
- artifact-store snapshot boundary;
- schema version;
- project/source fingerprints;
- checksum inventory.
Restore drills must verify the pair.

#### Migration Gate
Before state-changing migration:
1. compatibility assessment;
2. backup checkpoint;
3. migration rehearsal against representative data;
4. forward validation;
5. rollback/recovery plan;
6. post-migration evidence.

## 4. RAG / vector pressure test

### Rule
Vector similarity is a retrieval hint, never authority.

### Retrieval cascade
```text
exact/source IDs
→ lexical
→ AST/symbol/dependency
→ FIG/graph
→ vector semantic
→ rerank
→ authority/freshness filter
→ ContextCapsule
```

### Index lifecycle
Every derived chunk/vector records source digest + parser/chunker version + embedding profile/version + dimension + index version. Any incompatible change marks it stale/rebuildable.

### Vector backend decision
`pgvector` is default candidate for V1 simplicity. Dedicated vector DB remains adapter-backed escape hatch triggered only by benchmarked scale/latency/operational evidence.

## 5. New internal mechanisms

### VisualTruth Mirror
Guarantees every decorative/3D representation maps to a canonical textual/domain state and can be disabled without loss of functionality.

### PulseMux
Realtime event multiplexer that classifies/coalesces events based on semantic importance before browser delivery.

### ProjectionFence
Prevents UI projections from presenting a state newer/older than their bound canonical event watermark without a visible STALE/RECONCILING state.

### ResourcePeacekeeper
Coordinates cockpit graphics profile with local AI/media workload pressure. When local GPU/CPU pressure rises, the cockpit voluntarily reduces visual resource use before affecting critical workflows.

### RestoreProof
A restore is not marked VERIFIED until schema, canonical row counts/fingerprints, artifact digests and selected workflow replay checks pass.

## 6. Benchmark gates

### Cockpit
- interaction latency under chat stream + CI events + charts + Hive Core;
- p50/p95 frame time;
- memory/VRAM proxy;
- time to interactive;
- long-task count;
- reduced-mode semantic parity.

### Backend
- command API p50/p95 under worker load;
- SSE reconnect/replay correctness;
- duplicate-event/effect tests;
- worker crash/restart recovery;
- GitHub/provider outage behavior.

### Data
- migration rehearsal/restore time;
- event/job throughput;
- vacuum/queue contention;
- lexical/hybrid retrieval latency;
- pgvector exact/HNSW candidate tests;
- CAS reconciliation speed.

## Freeze recommendation
Freeze the architectural controls and authority boundaries above. Keep specific graphics thresholds, queue implementation, vector index type, chart engine and worker concurrency as benchmark-derived runtime policy rather than hard-coded architecture.
