# Checkpoint

Checkpoint ID: HP-CP-0015  
Status: PLANNING ACTIVE  
Canonical branch target: `main`  
Last canonical planning merge: `a7de9c5fda68facdf82103ce72e9183bfd555bf4` (`HP-PLAN-005`)  
Active planning increment: `HP-PLAN-006`  
Active planning branch: `docs/hp-plan-006-event-auto-review`

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
- Model self-confidence cannot upgrade assurance; evidence and policy control escalation/acceptance.
- HIGH_ASSURANCE cannot silently degrade; temporary permitted degradation creates Quality Debt.
- Provider-neutral ModelMesh/RouteGuard/CacheFabric/BudgetPilot/ProviderSentinel/RouteLab architecture.
- Fingerprint-bound layered cache with provider-specific caching isolated behind adapters.
- Capability-aware failover and routing/cache promotion only through quality/regression evals.
- Local-first conditional GitHub observation with durable normalized EventSpine and optional webhook adapter.
- At-least-once event processing with idempotent handlers, ReviewLease and EffectLedger exactly-once-effect strategy.
- ReviewMVCC/SnapshotGuard: review bound to exact base/head SHA + context root + evidence root; stale review is cancelled.
- EvidenceForge + Evidence Watermark: expensive semantic review starts only after required proof channels exist.
- Focused Senior Review Engine: actual diff + risk-governed semantic impact closure instead of whole-repository review.
- Feature Impact Graph mapping feature/requirement → code/symbol/contract/data/test/runtime/failure with predicted/verified provenance.
- Conditional UADS specialist-agent review with non-overlapping scope, normalized findings and STRONG Senior Review Lead.
- FindingGate noise suppression: actionable evidence-grounded defects only; unrelated/style noise is excluded unless policy requires it.
- Delta-first correction review with impacted regression coverage preserved.
- Adapter-based static analysis portfolio with SARIF-compatible finding normalization and benchmark-gated tools.
- Incisive Review/Correction Prompt Compiler with per-agent scope, evidence obligations, task-dependency graph, no unrelated refactors and explicit STOP CONDITION.

## Completed planning increments
- `HP-PLAN-001` — Interviewer + Planning Protocol and agent authority/escalation model.
- `HP-PLAN-002` — planning/delivery lifecycle, operational learning memory and GitHub governance; merged through PR #5.
- `HP-PLAN-003` — machine-readable artifact contracts; objectively audited and squash-merged through PR #7.
- `HP-PLAN-004` — Work Order Compiler & Context Optimization Engine; objectively audited and squash-merged through PR #9.
- `HP-PLAN-005` — Model Router + Cache/Cost Engine; objectively audited and squash-merged through PR #11.
- `HP-PLAN-006` — Event Spine + Auto Review + Focused Senior Review architecture; specification frozen and awaiting objective PR audit/merge.

## HP-PLAN-006 artifacts
- `docs/42-event-spine-auto-review-orchestrator.md` — frozen architecture.
- `docs/43-event-auto-review-evals.md` — event correctness/fault/replay eval plan.
- `docs/43-focused-review-engine.md` — focused semantic senior review architecture.
- `docs/44-feature-impact-graph.md` — persistent feature/code/contract/test/failure impact intelligence.
- `docs/45-uads-review-agent-plan.md` — conditional UADS specialist review/prompt plan.
- `docs/46-review-engine-evals.md` — focused review/multi-agent/impact/noise regression gates.
- `docs/47-review-technology-matrix.md` — benchmark-gated static/test/review technology portfolio.
- `docs/48-review-prompt-compiler.md` — incisive review/correction prompt and UADS task-graph compiler.
- Decisions Ledger D-024 and D-025.
- Issue #12.

## Open planning decisions
- Exact durable journal/database + wake-up queue implementation after stack/data ADR.
- Exact active/idle polling intervals and quiescence windows after benchmarks.
- Exact optional webhook/tunnel technology if/when enabled.
- Exact review impact-expansion thresholds and static-analysis portfolio after review benchmarks.
- Exact UADS/Hades V1 invocation/integration contract, agent transport and model-per-agent profiles.
- Initial model/provider tier assignments and numeric routing/budget thresholds after evals/current-provider refresh.
- Exact safe-result-cache eligibility details after implementation threat/eval testing.
- Exact repository-size/query thresholds for indexed lexical backend after benchmarks.
- Exact hybrid retrieval fusion/reranking algorithm after evals.
- Exact local embedding/reranking profiles after hardware/quality benchmarks.
- Data/persistence/vector-store benchmark decision.
- Technology stack ADR.
- Detailed cockpit design system and interaction model.
- Numeric Planning Confidence/question-priority thresholds after evals.
- Byte-level contract digest golden vectors and validator runtime selection at implementation time.

## Blockers
None for objective HP-PLAN-006 audit/merge or continued planning.

## Implementation authorization
NOT GRANTED. Production code remains blocked until the planning freeze audit authorizes the first implementation Work Order.

## Proposed next planning increment
Define and freeze the UADS/Hades V1 integration + Agent Execution Contract: capability discovery, multi-agent plan transport, role/context isolation, executor task dependencies, conflict avoidance, structured completion/evidence outputs, cancellation/retry, model-profile mapping and prompt rendering. This should make Hive Plan-generated implementation/correction prompts directly exploit UADS multitasking without coupling canonical Work Orders to one executor.