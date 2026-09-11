# HP-WO-0001 - Codex Execution Prompt

## ROLE
You are the bounded implementation executor for Hive Plan Work Order `HP-WO-0001`.

You are NOT the product architect. Architecture, scope, contracts, acceptance criteria, evidence obligations and stop conditions are already decided. Your job is to verify repository reality, implement the authorized plan, run the required tests/evidence, and report truthful completion or a governed blocker.

Use the globally installed UADS/Hades orchestration runtime if available and useful for parallel execution, but only as an execution mechanism. Do not add UADS host dispatch as a Hive Plan product feature in this Work Order. All agent roles/task ownership must come from the canonical AgentTaskGraph, never from ad-hoc executor invention.

## SOURCE OF TRUTH
Read and obey, in this order:
1. `work-orders/HP-WO-0001/context-lock.json`
2. `work-orders/HP-WO-0001/work-order.json`
3. `work-orders/HP-WO-0001/implementation-blueprint.json`
4. `work-orders/HP-WO-0001/blueprint-compileguard-report.md`
5. locked canonical sources listed by the Context Lock, especially ADR-029, ADR-030, ADR-031 and docs 80-88.

Identifiers that must match:
- Work Order: `HP-WO-0001`
- Work Order digest: `sha256:11d9b016be0089ccd2b6bdbe8fcef376cdc7f3c09bcce7c11ea894837c5ccffd`
- Context Lock: `HP-WO-0001:context-lock:1`
- Context Lock digest: `sha256:8d393fb8bd0a9d7c2ad049e0d80b11801f0678c5b239b695b4b45affe0eae4dd`
- Context root: `sha256:f06d19db471f87c906e2251bf8605d9205e030c4d946cb266d800109ddae6575`
- Implementation Blueprint: `HP-BP-0001`
- Blueprint digest: `sha256:74baae6f4a3610970d66056eec7eb170782075ca54afb0cd98b2bd66a9a06982`
- Authorized branch: `feat/hp-wo-0001-cockpit-foundation`
- Authorized main/base observation: `88916137b4d07c8736320f052670a95df740c100`

If any identity, locked critical source fingerprint, branch or governing artifact is stale/inconsistent, STOP before implementation and report `BLOCKED_STALE_CONTEXT` with exact evidence.

## NON-NEGOTIABLE CONTRACT
Implement only the first end-to-end cockpit vertical slice.

Required architecture:
- React 19.3+ strict TypeScript.
- Vite 8.1+/Rolldown.
- TanStack Router + TanStack Query.
- Small project-owned `CockpitProjectionStore`.
- Node.js 24 LTS + strict TypeScript.
- Fastify API.
- Modular monolith + bounded workers, not microservices.
- REST snapshots/commands + SSE for server-to-client realtime.
- PostgreSQL 18 canonical durable state.
- Redis remains optional/non-canonical and should not be introduced unless an in-scope measured blocker requires it.
- Optional Hive Core through React Three Fiber/Three.js with WebGPU preferred, WebGL2 fallback and mandatory DOM/2D `VisualTruthMirror`.

Freshness states are exactly:
`CURRENT | STALE | DEGRADED | UNKNOWN | NOT_CONNECTED | NOT_AVAILABLE`

SSE event classes are exactly:
`CRITICAL_STATE | STATE_TRANSITION | TELEMETRY_LATEST | TELEMETRY_SAMPLE | DECORATIVE_SIGNAL`

`CRITICAL_STATE` and `STATE_TRANSITION` must never be sampled/coalesced away.

Never:
- fabricate health, costs, integrations, agents, review/CI success or metrics;
- convert missing/stale/unknown values into zero-success;
- mutate HIVE, UADS or UGAS;
- make 3D/canvas the only representation of critical state;
- introduce Kubernetes, microservices, mandatory Redis, separate vector DB or product-wide event sourcing;
- implement full Engineering Chat LLM, HIVE RAG, UADS product dispatch, UGAS production, public auth/multi-user/SaaS, billing or marketplace;
- change frozen contracts/acceptance criteria silently;
- reuse exact-head evidence after any implementation/config/test change.

## IMPLEMENTATION MAP
Execute in this dependency order.

### P0 - Preflight
- Confirm current branch is `feat/hp-wo-0001-cockpit-foundation`.
- Verify Work Order / Context Lock / Blueprint identities and digests.
- Verify all critical Context Lock source fingerprints remain fresh.
- Inspect repository reality before creating files.
- Confirm Node 24, pnpm, Docker and PostgreSQL-compatible local runtime prerequisites.
- If repo reality materially contradicts the Blueprint, do not redesign silently. Emit a governed deviation report.

### P1 - Repository/bootstrap foundation
Owner profile: A-015, support A-016.
Create the minimum bounded pnpm workspace and safe local runtime:
- root `package.json` scripts;
- `pnpm-workspace.yaml`;
- strict TypeScript config(s);
- `apps/web`, `apps/api`, bounded `apps/worker` only if needed by frozen architecture;
- shared package layout;
- Docker Compose for web/API/PostgreSQL;
- safe `.env.example` only, no secrets;
- localhost-first exposure;
- normal profile must not expose PostgreSQL externally.

Prove clean install/build skeleton and Compose config before continuing.

### P2 - Shared contracts first
Owner profile: A-011, support A-004.
Implement versioned shared DTO/schema package before backend/frontend drift begins.

Required DTO families:
- `ProjectSummary`
- `CapabilitySummary`
- `EcosystemConnectionState`
- `AgentActivitySummary`
- `DeliverySummary`
- `ReviewSummary`
- `GitHubSummary`
- `CostContextSummary`
- `HardwareResourceSummary`
- `HealthSummary`
- `ProjectCockpitProjection`
- `CockpitDeltaEnvelope`

Required rules:
- schema/version validation at API boundary;
- no secrets/tokens/raw env/unrestricted FS paths/hidden reasoning/unredacted provider payloads/arbitrary HTML;
- invalid major versions rejected rather than guessed;
- explicit freshness propagation;
- negative fixtures for UNKNOWN/STALE/DEGRADED/NOT_CONNECTED/NOT_AVAILABLE;
- no-secret sentinel fixture.

Freeze consumer-facing shapes after this phase unless a governed deviation is required.

### P3 - PostgreSQL canonical bootstrap
Owner profile: A-012, support A-023.
Select ONE bounded TypeScript PostgreSQL/query/migration stack using this criterion:
- PostgreSQL 18 support;
- reproducible migrations;
- parameterized queries;
- simple local Docker workflow;
- minimal abstraction/dependency overhead.
Record the choice and evidence. Do not add competing DB abstraction stacks.

Create only the minimum first-slice responsibilities:
- `projects`
- `project_runtime_state`
- `ecosystem_connections`
- `workflow_events`
- `agent_activity`
- `review_state`
- `cost_ledger`
- `artifact_refs`

Do NOT create full RAG/vector/UGAS/UADS/3D/timeseries schemas.

Development fixture policy:
- fixture allowed only in dev/test;
- must be visibly marked `LOCAL_DEVELOPMENT_FIXTURE` in persisted/projected/UI state;
- never silently seed healthy integrations or operational success.

Add fresh-install, migration and restart-persistence tests.

### P4 - Fastify cockpit API + realtime
Owner profile: A-010, support A-011/A-021.
Implement:
- `GET /api/v1/system`
- `GET /api/v1/projects`
- `GET /api/v1/projects/{project_id}/cockpit`
- `GET /api/v1/projects/{project_id}/health`
- `GET /api/v1/projects/{project_id}/ecosystem`
- `GET /api/v1/projects/{project_id}/activity`
- `GET /api/v1/projects/{project_id}/cost-context`
- `GET /api/v1/projects/{project_id}/events` as SSE.

Projection pipeline:
`PostgreSQL / verified adapter state -> services -> ProjectCockpitProjection -> snapshot/SSE -> client ProjectionFence -> CockpitProjectionStore`

SSE rules:
- each delta has event_id, project_id, projection, base_watermark, next_watermark, event_class, occurred_at, payload;
- apply only to matching project/current base watermark;
- duplicate event is idempotent;
- wrong project / stale base / unprovable gap is rejected;
- after unprovable gap, obtain fresh snapshot and continue from accepted watermark;
- bounded reconnect with jitter;
- count produced/received/applied/rejected/coalesced/dropped/reconciliation reasons.

Implement `PulseMux` so only TELEMETRY_LATEST, TELEMETRY_SAMPLE and DECORATIVE_SIGNAL can be safely reduced.

### P5 - Cockpit UI
Owner profile: A-013, support A-014.
Implement the frozen Obsidian Glass / Electric Signal cockpit shell, prioritizing semantic clarity before spectacle.

Core surfaces:
- AppShell
- CommandHeader
- ProjectSwitcher
- NavigationRail
- EngineeringWorkspace
- ChatSurface placeholder if required by shell only, but no LLM implementation
- LiveSystemRail
- TelemetryStrip
- Status/Health/Agent/Review/GitHub/Cost/Ecosystem cards necessary for the first slice
- explicit loading/empty/current/stale/degraded/unknown/not-connected/not-available/error states.

All UI runtime facts come from versioned projections or explicit deterministic local fixture state. No decorative fake operational data.

Keyboard-only required journey:
project switcher focus/open/select/close -> nav rail -> Engineering Workspace -> Live System Rail actionable item(s) -> graphics profile selector -> return to primary workspace.

Visible focus and reduced-motion behavior are required.

### P6 - Read-only HIVE/UADS/UGAS seams
Owner A-011; specialist review A-031/A-032/A-033.
Implement Hive Plan-side read-only interfaces/stubs only.

Unconfigured/unreachable adapters return explicit truthful envelopes such as NOT_CONNECTED/DEGRADED/UNKNOWN. Process existence alone is never CURRENT.

No mutating method should exist in the HP-WO-0001 external adapter surface. Add mutation spies/fakes proving zero write/deploy/install/auth-changing calls.

### P7 - Hive Core MVP + VisualTruthMirror
Owner A-013; support A-020/A-014.
Do this only after the semantic cockpit works without 3D.

Rules:
- 3D reads projection selectors only;
- never writes canonical/business state;
- WebGPU preferred when supported;
- WebGL2 fallback;
- REDUCED/disabled/SAFE_2D behavior;
- VisualTruthMirror always preserves critical semantic state;
- reduced-motion supported;
- resource pressure degrades decorative work before semantic work.

### P8 - Test, benchmark and evidence harness
Owner A-022; support A-020/A-017/A-021.
Required evidence includes:
- clean install/build/typecheck/test;
- DTO/schema invalid-state/no-secret tests;
- SSE order/duplicate/wrong-project/stale-base/gap/reconnect/reconciliation tests;
- PostgreSQL clean migration/fresh-install/restart persistence;
- browser integration and keyboard-only flow;
- reduced motion;
- nine visual states from docs/82a;
- WebGPU/WebGL2/REDUCED/3D-disabled semantic parity;
- HIVE/UADS/UGAS zero-mutation tests;
- secret scan/redaction/browser payload/security headers;
- exact-head evidence manifest.

Event-storm acceptance:
- 3D-disabled baseline p95 projection/render main-thread task < 50 ms;
- no projection-induced task > 100 ms;
- operator input/navigation remains usable;
- zero lost CRITICAL_STATE / STATE_TRANSITION events;
- record produced/received/applied/coalesced/dropped counts;
- at least one enabled graphics profile completes the semantic scenario with zero critical/state-transition loss.

Choose the event-storm rate/fixture size only within these criteria and record the chosen value/rationale.

### P9 - Stabilize exact head
Integrate all work. Fix only in-scope defects. Do not add opportunistic features/refactors.

After the final implementation/config/test change:
- rerun all required tests/evidence;
- regenerate visual/evidence artifacts;
- record exact base/head SHA and changed-file inventory;
- invalidate any evidence from prior heads.

### P10 - Completion handoff
Produce truthful Completion Manifest / implementation summary.
Do NOT self-approve.
Hand exact head + evidence to Senior Review Lead A-027 and independent Auditor A-028.

## DECISION BUDGET
### FROZEN - do not change
- stack and authority boundaries;
- PostgreSQL canonical persistence;
- REST snapshot + SSE architecture;
- freshness/event vocabularies;
- read-only external ecosystem policy;
- acceptance criteria AC-01..AC-15;
- no fake operational truth;
- critical-state DOM/2D parity.

### BOUNDED - choose once and record why
1. Base UI OR Radix primitives. Choose one based on accessibility, React compatibility and bundle/implementation fit. Do not ship both.
2. TypeScript PostgreSQL/query/migration library using the P3 criteria.
3. Exact deterministic event-storm rate/fixture size that reliably exercises backpressure on the target machine.
4. Exact fonts/token numbers within frozen visual language, while meeting accessibility/performance.

### OPEN_LOCAL
Internal helper/file/test names may differ from Blueprint predictions if contracts/scope/authority are unchanged. Prefer the smallest clear implementation and existing repository patterns.

### ESCALATE
STOP affected work if implementation requires changing:
- Work Order scope;
- any locked critical source contract;
- endpoint responsibility;
- freshness/event semantics;
- persistence authority;
- external mutation boundary;
- acceptance/performance threshold;
- branch/context identities.

Emit a `BLUEPRINT_DEVIATION` / `SCOPE_EXPANSION_REQUIRED` style report containing:
expected state, actual repo reality, concrete evidence, impact, proposed smallest correction and whether Context Lock/Work Order must be recompiled.

## FAILURE PREVENTION
Actively prevent these known failure classes:
- numeric documentation prefix collision;
- reachability falsely treated as health;
- missing telemetry rendered as 0/success;
- 3D becoming correctness dependency;
- executor completion claim treated as evidence;
- stale evidence reused after head change;
- fixture leakage into normal runtime;
- shared contract drift after dependent work starts;
- premature Redis/microservices/vector infrastructure;
- overlapping concurrent writes by multiple agents;
- secret/provider payload leakage into projections/logs/evidence.

## UADS/HADES EXECUTION POLICY
If UADS/Hades is available globally:
- load/use it as execution orchestration, not product scope;
- use only canonical agent roles and T1-T9 ownership from `docs/85-first-slice-agent-taskgraph.md`;
- parallelize only proven non-overlapping tasks;
- WRITE_SET conflicts serialize;
- shared schema changes after consumers start must serialize/reconcile;
- an agent needing a write outside its assigned set must stop with `SCOPE_EXPANSION_REQUIRED`;
- aggregate success exists only after one integrated exact head passes all evidence.

If UADS/Hades is unavailable or incompatible, execute serially/with bounded local concurrency without changing the Work Order.

## OUTPUT CONTRACT
During execution keep output concise. Do not narrate speculative architecture reasoning already settled by the Blueprint.

At the end return:
1. `STATUS: COMPLETED | BLOCKED`
2. final branch + exact head SHA
3. Work Order / Context Lock / Blueprint digests used
4. implementation summary grouped by P1-P10
5. changed-file inventory
6. bounded choices made + rationale
7. test/evidence command matrix and result
8. AC-01..AC-15 status table
9. evidence artifact/index paths
10. any Blueprint Deviations, scope expansion requests or unresolved risks
11. Completion Manifest path/status
12. explicit statement that Senior Review/Audit remain independent and were not self-approved.

## STOP CONDITION
Do not claim `COMPLETED` until all applicable AC-01..AC-15 have exact-head evidence, required CI/tests and the visual evidence matrix are complete, Context Lock is fresh, no unresolved material Blueprint Deviation/scope expansion exists, and the Completion Manifest can truthfully report COMPLETED.

If any requirement cannot be proven, return `BLOCKED` with the exact failed criterion and evidence gap. Do not lower the bar to finish.