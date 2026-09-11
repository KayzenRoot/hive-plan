# First Slice AgentTaskGraph

Status: PROPOSED FOR FREEZE — HP-PLAN-009

## Goal
Pre-compose the minimum safe multi-agent execution plan for the first cockpit slice so UADS can parallelize only where ownership is demonstrably conflict-safe.

## Canonical rule
One Work Order remains authoritative. Agent tasks are derived execution partitions only and may not change scope, acceptance criteria, architecture or evidence obligations.

## Proposed task graph

### T1 — Repository/bootstrap foundation
Owner: A-015 Senior Platform / Infrastructure Engineer
Support: A-016 DevOps / Release
WRITE_SET:
- workspace/package manager/bootstrap files
- Docker/Compose bootstrap
- environment templates without secrets
READ_SET:
- ADR-029/030
- first-slice docs
WATCH_SET:
- API/web package manifests
Proof:
- clean install/build
- compose config validation
- localhost-only defaults

### T2 — Shared contracts
Owner: A-011 Senior API & Integration Engineer
Support: A-004 Requirements Engineer
WRITE_SET:
- shared schema/DTO package
- validation fixtures
READ_SET:
- docs/81, docs/83
WATCH_SET:
- API routes, frontend projection consumers
Proof:
- schema tests
- invalid-state tests
- no-secret projection fixture
Dependency: none after T1 package layout exists.

### T3 — PostgreSQL bootstrap
Owner: A-012 Senior Data Engineer / DBA
Support: A-023 Migration / Recovery Engineer
WRITE_SET:
- migration files
- DB bootstrap/config package
- schema tests
READ_SET:
- ADR-030
- docs/84
WATCH_SET:
- API persistence adapters
Proof:
- clean DB migration
- restart persistence
- rollback/recovery evidence as applicable
Dependency: T1.

### T4 — Backend cockpit API
Owner: A-010 Senior Backend Engineer
Support: A-011 API Engineer, A-021 Observability
WRITE_SET:
- API routes/services/projection builders
- SSE transport
READ_SET:
- shared contracts
- migration interfaces
WATCH_SET:
- frontend consumers
Proof:
- contract tests
- truthful NOT_CONNECTED/NOT_AVAILABLE states
- SSE watermark/reconnect tests
Dependencies: T2 + T3.

### T5 — Cockpit shell/UI
Owner: A-013 Senior Frontend / UI Engineer
Support: A-014 Principal UX/Product Design
WRITE_SET:
- app shell/navigation/workspace/live rail/telemetry strip
- design token implementation
- component states
READ_SET:
- docs/82/83
- shared contracts
WATCH_SET:
- API projection shapes
Proof:
- visual state matrix
- keyboard navigation
- responsive/density checks
Dependency: T2; can begin with contract fixtures before T4 completes.

### T6 — Hive Core + VisualTruth Mirror
Owner: A-013 Senior Frontend / UI Engineer or dedicated graphics subtask under same ownership
Support: A-020 Performance Engineer, A-014 UX
WRITE_SET:
- Hive Core renderer/scene module
- VisualTruthMirror binding
- graphics governor/fallback code
READ_SET:
- cockpit projection selectors
WATCH_SET:
- semantic status tokens
Proof:
- WebGPU/WebGL2/2D fallback
- reduced mode
- no critical information lost
Dependency: T5 shell + T2 contracts.

### T7 — Ecosystem adapter stubs
Owner: A-011 API Engineer
Specialist review: A-031 HIVE, A-032 UGAS, A-033 UADS
WRITE_SET:
- Hive Plan-side adapter interfaces/stubs only
READ_SET:
- live ecosystem specialist policy/ADRs
WATCH_SET:
- external repositories are read-only evidence sources
Proof:
- explicit NOT_CONNECTED state
- no accidental mutation of HIVE/UADS/UGAS
- adapter contract tests
Dependency: T2.

### T8 — Test/benchmark/evidence harness
Owner: A-022 Principal QA / Test Engineer
Support: A-020 Performance, A-017 Security, A-021 Observability
WRITE_SET:
- tests/evals/bench harness/evidence scripts
READ_SET:
- all acceptance criteria
WATCH_SET:
- implementation outputs
Proof:
- browser integration
- accessibility
- event storm/reconnect
- restart/recovery
- security/secret scan
- graphics profile benchmark
Dependencies: starts early after T1, finalizes after T4-T7.

### T9 — Senior review and audit
Owner: A-027 Senior Review Lead
Independent: A-028 Auditor
No implementation mutation by default.
Inputs:
- exact diff/head
- FIG/change surface
- test/evidence bundle
- specialist findings
Outcome:
- APPROVED / CORRECTION REQUIRED / BLOCKED
Dependency: all implementation tasks/evidence complete.

## Parallelism policy
Safe parallel candidates:
- T2 and T3 after T1;
- T5 can start from frozen contracts while T4 is implemented;
- T7 can run alongside T4/T5 because it owns adapter boundary files;
- T8 starts early and expands as interfaces stabilize.

Serialize when:
- package layout ownership overlaps;
- shared schema changes after frontend/backend implementation begins;
- migration changes alter API contract assumptions;
- same frontend files would be touched by T5 and T6.

## Scope-expansion rule
Any agent needing to write outside its assigned WRITE_SET must stop and return `SCOPE_EXPANSION_REQUIRED` with rationale and impacted acceptance criteria. TeamComposer may recompile ownership, but the Work Order scope may not silently expand.

## Model/assurance routing
- ordinary implementation tasks: BALANCED minimum;
- architecture/security/data/recovery decisions: STRONG;
- security-sensitive/recovery/audit disputes: HIGH_ASSURANCE according to frozen policy;
- deterministic validation remains preferred wherever possible.

## Completion rule
Parallel task completion is not overall completion. The slice completes only after integration head is fixed, required tests/evidence run against that exact head, ReviewScope closes, Senior Review issues a verdict and independent audit passes where policy requires.