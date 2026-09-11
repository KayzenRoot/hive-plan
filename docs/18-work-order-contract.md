# Work Order Contract

Every implementation increment uses one stable Work Order ID across prompt, branch, PR, evidence, corrections, review, audit, and checkpoint.

## Required sections
- ID
- OBJECTIVE
- CONTEXT
- SCOPE
- OUT OF SCOPE
- FILES/SOURCES TO READ
- REQUIREMENTS
- ARCHITECTURE RULES
- CONSTRAINTS
- ACCEPTANCE CRITERIA
- TESTS
- DELIVERABLES
- REVIEW FORMAT
- STOP CONDITION
- RISK CLASS
- CONTEXT LOCK / source fingerprints when available

## Context Lock
A Work Order records the Git base and fingerprints/versions of critical sources. If Checkpoint, Scope, DoD, Architecture, Security, or a relevant approved decision changes, the Work Order becomes STALE until reconciled/rebased.

## Correction Delta
Corrections preserve the original Work Order identity and PR when safe. A Correction Delta contains only verified defects, impacted acceptance criteria, required changes, required regression checks, and the same stop condition lineage.

## Executor evidence bundle
At completion, executor should provide or reference:
- base/head SHA;
- files changed;
- decisions/assumptions;
- tests and results;
- lint/typecheck/build results where applicable;
- security/migration/benchmark/recovery results when applicable;
- errors discovered and corrected;
- remaining risks;
- evidence/artifact references;
- proposed Checkpoint Delta.

`COMPLETED` is a state claim, not proof. Hive Plan independently verifies evidence.
