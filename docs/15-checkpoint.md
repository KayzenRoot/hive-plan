# Checkpoint

Checkpoint ID: HP-CP-0009  
Status: PLANNING ACTIVE  
Canonical branch target: `main`  
Last canonical planning merge: `b5be6c0faf188b718fe2e8223f5afc34896143f0` (`HP-PLAN-002`)  
Active planning increment: `HP-PLAN-003`  
Active planning branch: `docs/hp-plan-003-artifact-contracts`

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
- Versioned machine-readable artifact contracts using canonical JSON + JSON Schema 2020-12.
- JCS-compatible canonicalization + SHA-256 artifact/context/evidence fingerprints.
- Review Receipt bound to exact head SHA + context root + evidence root.
- Completion Manifest as claim/trigger only; independently assembled Evidence Bundle as proof surface.
- Structured Correction Delta and Checkpoint Delta contracts.
- Unsupported major schema versions BLOCK rather than being guessed.

## Completed planning increments
- `HP-PLAN-001` — Interviewer + Planning Protocol and agent authority/escalation model.
- `HP-PLAN-002` — planning/delivery lifecycle, operational learning memory and GitHub governance; audited and squash-merged through PR #5.
- `HP-PLAN-003` — machine-readable artifact contracts; specification frozen and awaiting PR audit/merge.

## HP-PLAN-003 artifacts
- `docs/25-artifact-contracts.md` — frozen.
- `docs/26-contract-validation-test-plan.md` — frozen.
- `contracts/v1/*.schema.json` — Project Manifest, Context Lock, Work Order, Completion Manifest, Evidence Bundle, Review Receipt, Correction Delta and Checkpoint Delta.
- Decisions Ledger D-020.

## Open planning decisions
- Work Order Compiler/context optimization architecture.
- Exact UADS/Hades V1 integration contract and compatible version.
- Data/persistence/vector-store benchmark decision.
- Initial model-provider/profile matrix and routing thresholds.
- Technology stack ADR.
- Detailed cockpit design system and interaction model.
- Numeric Planning Confidence/question-priority thresholds after evals.
- Byte-level digest golden vectors and validator runtime selection at implementation time.

## Blockers
None for continued planning after HP-PLAN-003 audit.

## Implementation authorization
NOT GRANTED. Production code remains blocked until the planning freeze audit authorizes the first implementation Work Order.

## Proposed next planning increment
Define and freeze the Work Order Compiler and Context Optimization Engine: repository indexing, text/AST/symbol/dependency retrieval, RAG fusion, negative-knowledge preflight, change-surface prediction, test-impact mapping, context budgeting, provider prompt-cache layout, executor capability profiles and compile-time quality gates.