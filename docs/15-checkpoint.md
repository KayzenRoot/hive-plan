# Checkpoint

Checkpoint ID: HP-CP-0021  
Status: PLANNING ACTIVE  
Canonical branch target: `main`  
Last canonical planning merge: `9343973050bc40998a2d897a7b6a19475f4606ad` (HP-PLAN-008)  
Active planning increment: `HP-PLAN-009`  
Active planning branch: `docs/hp-plan-009-cockpit-readiness`

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
- Principal ecosystem specialists A-031 HIVE, A-032 UGAS and A-033 UADS with EcosystemContextStamp and Tri-System Harmony Protocol.
- HP-PLAN-008 frozen stack/cockpit/data architecture: React/Vite/TanStack/Motion/R3F/Three.js progressive 3D; Node 24/Fastify modular monolith + workers; PostgreSQL 18 canonical durability; pgvector replaceable default; optional Redis; local CAS artifacts; snapshot+SSE projections; VisualTruthMirror; ResourcePeacekeeper; RestoreProof.

## Completed planning increments
- HP-PLAN-001 — Interviewer + Planning Protocol.
- HP-PLAN-002 — delivery lifecycle, operational memory and GitHub governance.
- HP-PLAN-003 — machine-readable artifact contracts.
- HP-PLAN-004 — Work Order Compiler & Context Optimization Engine.
- HP-PLAN-005 — Model Router + Cache/Cost Engine.
- HP-PLAN-006 — Event Spine + Auto Review + Focused Senior Review.
- HP-PLAN-007 — Governed Agent OS, skills/research fabric and UADS AgentTaskGraph.
- HP-PLAN-008 — application/runtime stack, cockpit/realtime architecture, data/persistence/recovery and ecosystem specialists; audited/merged through PR #18.

## Active HP-PLAN-009 objective
Prepare the first cockpit vertical slice as one bounded implementation-ready package without authorizing uncontrolled production coding.

## Newly specified in HP-PLAN-009
- `docs/82-cockpit-design-tokens-and-component-contract.md` — semantic design tokens, surface classes, component inventory, state completeness and motion rules.
- `docs/83-cockpit-contracts-and-api-surface.md` — versioned projection DTOs, minimal REST surface, SSE envelope and freshness vocabulary.
- `docs/84-first-slice-postgres-bootstrap.md` — minimum PostgreSQL tables and persistence authority boundaries.
- `docs/85-first-slice-agent-taskgraph.md` — bounded UADS AgentTaskGraph with WRITE_SET/READ_SET/WATCH_SET and safe-parallelism rules.
- `docs/86-first-cockpit-work-order-candidate.md` — HP-WO-0001 candidate with AC-01..AC-15, evidence obligations and STOP CONDITION; explicitly NOT AUTHORIZED.

## First-slice key invariants
- no fake metrics, seeded healthy integrations or demo-only success paths;
- every runtime component has CURRENT/STALE/DEGRADED/UNKNOWN/NOT_CONNECTED/NOT_AVAILABLE semantics as applicable;
- 3D remains optional and never owns critical state;
- first slice must remain useful with HIVE/UADS/UGAS disconnected;
- external ecosystem stubs are read-only/no-mutation in HP-WO-0001;
- PostgreSQL is required for canonical slice state; Redis is not required;
- shared contracts precede frontend/backend divergence;
- UADS parallelism requires disjoint ownership or explicit serialization;
- acceptance includes performance, accessibility, reconnect, restart/recovery and security evidence.

## Still benchmark/implementation-detail gated
- Base UI vs Radix primitive choice.
- exact font family and numeric design-token values.
- exact chart engine.
- exact TypeScript query/migration library.
- exact graphics DPR/LOD/frame budgets.
- exact pg-boss/outbox implementation for later worker-heavy slices.
- exact SecretVault provider.
- numeric local SLOs.

## Current blockers
None for continued HP-PLAN-009 planning audit. Production implementation remains blocked by authorization gate.

## Implementation authorization
NOT GRANTED.
HP-WO-0001 remains a candidate and MUST NOT be sent to Codex/UADS until objective audit, CompileGuard and Context Lock pass and policy promotes it to AUTHORIZED.

## Next necessary action
Pressure-test HP-WO-0001 and the first-slice contracts for ambiguity, missing failure states, frontend/backend/data conflicts, security gaps and unverifiable acceptance criteria. Then freeze HP-PLAN-009 readiness artifacts, create the Context Lock against current canonical main, and decide whether the first implementation Work Order can be authorized.