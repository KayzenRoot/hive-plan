# HP-PLAN-010 — Executor Blueprint Contract

Status: PROPOSED

## Mission
Give low-cost executors a near-mechanical implementation contract so architecture/reasoning stays in Hive Plan and execution stays bounded.

## Blueprint sections
1. Identity: project, Work Order, branch, base/head/context fingerprints.
2. Objective: single bounded implementation outcome.
3. Scope: IN / OUT / MUST_NOT_TOUCH.
4. Preconditions: environment, required services, migrations, feature flags.
5. Change Surface: MUST_TOUCH / LIKELY_TOUCH / WATCH_ONLY.
6. File Plan: create/update/delete candidates with reason.
7. Symbol Plan: classes/functions/components/types/schemas with expected signatures where known.
8. Data Flow: request/event/state/storage movement.
9. Algorithm Plan: deterministic steps/pseudocode.
10. Contracts: API/schema/event/error/telemetry contracts.
11. Error Handling: failure taxonomy and expected behavior.
12. Edge Cases: explicit adversarial/boundary conditions.
13. FailureShield: relevant prior verified failures and prevention constraints.
14. Test Plan: unit/integration/e2e/property/perf/security as applicable.
15. Evidence Plan: exact evidence required for acceptance.
16. Observability: logs/metrics/traces/events required.
17. Migration/Rollback: when applicable.
18. Blueprint Deviations: allowed only with repository evidence and declared impact.
19. STOP CONDITION.

## Guidance levels
- G0 CONTRACT_ONLY: trivial/localized tasks.
- G1 STRUCTURAL: files, symbols, contracts, tests.
- G2 ALGORITHMIC: adds data flow, pseudocode, edge/error cases.
- G3 NEAR_EXECUTABLE: adds signatures, ordered implementation steps, detailed tests/evidence and narrowly bounded choices.

## G3 selection signals
Prefer G3 when one or more are true:
- executor model quality is below planning model;
- risk is ELEVATED/HIGH_ASSURANCE;
- similar prior failures exist;
- task spans multiple contracts/modules;
- rework cost is high;
- migration/security/concurrency/state machine involved;
- architecture choice already frozen and executor should not redesign it.

## Decision budget
Every blueprint includes a `decision_budget`:
- FROZEN: executor must follow exact decision;
- BOUNDED: choose among listed alternatives using stated criterion;
- OPEN_LOCAL: implementation-local choice that does not affect architecture/contracts;
- ESCALATE: executor must stop and report if encountered.

## Repository Reality Rule
Repository reality overrides stale assumptions, but never silently. Any material mismatch emits `BLUEPRINT_DEVIATION` with expected state, actual state, evidence, proposed bounded correction and impact on tests/contracts/context lock.

## Anti-overengineering
A detailed blueprint must not force speculative abstractions. Prefer existing project patterns and the minimal implementation needed to satisfy the Work Order.