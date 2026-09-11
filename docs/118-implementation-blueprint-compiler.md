# HP-PLAN-010 — Implementation Blueprint Compiler

Status: PROPOSED

## Mission
Move high-value reasoning upstream into Hive Plan so lower-cost executors spend most of their effort implementing a pre-decided engineering plan rather than rediscovering architecture, scope and code strategy.

## Principle
A Work Order SHOULD include an `Implementation Blueprint` whenever the change is complex enough that executor interpretation is a meaningful source of defects, token usage or rework.

Hive Plan decides the engineering intent. The executor implements and verifies it.

## Blueprint contents
For each functional change, compile:
- objective and user-visible behavior;
- exact scope and explicit non-scope;
- affected bounded contexts/modules;
- predicted MUST_TOUCH / LIKELY_TOUCH / WATCH_ONLY files or symbols;
- contracts/interfaces/types to add or change;
- function/class/component responsibilities;
- state transitions/data flow;
- algorithm or pseudocode for nontrivial logic;
- persistence/query/migration behavior where applicable;
- validation/error/retry/idempotency rules;
- concurrency/transaction boundaries where applicable;
- security/privacy/permission constraints;
- observability events/metrics/traces/logging expectations;
- backward compatibility/deprecation expectations;
- UI states/interactions/accessibility if applicable;
- tests to add/change by level;
- deterministic proof/evidence required;
- known prior failure patterns and prevention constraints;
- performance/resource budgets;
- implementation sequence and dependency ordering;
- forbidden shortcuts/anti-patterns;
- exact STOP CONDITION.

## Code-level guidance depth
The compiler chooses one of four guidance depths:
- G0 CONTRACT_ONLY: trivial/mechanical work;
- G1 STRUCTURAL: files, symbols, interfaces and tests;
- G2 ALGORITHMIC: G1 + data flow, pseudocode, edge cases, error behavior;
- G3 NEAR_EXECUTABLE: G2 + step-by-step implementation recipe, signatures/schema sketches and test matrix for high-risk/weak-executor tasks.

Higher depth is used when risk, ambiguity, novelty, repeated prior failure, weak executor profile or expensive rework justify it.

## Executor freedom
The executor MAY deviate from the blueprint only when:
- repository reality proves the predicted approach invalid;
- a simpler equivalent implementation satisfies all contracts and proof obligations;
- dependency/API reality differs from the locked source state;
- following the blueprint would introduce a defect.

Material deviation must be reported in the Completion Manifest with reason and evidence. Silent architecture invention is prohibited.

## Source grounding
Blueprint compilation uses RepoPulse, ChangeGraph, FailureShield, TestLens, canonical sources and exact repository symbols. It must not invent nonexistent files/APIs and must carry source fingerprints for critical assumptions.

## Token-efficiency strategy
Prefer compact structured directives over prose repetition. Reuse content-addressed ContextCapsules and stable contract references. Send only exact source excerpts needed for implementation.

## Review feedback loop
After merge, compare predicted vs actual files/symbols/tests, deviations, rework and defects. Feed results into ChangeGraph and future blueprint depth selection.

## Anti-overengineering rule
The blueprint must not prescribe incidental implementation details when multiple equivalent choices are low-risk. Constrain what matters to correctness, architecture, maintainability, performance and evidence.

## STOP CONDITION
Freeze only when guidance depth, required sections, deviation policy, source grounding and feedback metrics are machine-testable.