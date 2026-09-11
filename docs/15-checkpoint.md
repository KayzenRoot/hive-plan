# Checkpoint

Checkpoint ID: HP-CP-0013  
Status: PLANNING ACTIVE  
Canonical branch target: `main`  
Last canonical planning merge: `fb769014f1b4002aaa71942ef466f21760eeb935` (`HP-PLAN-004`)  
Active planning increment: `HP-PLAN-005`  
Active planning branch: `docs/hp-plan-005-model-router-cache`

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

## Completed planning increments
- `HP-PLAN-001` — Interviewer + Planning Protocol and agent authority/escalation model.
- `HP-PLAN-002` — planning/delivery lifecycle, operational learning memory and GitHub governance; merged through PR #5.
- `HP-PLAN-003` — machine-readable artifact contracts; objectively audited and squash-merged through PR #7.
- `HP-PLAN-004` — Work Order Compiler & Context Optimization Engine; objectively audited and squash-merged through PR #9.
- `HP-PLAN-005` — Model Router + Cache/Cost Engine; specification frozen and awaiting objective PR audit/merge.

## HP-PLAN-005 artifacts
- `docs/34-model-router-cache-cost-engine.md` — frozen architecture.
- `docs/35-quality-floor-routing-policy.md` — frozen QualityFloor/routing policy.
- `docs/36-routing-cache-evals.md` — frozen eval/regression policy.
- `docs/37-provider-capability-live-notes.md` — living, non-canonical provider research/config input.
- Decisions Ledger D-022 and D-023.
- Issue #10.

## Open planning decisions
- Initial model/provider tier assignments and numeric routing/budget thresholds after evals/current-provider refresh.
- Exact safe-result-cache eligibility details after implementation threat/eval testing.
- Exact repository-size/query thresholds for indexed lexical backend after benchmarks.
- Exact hybrid retrieval fusion/reranking algorithm after evals.
- Exact local embedding/reranking profiles after hardware/quality benchmarks.
- Exact UADS/Hades V1 integration contract and compatible version.
- Data/persistence/vector-store benchmark decision.
- Technology stack ADR.
- Detailed cockpit design system and interaction model.
- Numeric Planning Confidence/question-priority thresholds after evals.
- Byte-level contract digest golden vectors and validator runtime selection at implementation time.

## Blockers
None for continued planning after HP-PLAN-005 audit.

## Implementation authorization
NOT GRANTED. Production code remains blocked until the planning freeze audit authorizes the first implementation Work Order.

## Proposed next planning increment
Define and freeze the Event Spine + Auto Review Orchestrator: local GitHub observation strategy, completion-manifest/CI event correlation, event journal, idempotency/debounce, PR-head drift cancellation, review eligibility state machine, automatic Evidence Bundle assembly, review/audit triggering, correction prompt generation and operator notification. Webhook/tunnel support remains optional; local V1 must work without exposing the machine publicly.