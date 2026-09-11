# HP-PLAN-006 Review Freeze Summary

Status: FROZEN — pending PR audit/merge

The HP-PLAN-006 review subsystem freezes these principles:

1. Auto-review is event-driven/local-first and starts only on an eligible immutable snapshot.
2. Completion manifests are triggers/claims; EvidenceForge assembles proof independently.
3. ReviewScope is actual diff plus semantic impact closure, not the whole repository.
4. Feature Impact Graph continuously maps capabilities to code/contracts/data/tests/runtime/failures with provenance.
5. Deterministic/static/test analysis runs before expensive semantic review.
6. UADS specialists are spawned conditionally from distinct affected risk domains, with non-overlapping scopes.
7. Senior Review Lead is the semantic adjudicator; independent audit remains required by risk/authority policy.
8. Findings must be actionable, evidence-grounded and deduplicated; style/unrelated legacy noise is suppressed.
9. Correction prompts are delta-first, scope-locked, agent-decomposable and test/evidence bound.
10. Review quality is measured by escaped defects/false approvals/impact coverage alongside wall-clock and cost.
11. ReviewMVCC cancels stale work when head/context/evidence changes.
12. Technology choices such as CodeQL/Semgrep/mutation/fuzzing are portfolio adapters promoted by measured unique defect yield.

Exact thresholds, analyzer mix and UADS invocation syntax remain benchmark/integration decisions.