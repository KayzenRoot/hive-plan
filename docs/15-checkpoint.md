# Checkpoint

Checkpoint ID: HP-CP-0008  
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
- Canonical Source Pack foundation.
- Context-first adaptive interviewing, specialist escalation, Assumption Register, Planning Confidence Map and Decision Pressure Test.
- Governed agent authority levels and explicit discovery Stop Condition.
- Innovation governance without silent scope expansion.
- Operational learning memory with provenance, authority, successful patterns and failure/negative knowledge.
- Stable increment identity and prior-failure retrieval before Work Order finalization.
- Layered deterministic-first review, correction-in-place and verified-throughput optimization.
- Professional GitHub lifecycle: short-lived branches, governed planning/implementation PRs, freeze semantics, SemVer, immutable release tags, evidence-based patches, SHA promotion, health signals and publication safeguards.

## Completed planning increments
- `HP-PLAN-001` — Interviewer + Planning Protocol and agent authority/escalation model.
- `HP-PLAN-002` — planning/delivery lifecycle, operational learning memory and GitHub governance; audited and squash-merged through PR #5.

## Active planning increment
`HP-PLAN-003` — versioned machine-readable artifact contracts.

### Proposed HP-PLAN-003 artifacts
- `docs/25-artifact-contracts.md`
- `docs/26-contract-validation-test-plan.md`
- `contracts/v1/common.schema.json`
- `contracts/v1/project-manifest.schema.json`
- `contracts/v1/context-lock.schema.json`
- `contracts/v1/work-order.schema.json`
- `contracts/v1/completion-manifest.schema.json`
- `contracts/v1/evidence-bundle.schema.json`
- `contracts/v1/review-receipt.schema.json`
- `contracts/v1/correction-delta.schema.json`
- `contracts/v1/checkpoint-delta.schema.json`

## Proposed technical direction under discussion
- JSON as canonical contract representation.
- JSON Schema Draft 2020-12 deterministic validation.
- JCS-compatible canonicalization + SHA-256 canonical artifact/context/evidence digests.
- Review Receipt bound to exact Git head SHA + context root + evidence root.
- Completion Manifest remains a trigger/claim, never proof.
- Checkpoint Delta is first-class so canonical promotion is structured rather than prose-only.
- Unknown core fields rejected; provider/executor fields namespaced under extensions.
- Contract version compatibility explicitly governed; unsupported major versions BLOCK.
- Large/sensitive evidence referenced by location + digest rather than embedded by default.

## Open planning decisions
- Final HP-PLAN-003 contract field semantics and freeze.
- Exact digest self-field convention and frozen byte-level test vectors.
- Exact UADS/Hades V1 integration contract and current compatible version.
- Data/persistence/vector-store benchmark decision.
- Initial model-provider/profile matrix and routing thresholds.
- Technology stack ADR.
- Detailed cockpit design system and interaction model.
- Numeric Planning Confidence/question-priority thresholds after evals.

## Blockers
None for continued planning.

## Implementation authorization
NOT GRANTED. Production code remains blocked until the planning freeze audit authorizes the first implementation Work Order.

## Next necessary discussion
Review and freeze the HP-PLAN-003 contract architecture, especially canonical JSON/schema versioning, digest/fingerprint semantics, Review Receipt invalidation and Checkpoint Delta promotion behavior.
