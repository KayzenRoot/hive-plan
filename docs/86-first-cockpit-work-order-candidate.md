# First Cockpit Work Order Candidate

Status: NOT AUTHORIZED — COMPILEGUARD/AUDIT REQUIRED
Increment: HP-PLAN-009
Candidate implementation ID: HP-WO-0001

## Objective
Implement the first end-to-end Hive Plan cockpit vertical slice on the frozen HP-PLAN-008 architecture so the operator can open one local project cockpit, see truthful current/degraded/disconnected state, navigate the engineering workspace, observe agents/review/GitHub/health/cost-context summaries, and use an optional adaptive Hive Core 3D visualization without terminal work.

## Scope
### Repository/bootstrap
- pnpm workspace with `apps/web`, `apps/api`, `apps/worker` and bounded shared packages.
- Node 24 LTS / strict TypeScript.
- Vite 8.1+ frontend.
- Fastify API.
- Docker Compose local-first bootstrap.
- PostgreSQL 18 service.

### Frontend
- AppShell, command header, navigation rail, engineering workspace, live system rail and telemetry strip.
- project cockpit route and project selector foundation.
- design token implementation from `docs/82a-cockpit-design-tokens-and-component-contract.md`.
- structured runtime states for CURRENT/STALE/DEGRADED/UNKNOWN/NOT_CONNECTED/NOT_AVAILABLE.
- Hive Core MVP with WebGPU/WebGL2/2D fallback and VisualTruthMirror.
- graphics profile control and reduced-motion behavior.

### Contracts/API
- shared versioned DTO/schema package from `docs/83-cockpit-contracts-and-api-surface.md`.
- system/project/cockpit/health/ecosystem/activity/cost-context endpoints.
- HTTP snapshot + SSE delta stream with watermark reconciliation.
- no-secret projection DTOs.

### Persistence
- minimum tables from `docs/84-first-slice-postgres-bootstrap.md`.
- reproducible first migration.
- restart persistence proof.
- no mandatory Redis.

### Ecosystem seams
- Hive Plan-side HIVE/UADS/UGAS adapter interfaces/stubs.
- truthful NOT_CONNECTED behavior by default.
- no mutation of external repositories/systems in this Work Order.

### Test/evidence
- unit/contract/integration/browser tests.
- accessibility checks.
- reconnect/out-of-order/event-storm tests.
- graphics fallback/profile benchmark.
- PostgreSQL restart/recovery test.
- secret scan/security headers checks.
- screenshots/video for required visual states.

## Deterministic bootstrap fixture
The implementation may create a clearly marked `LOCAL_DEVELOPMENT_FIXTURE` project only through a documented bootstrap/test command or migration fixture path. It must be persisted in PostgreSQL, carry `fixture=true`, and must not fabricate GitHub/HIVE/UADS/UGAS health, cost, token, review or CI success. Normal runtime startup must not silently seed it outside development/test profile.

## Explicit out of scope
- full engineering-chat LLM execution;
- full HIVE integration/RAG ingestion;
- UADS host dispatch execution;
- UGAS generation/production operations;
- complete agent orchestration runtime;
- cloud auth/multi-user support;
- Redis requirement;
- Kubernetes/microservices;
- full vector/RAG schema;
- complete cost/model router implementation;
- marketplace/plugins;
- unrelated refactors;
- replacing frozen stack choices.

## Required acceptance criteria
AC-01 Clean checkout can install/build/typecheck/test the bounded workspace using documented commands with zero unexplained failures.
AC-02 Docker Compose starts API, web and PostgreSQL locally with localhost-first exposure; PostgreSQL is not published externally unless explicitly required by the dev profile.
AC-03 Cockpit loads one persisted project from PostgreSQL. If the development fixture is used, it is visibly identified as `LOCAL_DEVELOPMENT_FIXTURE`; no health/cost/integration/review/CI data is fabricated.
AC-04 HIVE/UADS/UGAS disconnected states are explicit, distinguishable from UNKNOWN/DEGRADED, and all affected controls explain why unavailable.
AC-05 Snapshot + SSE deltas preserve watermark ordering, reject wrong-project/old-base deltas and force reconciliation on mismatch/gap.
AC-06 UNKNOWN/STALE/DEGRADED are never rendered as healthy/current; timeout/missing telemetry is never converted to zero-success.
AC-07 3D failure, browser lack of WebGPU/WebGL capability, REDUCED profile and explicit 3D disablement each preserve critical-state usability through VisualTruthMirror.
AC-08 Keyboard-only evidence covers: project switcher focus/open/select/close; navigation rail traversal; Engineering Workspace focus; Live System Rail actionable item traversal; graphics profile selector; and return to primary workspace. Visible focus and reduced-motion behavior are required.
AC-09 PostgreSQL process/container restart preserves project/runtime state required by the slice and cockpit recovers without reseeding or fabricated current state.
AC-10 no plaintext secrets appear in repository, projection DTOs, browser fixtures, structured logs or evidence artifacts; projection security fixture must demonstrate redaction/exclusion.
AC-11 Under the frozen event-storm fixture, p95 main-thread task duration attributable to cockpit projection/render processing must remain below 50 ms in 3D-disabled baseline, no single projection-induced long task may exceed 100 ms, and the UI must process operator navigation/input during the run without missed critical state transitions. At least one enabled graphics profile must complete the same semantic scenario with zero lost CRITICAL_STATE/STATE_TRANSITION events. Frame/FPS targets for enabled 3D remain benchmark evidence rather than release guarantee in this first slice.
AC-12 the nine required visual states from `docs/82a-cockpit-design-tokens-and-component-contract.md` have exact-head screenshot/video evidence with state source/freshness visible where relevant.
AC-13 HIVE/UADS/UGAS adapters in this Work Order are read-only stubs/interfaces: when unconfigured/unreachable they return explicit NOT_CONNECTED/DEGRADED/UNKNOWN according to contract, perform zero external mutation attempts, and never synthesize capability success.
AC-14 exact-head evidence bundle is generated after final implementation changes and contains base/head SHA, changed-file inventory and required proof references.
AC-15 Senior Review finds no unresolved HIGH/CRITICAL material defect and independent audit requirements are satisfied.

## Event-storm fixture
A deterministic test fixture MUST generate a documented bounded mixture of:
- CRITICAL_STATE events;
- STATE_TRANSITION events;
- TELEMETRY_LATEST updates;
- TELEMETRY_SAMPLE updates;
- DECORATIVE_SIGNAL events.

The fixture records produced/received/applied/coalesced/dropped counts by class. CRITICAL_STATE and STATE_TRANSITION produced count must equal applied semantic count after reconciliation, with duplicates handled idempotently rather than double-applied. Exact event rates/duration may be tuned during implementation benchmark but the fixture definition and results are versioned evidence.

## Evidence obligations
- exact base/head SHA;
- changed-file inventory;
- install/build/typecheck/test receipts;
- migration/fresh-install/restart receipts;
- browser screenshots/video by visual state;
- accessibility report including keyboard-only scenario;
- performance/event-storm report including long-task and event preservation evidence;
- SSE reconnect/watermark proof;
- graphics fallback proof;
- security headers + secret scan proof;
- API/schema contract report;
- ecosystem zero-mutation stub tests;
- evidence manifest bound to exact head.

## Agent execution plan
Use `docs/85-first-slice-agent-taskgraph.md`. UADS may parallelize only where TeamComposer and ownership checks prove conflict safety. Any write outside assigned WRITE_SET returns `SCOPE_EXPANSION_REQUIRED`.

## Correction policy
Corrections remain within HP-WO-0001 and the same PR when safe. Use Correction Delta for failed acceptance criteria/findings rather than recompiling unrelated context.

## STOP CONDITION
Stop execution and do not claim completion until all applicable AC-01..AC-15 have exact-head evidence, required CI/tests are complete, the visual evidence matrix exists, no stale Context Lock or scope expansion is unresolved, and the Completion Manifest can truthfully report COMPLETED. Otherwise report BLOCKED with the failing criterion and evidence gap.

## Authorization gate
This candidate MUST NOT be sent to Codex/UADS until:
1. HP-PLAN-009 planning artifacts pass objective audit;
2. CompileGuard confirms no ambiguity/contradiction/stale source/unverifiable criterion;
3. Context Lock is generated against the current canonical `main` SHA;
4. operator/plan policy promotes the Work Order to AUTHORIZED.