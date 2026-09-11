# Checkpoint

Checkpoint ID: HP-CP-0014  
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

## Completed planning increments
- `HP-PLAN-001` — Interviewer + Planning Protocol and agent authority/escalation model.
- `HP-PLAN-002` — planning/delivery lifecycle, operational learning memory and GitHub governance; merged through PR #5.
- `HP-PLAN-003` — machine-readable artifact contracts; objectively audited and squash-merged through PR #7.
- `HP-PLAN-004` — Work Order Compiler & Context Optimization Engine; objectively audited and squash-merged through PR #9.
- `HP-PLAN-005` — Model Router + Cache/Cost Engine; objectively audited and squash-merged through PR #11.

## Active planning increment
`HP-PLAN-006` — Event Spine + Auto Review Orchestrator.

### HP-PLAN-006 current artifacts
- `docs/42-event-spine-auto-review-orchestrator.md` — proposed architecture.
- `docs/43-event-auto-review-evals.md` — proposed correctness/fault/replay eval plan.
- Issue #12.

## Current proposed direction
- Local V1 observes GitHub through authenticated conditional polling by default; webhook/tunnel is optional.
- GitPulse uses ETag/304, X-Poll-Interval compliance, adaptive cadence and minimal API reads.
- EventSpine is a durable append-only normalized event journal; events are signals, not authority.
- Reliability target is at-least-once observation/processing + idempotent handlers + exactly-once-effect semantics where practical.
- EffectLedger/outbox-like tracking and ReviewLease prevent duplicate external review/correction/checkpoint effects.
- ReviewGate is an explicit persisted eligibility state machine.
- SnapshotGuard/ReviewMVCC pins base SHA + head SHA + context root + evidence root and cancels stale in-flight reviews.
- EvidenceForge independently assembles Evidence Bundles from GitHub/CI/tool facts.
- Evidence Watermark prevents semantic review until every required proof channel is satisfied/authorized.
- Quiescence Guard avoids reviewing transient rapid-push states.
- deterministic/evidence preflight occurs before expensive model review.
- correction cycles regenerate bounded Correction Deltas and are re-observed automatically.
- crash/restart recovery reconciles durable state against GitHub instead of restarting workflows blindly.

## Open planning decisions
- Final HP-PLAN-006 architecture/freeze.
- Exact durable journal/database + wake-up queue implementation after stack/data ADR.
- Exact active/idle polling intervals and quiescence windows after benchmarks.
- Exact optional webhook/tunnel technology if/when enabled.
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
None for continued planning.

## Implementation authorization
NOT GRANTED. Production code remains blocked until the planning freeze audit authorizes the first implementation Work Order.

## Next necessary discussion
Review and refine the Event Spine/Auto Review design, especially polling vs optional webhooks, ReviewMVCC/stale-head cancellation, Evidence Watermark, durable idempotency/effect semantics and operator-notification behavior before freezing HP-PLAN-006.