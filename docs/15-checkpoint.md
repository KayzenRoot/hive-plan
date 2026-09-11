# Checkpoint

Checkpoint ID: HP-CP-0016  
Status: PLANNING ACTIVE  
Canonical branch target: `main`  
Last canonical planning merge: `a1830a317c1fd5bef77409b5bc00426ec85d6c75` (`HP-PLAN-006`)  
Active planning increment: `HP-PLAN-007`  
Active planning branch: `docs/hp-plan-007-uads-agent-contract`

## Frozen
- Product identity and V1 mission.
- Local-first single-user Docker deployment.
- GitHub as canonical truth.
- Hive V1 preferred MemoryProvider + embedded local-RAG fallback.
- Codex as external executor in V1.
- Cheap-model default + risk/complexity escalation + aggressive caching/context optimization.
- Professional specialized agent organization.
- Automatic completion-triggered review with independent evidence verification.
- Dark technological command cockpit and early frontend vertical slice.
- Context-first interviewing, specialist escalation, Assumption Register, Planning Confidence Map and Decision Pressure Test.
- Agent authority levels, discovery Stop Condition and governed innovation lane.
- Operational learning memory with successful patterns plus failure/negative knowledge and provenance.
- Stable increment identity, short-lived GitHub branches, governed PRs, SemVer/release lifecycle and SHA-based canonical promotion.
- Verified-throughput objective, deterministic-first review and correction-in-place.
- Machine-readable artifact contracts with JSON Schema 2020-12, JCS-compatible SHA-256 fingerprints, Review Receipts and Checkpoint Deltas.
- Work Order Compiler architecture: RepoPulse, ChangeGraph, FailureShield, TestLens, ContextCapsule, ExecutorFit and CompileGuard.
- Deterministic-first search cascade and content-addressed incremental caches.
- Benchmark-gated, replaceable search/parser/embedding/reranking backends.
- Risk-weighted compiler evals and downstream verified-outcome regression gates.
- QualityFloor tiers T0 DETERMINISTIC, T1 FAST_CHEAP, T2 BALANCED, T3 STRONG and T4 HIGH_ASSURANCE.
- Verified Outcome Cost + Rework Tax as routing economics rather than isolated API-call price.
- HIGH_ASSURANCE cannot silently degrade; temporary permitted degradation creates Quality Debt.
- Provider-neutral ModelMesh/RouteGuard/CacheFabric/BudgetPilot/ProviderSentinel/RouteLab architecture.
- Fingerprint-bound layered cache with provider-specific caching isolated behind adapters.
- Local-first conditional GitHub observation with durable normalized EventSpine and optional webhook adapter.
- At-least-once event processing with idempotent handlers, ReviewLease and EffectLedger exactly-once-effect strategy.
- ReviewMVCC/SnapshotGuard: review bound to exact base/head SHA + context root + evidence root; stale review is cancelled.
- EvidenceForge + Evidence Watermark: semantic review starts only after required proof channels exist.
- Focused Senior Review Engine: actual diff + risk-governed semantic impact closure instead of whole-repository review.
- Feature Impact Graph mapping feature/requirement → code/symbol/contract/data/test/runtime/failure with predicted/verified provenance.
- Conditional UADS specialist-agent review with non-overlapping scope, normalized findings and STRONG Senior Review Lead.
- FindingGate noise suppression and delta-first correction review.
- Adapter-based static-analysis portfolio with SARIF-compatible finding normalization and benchmark-gated tools.
- Incisive Review/Correction Prompt Compiler with per-agent scope, evidence obligations, task DAG, no unrelated refactors and explicit STOP CONDITION.

## Completed planning increments
- `HP-PLAN-001` — Interviewer + Planning Protocol and agent authority/escalation model.
- `HP-PLAN-002` — planning/delivery lifecycle, operational learning memory and GitHub governance; merged through PR #5.
- `HP-PLAN-003` — machine-readable artifact contracts; audited and squash-merged through PR #7.
- `HP-PLAN-004` — Work Order Compiler & Context Optimization Engine; audited and squash-merged through PR #9.
- `HP-PLAN-005` — Model Router + Cache/Cost Engine; audited and squash-merged through PR #11.
- `HP-PLAN-006` — Event Spine + Auto Review + Focused Senior Review architecture; audited and squash-merged through PR #13 (`a1830a317c1fd5bef77409b5bc00426ec85d6c75`).

## Active planning increment
`HP-PLAN-007` — UADS/Hades V1 Agent Execution Contract.

### Objective
Compile executor-neutral Work Orders/Correction Deltas into safe multi-agent execution DAGs that UADS/Hades can exploit without polluting canonical project semantics or increasing merge conflicts, duplicate work or unverified executor claims.

### Planned HP-PLAN-007 subjects
- Executor Capability Manifest / capability handshake.
- AgentTaskGraph with dependency DAG and parallelism policy.
- Per-agent role, scope, ContextCapsule and proof obligations.
- File/symbol ownership hints and conflict avoidance.
- Cancellation/retry/resume and partial-failure semantics.
- Structured per-agent completion results and aggregate Completion Manifest.
- Evidence Bundle correlation across agents.
- Model/profile hints mapped through ModelMesh/QualityFloor.
- UADS/Hades adapter plus safe fallback to single-agent Codex.
- Multi-agent vs single-agent benchmark/eval gates.
- Issue #14.

## Open planning decisions
- Exact UADS/Hades V1 invocation syntax, version/capability discovery and adapter transport.
- Exact conflict-safe workspace strategy supported by UADS/Hades, if any.
- Exact agent task/context/output contracts after this increment.
- Exact durable journal/database + wake-up queue implementation after stack/data ADR.
- Exact polling/quiescence thresholds after benchmarks.
- Exact review impact-expansion thresholds and analyzer portfolio after review benchmarks.
- Initial model/provider tier assignments and numeric routing/budget thresholds after evals/current-provider refresh.
- Exact Work Order compiler backend thresholds/retrieval fusion/local embedding profiles after benchmark.
- Data/persistence/vector-store benchmark decision.
- Technology stack ADR.
- Detailed cockpit design system and interaction model.
- Numeric Planning Confidence/question-priority thresholds after evals.
- Byte-level artifact digest golden vectors and validator runtime selection at implementation time.

## Blockers
None for continued planning.

## Implementation authorization
NOT GRANTED. Production code remains blocked until the planning freeze audit authorizes the first implementation Work Order.

## Next necessary discussion
Define the AgentTaskGraph / Executor Capability Manifest boundary: what Hive Plan may safely parallelize, how agents receive isolated context and file/symbol ownership, and how per-agent outputs become one evidence-backed completion surface without executor-specific semantics entering the canonical Work Order.