# HP-PLAN-010 — Work Order ↔ Implementation Blueprint Integration Contract

Status: PROPOSED CORRECTION

## Purpose
Make the Implementation Blueprint a governed attachment to a Work Order rather than a free-floating prompt artifact.

## Compatibility rule
Do not rewrite the frozen Work Order v1 contract ad hoc. Integrate through a versioned extension/reference first, and promote to a future schema version only through normal contract governance.

## Blueprint identity
Every blueprint has:
- artifact_type = implementation_blueprint;
- schema_version;
- artifact_id;
- artifact_digest;
- project_id;
- increment_id;
- work_order_ref;
- context_lock_ref;
- executor_profile_ref where applicable;
- guidance_level G0/G1/G2/G3;
- decision_budget;
- source_fingerprints;
- generated_at;
- producer.

## Work Order linkage
Work Order carries a governed reference through `extensions.hive_plan.implementation_blueprint_ref` until a future schema promotion makes it first-class.

The rendered executor package MUST prove:
`Work Order digest -> Blueprint digest -> Context Lock digest -> source fingerprints`.

A blueprint cannot authorize scope beyond its Work Order.

## Compile order
1. validate Context Lock;
2. validate Work Order;
3. gather RepoPulse/ChangeGraph/TestLens/FailureShield inputs;
4. choose executor profile and guidance depth;
5. compile blueprint;
6. run BlueprintGuard;
7. render executor prompt/package;
8. persist exact digests/references.

## BlueprintGuard
Reject or block when:
- blueprint contradicts Work Order/ADR/contract;
- MUST_TOUCH prediction references nonexistent source without explicit create intent;
- FROZEN decision conflicts with repository reality;
- tests/evidence do not map to acceptance criteria;
- guidance depth is insufficient for risk/executor profile;
- guidance is bloated with irrelevant repository context;
- secret-bearing context would leak to executor/provider;
- blueprint introduces unapproved dependency/scope expansion.

## Correction rounds
Corrections reference the same Work Order and current blueprint lineage. Prefer Blueprint Delta + Context Diff rather than regenerating the complete package when unchanged sections remain valid.

## Completion Manifest
Executor must report blueprint digest consumed and all `BLUEPRINT_DEVIATION` records. A completion claim against an unknown/stale blueprint digest is not review-eligible.

## Metrics
Track blueprint compile tokens/latency, executor tokens, deviation rate, predicted-vs-actual surface, first-pass acceptance and verified outcome cost.

## STOP CONDITION
Freeze when blueprint identity/linkage, guard rules, correction lineage, completion reporting and backward-compatible Work Order attachment are represented in machine-readable contracts/tests.