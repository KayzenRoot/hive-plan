# Checkpoint

Checkpoint ID: HP-CP-0012  
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

## Completed planning increments
- `HP-PLAN-001` — Interviewer + Planning Protocol and agent authority/escalation model.
- `HP-PLAN-002` — planning/delivery lifecycle, operational learning memory and GitHub governance; merged through PR #5.
- `HP-PLAN-003` — machine-readable artifact contracts; objectively audited and squash-merged through PR #7.
- `HP-PLAN-004` — Work Order Compiler & Context Optimization Engine; objectively audited and squash-merged through PR #9.

## Active planning increment
`HP-PLAN-005` — Model Router + Cache/Cost Engine.

### HP-PLAN-005 current artifacts
- `docs/34-model-router-cache-cost-engine.md` — proposed architecture.
- `docs/35-model-router-cache-evals.md` — proposed eval/regression policy.
- Issue #10.

## Current proposed direction
- RouteGuard classifies task/risk/assurance before selecting a model.
- ModelMesh keeps provider/model capabilities replaceable and telemetry-backed.
- QualityFloor prevents cost optimization from silently lowering assurance.
- CacheFabric layers deterministic, retrieval, semantic, ContextCapsule, safe result and provider caches.
- Cache reuse is fingerprint-bound to canonical state, policy, prompt/template, model/tool/schema dependencies.
- BudgetPilot tracks token/money/latency budgets without overriding QualityFloor.
- ProviderSentinel supplies health telemetry, bounded retries, circuit breakers and capability-aware failover.
- RouteLab uses shadow routing/evals before policy promotion.
- Provider-specific prompt/context caching is an adapter capability, not core workflow semantics.

## Open planning decisions
- Final HP-PLAN-005 architecture/freeze.
- Initial model/provider capability profiles and routing thresholds after current-provider research/evals.
- Exact safe-result-cache eligibility policy.
- Exact cost/latency budget defaults by task class.
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
None for continued planning.

## Implementation authorization
NOT GRANTED. Production code remains blocked until the planning freeze audit authorizes the first implementation Work Order.

## Next necessary discussion
Review the proposed Model Router + Cache/Cost architecture, especially QualityFloor, cache safety/invalidation, failover semantics and whether V1 should start with one provider plus provider-neutral adapters or multiple live providers from day one.