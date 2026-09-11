# Checkpoint

Checkpoint ID: HP-CP-0020  
Status: PLANNING ACTIVE  
Canonical branch target: `main`  
Last canonical planning merge: `b13834fe01ed8b25f1277c114e3b3a7684877e52` (HP-PLAN-007 status reconciliation after PR #15/#17)  
Active planning increment: `HP-PLAN-008`  
Active planning branch: `docs/hp-plan-008-stack-data-architecture`

## Frozen foundation
- Product identity/V1 mission, local-first single-user Docker deployment and GitHub canonical truth.
- Hive V1 preferred MemoryProvider with embedded local-RAG fallback.
- Codex remains external executor; Hive Plan owns planning/governance/Work Orders/review/audit/continuity.
- Context-first discovery, Planning Confidence, Assumption Register, Decision Pressure Test and governed agent authority.
- Operational learning memory with verified successes, failures, corrections and provenance.
- Short-lived GitHub branches, governed PR/release lifecycle and verified-throughput objective.
- Versioned JSON artifact contracts, deterministic fingerprints, Review Receipts and Checkpoint Deltas.
- Work Order Compiler: RepoPulse, ChangeGraph/FIG, FailureShield, TestLens, ContextCapsule, ExecutorFit and CompileGuard.
- QualityFloor T0–T4, Verified Outcome Cost/Rework Tax, provider-neutral ModelMesh/CacheFabric and no silent HIGH_ASSURANCE downgrade.
- EventSpine/GitPulse, ReviewMVCC/SnapshotGuard, EvidenceForge/Watermark, ReviewLease/EffectLedger and stale-review cancellation.
- Focused Senior Review: actual diff + semantic impact closure, conditional UADS specialists, FindingGate, SARIF-normalized analyzers and delta-first corrections.
- Governed Agent OS, SkillForge, ResearchRadar, TeamComposer, CouncilBus, Dissent Ledger, AgentGovernor and AgentTaskGraph.
- Open interoperability direction using Agent Skills-style packages and MCP/A2A-compatible adapters without lock-in.
- Principal ecosystem specialists A-031 HIVE, A-032 UGAS and A-033 UADS use live repository truth, EcosystemContextStamp and Tri-System Harmony Protocol.

## Completed planning increments
- HP-PLAN-001 — Interviewer + Planning Protocol.
- HP-PLAN-002 — delivery lifecycle, operational memory and GitHub governance.
- HP-PLAN-003 — machine-readable artifact contracts.
- HP-PLAN-004 — Work Order Compiler & Context Optimization Engine.
- HP-PLAN-005 — Model Router + Cache/Cost Engine.
- HP-PLAN-006 — Event Spine + Auto Review + Focused Senior Review.
- HP-PLAN-007 — Governed Agent OS, skills/research fabric and UADS AgentTaskGraph; audited/merged through PR #15, status headers reconciled through PR #17.

## Active HP-PLAN-008
Objective: freeze implementation technology stack plus data/persistence architecture, with unusually strong emphasis on a beautiful high-performance realtime cockpit, truthful system visualization and maintainable local-first backend.

### Accepted architecture decisions in this branch
- ADR-029 accepts React 19.3+ + TypeScript strict + Vite 8.1+/Rolldown + TanStack Router/Query + project-owned CockpitProjectionStore.
- Motion is the preferred interaction animation layer.
- React Three Fiber + Three.js WebGPURenderer is the optional Hive Core path with WebGL2 fallback and mandatory DOM/2D VisualTruth Mirror.
- Node.js 24 LTS + TypeScript + Fastify modular monolith/workers is the V1 backend direction.
- HTTP snapshots/commands + SSE are the default realtime pattern; WebSocket is exception-by-need.
- pnpm workspace + Docker Compose local-first; no premature Kubernetes/microservices.
- ADR-030 accepts PostgreSQL 18 as primary canonical transactional datastore.
- pgvector is the default replaceable V1 vector/RAG candidate.
- durable PostgreSQL jobs/outbox is the architecture direction; pg-boss remains TRIAL.
- Redis is optional/non-canonical in standalone V1.
- large immutable evidence/log/benchmark assets use local content-addressed storage.
- RestoreProof is required before recovered state becomes READY.

### Frontend / cockpit controls
- Obsidian Glass / Electric Signal visual language.
- RenderBudget Governor + Frame-Time Circuit Breaker.
- VisualTruth Mirror and 2D semantic fallback for critical 3D state.
- CockpitProjectionStore separates business projection, ephemeral UI and graphics state.
- PulseMux event coalescing/backpressure and ProjectionFence freshness protection.
- ResourcePeacekeeper coordinates cockpit GPU/CPU demand with local HIVE/UGAS/AI workloads.
- graphics profiles: CINEMATIC, BALANCED, EFFICIENT and REDUCED.
- first vertical slice is specified as a real end-to-end cockpit, not a mock dashboard.

### Realtime projection contract
- initial HTTP snapshot + watermark-bound SSE deltas;
- explicit CURRENT / STALE / DEGRADED / UNKNOWN / NOT_CONNECTED / NOT_AVAILABLE states;
- critical transitions are never sampled away;
- out-of-order/mismatched watermarks trigger reconciliation;
- Canvas/3D consumes throttled visualization projections separate from business truth;
- projection caches are rebuildable and never canonical.

### Operational/security/resilience direction
- worker isolation for indexing/review/model/GitHub work;
- durable reconnect/event cursor semantics;
- PostgreSQL authority classes, paired backup epoch, CAS reconciliation and Migration Gate;
- retrieval cascade exact/lexical/AST/FIG/vector/rerank/authority filter;
- trust zones, AgentGovernor authority checks, prompt/tool-injection containment;
- dependency circuit breakers, bulkheads and Incident Capsules;
- OpenTelemetry-compatible tracing/metrics/logs.

## HP-PLAN-008 artifacts
- `docs/73-technology-stack-proposal.md`
- `docs/74-cockpit-frontend-visual-system.md`
- `docs/75-data-persistence-architecture.md`
- `docs/76-stack-benchmark-and-adoption-plan.md`
- `docs/77-hive-ugas-uads-specialist-agents.md`
- `docs/78-hp-plan-008-pressure-test.md`
- `docs/79-operational-security-observability-resilience.md`
- `docs/80-first-vertical-slice-cockpit.md`
- `docs/81-cockpit-realtime-projection-contract.md`
- `adr/ADR-028-hive-ugas-uads-principal-specialists.md`
- `adr/ADR-029-v1-application-runtime-and-cockpit-stack.md`
- `adr/ADR-030-v1-data-persistence-and-recovery-architecture.md`
- `agents/registry.yaml` v1.1 with A-001..A-033.
- Issue #16.

## Still benchmark-gated / open
- Base UI vs Radix primitive layer.
- ECharts vs uPlot or one-engine simplification.
- pg-boss vs smaller explicit PostgreSQL outbox/worker.
- exact TypeScript SQL/query/migration library.
- exact Redis activation threshold.
- exact dedicated-vector-DB threshold.
- exact graphics/LOD/DPR/worker budgets on representative hardware.
- exact SecretVault Windows/Docker provider.
- exact telemetry persistence/retention and numeric SLOs.
- exact UADS/HIVE/UGAS adapter API versions and bridge contracts at implementation time.

## Blockers
None for final HP-PLAN-008 audit/freeze.

## Implementation authorization
NOT GRANTED. Production code remains blocked until planning freeze audit authorizes the first implementation Work Order.

## Next necessary action
Perform the final HP-PLAN-008 architecture audit against issue #16, reconcile any contradictions, freeze the accepted stack/data/cockpit boundaries, merge the planning PR, then open the first implementation-readiness increment for the frontend-first cockpit vertical slice without yet allowing Codex to expand scope beyond its Work Order.