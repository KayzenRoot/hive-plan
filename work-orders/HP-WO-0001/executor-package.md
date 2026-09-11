# HP-WO-0001 — UADS / Codex Executor Package

Status: PENDING FINAL AUTHORIZATION PR AUDIT

## Absolute instruction
Execute **only** the canonical `work-orders/HP-WO-0001/work-order.json` after authorization is merged and its Context Lock is revalidated. This file is a rendering aid, not a second source of truth.

If any critical source fingerprint differs from `work-orders/HP-WO-0001/context-lock.json`, STOP and report `STALE_CONTEXT_LOCK`. Do not reinterpret or continue from memory.

## Objective
Build the first bounded, frontend-first, end-to-end Hive Plan cockpit foundation with truthful runtime states, PostgreSQL durability, snapshot+SSE projections, optional adaptive Hive Core 3D, accessible 2D semantic parity, and no external HIVE/UADS/UGAS mutations.

## UADS team composition
Use the smallest conflict-safe team. Tasks derive from `docs/85-first-slice-agent-taskgraph.md`.

### Agent T1 — Platform bootstrap
Role: A-015 Senior Platform / Infrastructure Engineer.
Own: workspace, package manager, Docker/Compose, environment bootstrap.
Do not implement product UI/API logic.

### Agent T2 — Contracts
Role: A-011 Senior API & Integration Engineer, A-004 support.
Own: shared DTO/schema contracts and validation fixtures.
Contracts freeze before dependent implementation diverges.

### Agent T3 — Data
Role: A-012 Senior Data Engineer / DBA, A-023 recovery support.
Own: PostgreSQL migration/bootstrap/schema tests.
Do not introduce full RAG/vector schema or Redis dependency.

### Agent T4 — Backend
Role: A-010 Senior Backend Engineer, A-011/A-021 support.
Own: Fastify API, projection builders, SSE transport and bounded persistence adapters.
No broad mutation APIs.

### Agent T5 — Frontend cockpit
Role: A-013 Senior Frontend/UI Engineer, A-014 UX support.
Own: shell, navigation, workspace, live rail, telemetry strip, design-token implementation and complete semantic states.

### Agent T6 — Hive Core
Role: A-013 under serialized frontend ownership, A-020 performance support.
Own: optional R3F/Three.js Hive Core, VisualTruthMirror binding, graphics fallback/governor.
Never hide critical state inside canvas.

### Agent T7 — Ecosystem seams
Role: A-011; reviews by A-031 HIVE, A-032 UGAS, A-033 UADS.
Own: Hive Plan-side read-only adapter interfaces/stubs.
Zero external mutation attempts.

### Agent T8 — QA/evidence
Role: A-022 Principal QA, with A-020/A-017/A-021.
Own: tests, event storm, accessibility, performance, recovery, security and evidence harness.
Start early; final evidence runs only on fixed integration head.

### T9 — Review
A-027 Senior Review Lead + A-028 independent auditor.
Do not self-certify implementation tasks.

## Parallelism
Permitted only where WRITE_SET ownership is disjoint. T2/T3 may follow T1 in parallel. T5 may build from frozen contract fixtures while T4 proceeds. T7 may proceed against shared contracts. T8 starts early.

Serialize immediately if two tasks need the same files/symbols or if shared contracts change after consumers exist.

Any required write outside assigned ownership returns:
`SCOPE_EXPANSION_REQUIRED`
with path/symbol, rationale, acceptance criterion affected, and proposed ownership change. Do not edit first and explain later.

## Hard prohibitions
Do NOT:
- implement full HIVE/RAG;
- invoke UADS host execution as a product feature;
- generate through UGAS;
- add cloud/multi-user auth;
- require Redis;
- add Kubernetes/microservices;
- add separate vector DB;
- implement full model/cost router;
- create plugin marketplace;
- refactor unrelated code;
- fabricate health, cost, token, CI, review or integration success;
- mutate external HIVE/UADS/UGAS systems;
- change frozen architecture without `SCOPE_EXPANSION_REQUIRED` and governed correction.

## Truth rules
Use only CURRENT / STALE / DEGRADED / UNKNOWN / NOT_CONNECTED / NOT_AVAILABLE according to the frozen contracts. Missing or timed-out telemetry is never `0`, `healthy` or `CURRENT` unless evidence supports that state.

A development sample project, if needed, must be explicitly marked `LOCAL_DEVELOPMENT_FIXTURE`, persisted in PostgreSQL, and must not create fake operational signals.

## Implementation-time bounded decisions
You may choose Base UI vs Radix, the TypeScript query/migration library, exact fonts/token numerics, event-storm rate/duration and WebGPU subset only within frozen boundaries. For each choice:
1. prefer the simpler viable option;
2. record rationale/evidence;
3. do not widen infrastructure;
4. preserve adapters/reversibility.

## Required proof
Every AC-01..AC-15 in the canonical JSON is mandatory. No prose claim substitutes for evidence.

The final evidence package must bind to the exact final head and include build/type/test, DB migration/restart, nine visual states, keyboard/accessibility, event-storm/long-task data, SSE reconciliation, graphics fallback, no-secret/security evidence, API contracts, and zero-mutation ecosystem tests.

## Completion output
Write the canonical Completion Manifest required by Hive Plan. `COMPLETED` is allowed only after every applicable AC has proof on exact head. Otherwise return `BLOCKED` with criterion IDs and evidence gaps.

## STOP CONDITION
The exact STOP CONDITION in `work-order.json` is binding. Do not continue into later Hive Plan modules after this slice is complete.