# Checkpoint

Checkpoint ID: HP-CP-0019  
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
- Principal ecosystem specialists A-031 HIVE, A-032 UGAS and A-033 UADS are accepted by ADR-028 and use live repository truth + Tri-System Harmony Protocol.

## Completed planning increments
- HP-PLAN-001 — Interviewer + Planning Protocol.
- HP-PLAN-002 — delivery lifecycle, operational memory and GitHub governance.
- HP-PLAN-003 — machine-readable artifact contracts.
- HP-PLAN-004 — Work Order Compiler & Context Optimization Engine.
- HP-PLAN-005 — Model Router + Cache/Cost Engine.
- HP-PLAN-006 — Event Spine + Auto Review + Focused Senior Review.
- HP-PLAN-007 — Governed Agent OS, 30 senior/principal agents, skills/research fabric and UADS AgentTaskGraph; audited/merged through PR #15, status headers reconciled through PR #17.

## Active HP-PLAN-008
Objective: freeze the implementation technology stack and data/persistence architecture with unusually strong emphasis on a beautiful high-performance realtime cockpit and maintainable local-first backend.

### Current proposed direction
- React 19.3+ + TypeScript strict.
- Vite 8.1+/Rolldown client build system.
- TanStack Router + TanStack Query.
- Base UI candidate + Tailwind CSS 4.3 custom design layer.
- Motion for React.
- Three.js WebGPURenderer + React Three Fiber for optional data-driven 3D, WebGL2 fallback and adaptive graphics profiles.
- Node.js 24 LTS + TypeScript + Fastify backend.
- HTTP/REST commands + SSE default realtime/LLM stream; WebSocket only where benchmarked need exists.
- PostgreSQL 18 canonical datastore.
- pgvector default vector/RAG candidate.
- durable PostgreSQL event/outbox state with pg-boss as TRIAL candidate.
- Redis optional/non-canonical in standalone V1.
- content-addressed local artifact store for large immutable evidence/log assets.
- OpenTelemetry-compatible instrumentation.
- pnpm workspace modular monolith + workers, Docker Compose, no premature Kubernetes/microservices.

### Newly added ecosystem specialization
- A-031 Principal HIVE Systems Specialist.
- A-032 Principal UGAS Production Systems Specialist.
- A-033 Principal UADS Orchestration Specialist.
- `EcosystemContextStamp` freshness rule before consequential cross-system guidance.
- Cross-system skills require affected specialist reviews + SkillForge/security gates.
- HIVE = context/memory/intelligence substrate; UADS = engineering orchestration; UGAS = multimodal production; Hive Plan retains planning/governance/review authority.

### Pressure-test controls now proposed
- RenderBudget Governor + Frame-Time Circuit Breaker.
- VisualTruth Mirror and 2D semantic fallback for every critical 3D state.
- CockpitProjectionStore separating canonical server state, realtime projection, ephemeral UI and graphics state.
- PulseMux event classification/coalescing and ProjectionFence freshness protection.
- worker isolation for indexing/review/model/GitHub tasks.
- durable reconnect/event cursor for SSE projections.
- PostgreSQL authority classes, paired backup epoch, CAS reconciliation and Migration Gate.
- retrieval cascade exact/lexical/AST/FIG/vector/rerank/authority filter.
- ResourcePeacekeeper coordinating cockpit resource demand with local AI/UGAS/HIVE work.
- RestoreProof before recovered state is marked READY.
- trust zones, AgentGovernor authority checks, prompt/tool-injection containment, dependency circuit breakers, bulkheads and Incident Capsules.

## HP-PLAN-008 artifacts
- `docs/73-technology-stack-proposal.md`
- `docs/74-cockpit-frontend-visual-system.md`
- `docs/75-data-persistence-architecture.md`
- `docs/76-stack-benchmark-and-adoption-plan.md`
- `docs/77-hive-ugas-uads-specialist-agents.md`
- `docs/78-hp-plan-008-pressure-test.md`
- `docs/79-operational-security-observability-resilience.md`
- `adr/ADR-028-hive-ugas-uads-principal-specialists.md`
- `agents/registry.yaml` v1.1 with A-001..A-033.
- Issue #16.

## Frontend visual direction under review
Working language: **Obsidian Glass / Electric Signal**.
- dark graphite/obsidian cockpit;
- restrained glassmorphism;
- cyan/blue/violet signal spectrum;
- data-driven energy flow;
- optional central 3D Hive Core;
- real-time project/agent/review/cost/CI telemetry;
- cinematic, balanced, efficient and reduced-motion graphics tiers;
- 3D is progressive enhancement and never the sole representation of critical state;
- frontend vertical slice remains an early implementation priority.

## Open HP-PLAN-008 decisions
- Base UI vs Radix final primitive choice after slice benchmark.
- ECharts vs uPlot split by chart workload.
- pg-boss vs explicit lightweight Postgres worker/outbox implementation.
- exact TypeScript SQL/query/migration layer.
- exact Redis activation threshold.
- exact dedicated-vector-DB threshold.
- exact 3D graphics budgets/LOD/DPR/worker strategy after RTX 5050/browser benchmark.
- exact SecretVault Windows/Docker provider.
- exact local telemetry persistence/retention backend and numeric SLOs.
- exact UADS/HIVE/UGAS adapter API versions and bridge contracts at implementation time.

## Blockers
None for continued HP-PLAN-008 planning/research.

## Implementation authorization
NOT GRANTED. Production code remains blocked until planning freeze audit authorizes the first implementation Work Order.

## Next necessary discussion
Freeze or revise HP-PLAN-008 stack boundaries after final architecture pressure test, then define the first frontend-first vertical slice and its acceptance/benchmark/evidence contract without yet authorizing implementation.