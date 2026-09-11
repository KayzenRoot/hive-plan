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
- design token implementation from docs/82.
- structured runtime states for CURRENT/STALE/DEGRADED/UNKNOWN/NOT_CONNECTED/NOT_AVAILABLE.
- Hive Core MVP with WebGPU/WebGL2/2D fallback and VisualTruthMirror.
- graphics profile control and reduced-motion behavior.

### Contracts/API
- shared versioned DTO/schema package from docs/83.
- system/project/cockpit/health/ecosystem/activity/cost-context endpoints.
- HTTP snapshot + SSE delta stream with watermark reconciliation.
- no-secret projection DTOs.

### Persistence
- minimum tables from docs/84.
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
AC-01 Clean checkout can install/build/typecheck/test the bounded workspace.
AC-02 Docker Compose starts API, web and PostgreSQL locally with localhost-first exposure.
AC-03 Cockpit loads one real persisted project and renders no fabricated health/cost/integration data.
AC-04 HIVE/UADS/UGAS disconnected states are explicit and visually usable.
AC-05 Snapshot + SSE deltas preserve watermark ordering and reconcile on mismatch/gap.
AC-06 UNKNOWN/STALE/DEGRADED are never rendered as healthy/current.
AC-07 3D failure/disablement preserves full critical-state usability through VisualTruthMirror.
AC-08 Reduced-motion and keyboard navigation work for required flows.
AC-09 PostgreSQL restart preserves required canonical slice state.
AC-10 no plaintext secrets appear in repository, projections, logs or browser fixtures.
AC-11 performance benchmark proves the cockpit remains interactive under event-storm simulation with 3D disabled and under at least one enabled graphics profile.
AC-12 required nine visual states have review evidence.
AC-13 external ecosystem adapters perform no mutation and fail closed/truthfully when unavailable.
AC-14 exact-head evidence bundle is generated before review.
AC-15 Senior Review finds no unresolved HIGH/CRITICAL material defect and independent audit requirements are satisfied.

## Evidence obligations
- exact base/head SHA;
- changed-file inventory;
- install/build/typecheck/test receipts;
- migration/fresh-install/restart receipts;
- browser screenshots/video by visual state;
- accessibility report;
- performance/event-storm report;
- SSE reconnect/watermark proof;
- graphics fallback proof;
- security headers + secret scan proof;
- API/schema contract report;
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