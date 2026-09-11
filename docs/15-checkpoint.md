# Checkpoint

Checkpoint ID: HP-CP-0010  
Status: PLANNING ACTIVE  
Canonical branch target: `main`  
Last canonical planning merge: `88858f5bb1b1d63e7bb2ea95acc2e0e139c9726f` (`HP-PLAN-003`)  
Active planning increment: `HP-PLAN-004`  
Active planning branch: `docs/hp-plan-004-work-order-compiler`

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

## Completed planning increments
- `HP-PLAN-001` — Interviewer + Planning Protocol and agent authority/escalation model.
- `HP-PLAN-002` — planning/delivery lifecycle, operational learning memory and GitHub governance; merged through PR #5.
- `HP-PLAN-003` — machine-readable artifact contracts; objectively audited and squash-merged through PR #7.

## Active planning increment
`HP-PLAN-004` — Work Order Compiler & Context Optimization Engine.

### HP-PLAN-004 current artifacts
- `docs/27-work-order-compiler-context-engine.md` — proposed architecture.
- `docs/28-work-order-technology-matrix.md` — candidate/adoption matrix.
- `docs/29-work-order-compiler-evals.md` — evals/regression-gate proposal.
- Issue #8.

## Current proposed direction
- Work Order compilation is a deterministic-first multi-pass compiler, not prose generation.
- Git/source resolution precedes semantic retrieval.
- Incremental content-addressed repository indexes avoid reparsing/re-embedding unchanged blobs.
- Adaptive lexical backend: simple fallback for small repos; indexed backend candidate for large/hot repos.
- Syntax/AST structural search behind a replaceable provider, with ast-grep as leading candidate.
- Hybrid retrieval combines exact, lexical, AST, dependency graph, semantic RAG and validated memory.
- FailureShield prevents recurrence of compatible prior failures.
- ChangeGraph predicts change surface/blast radius and learns from verified outcomes.
- TestLens maps acceptance criteria/change impact to required proof channels/tests.
- ContextCapsule budgets/deduplicates context and maximizes cache reuse.
- ExecutorFit adapts rendering to Codex/future executors without changing semantics.
- CompileGuard blocks stale/ambiguous/untestable/unsafe Work Orders before execution.
- Technology adoption is benchmark-gated and reversible.

## Open planning decisions
- Final HP-PLAN-004 architecture/freeze.
- Exact repository-size/query thresholds for indexed lexical backend after benchmarks.
- Exact hybrid retrieval fusion/reranking algorithm after evals.
- Exact local embedding/reranking profiles after hardware/quality benchmarks.
- Exact UADS/Hades V1 integration contract and compatible version.
- Data/persistence/vector-store benchmark decision.
- Initial model-provider/profile matrix and routing thresholds.
- Technology stack ADR.
- Detailed cockpit design system and interaction model.
- Numeric Planning Confidence/question-priority thresholds after evals.
- Byte-level contract digest golden vectors and validator runtime selection at implementation time.

## Blockers
None for continued planning.

## Implementation authorization
NOT GRANTED. Production code remains blocked until the planning freeze audit authorizes the first implementation Work Order.

## Next necessary discussion
Review the Work Order Compiler architecture, technology matrix and eval gates, then freeze only the architecture and benchmark-gated adoption rules. Exact third-party backend choices remain replaceable and evidence-driven.