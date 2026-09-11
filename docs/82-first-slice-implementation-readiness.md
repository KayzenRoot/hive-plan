# HP-PLAN-009 — First Cockpit Slice Implementation Readiness

Status: PLANNING ACTIVE

## Objective
Turn the frozen cockpit architecture into one implementation-ready bounded slice with enough repository, contract, visual, test and evidence detail that Codex/UADS can execute without rediscovering architecture or widening scope.

## Initial repository shape
```text
apps/
  web/
  api/
  worker/
packages/
  contracts/
  ui/
  telemetry/
  config/
  test-fixtures/
infra/
  docker/
  db/
```

This is a planning target, not implementation authorization.

## First-slice bounded modules
### Web
- app shell + routing;
- project cockpit route;
- Engineering Chat shell;
- Live System rail;
- bottom telemetry strip;
- Hive Core viewport + 2D VisualTruth Mirror;
- projection consumers;
- graphics profile controls;
- diagnostics/degraded-state surfaces.

### API
- `/health` and `/capabilities`;
- project cockpit snapshot;
- ecosystem status snapshot;
- agent/delivery/review/cost/health projection endpoints;
- SSE projection stream;
- no broad mutation surface beyond what first slice strictly needs.

### Worker
Initially minimal. Heavy/realtime background work is represented by bounded interfaces and test fixtures. Do not introduce a queue/runtime dependency merely to make the repository look complete.

### Contracts
Versioned schemas/types for:
- cockpit snapshot;
- realtime delta;
- freshness state;
- ecosystem connection state;
- health state;
- agent activity summary;
- delivery/review summary;
- cost/context summary;
- graphics/resource pressure summary.

## Standalone-first rule
The slice MUST start and remain useful with HIVE, UADS and UGAS disconnected.

Disconnected state is first-class:
- NOT_CONNECTED with reason and last probe time;
- no fake agents/jobs/assets;
- integration cards remain discoverable and explain connection requirements.

## Hive Core MVP
The first Hive Core is intentionally small:
- project root node;
- GitHub node;
- HIVE node;
- UADS node;
- UGAS node;
- Agents node;
- Review node;
- Evidence/Checkpoint node.

Only real connection/health/activity data drives visual state. No decorative fake traffic.

### Required parallel 2D view
The same topology/state is rendered as semantic DOM cards/list/graph summary. Critical information must be fully usable with canvas disabled.

## Visual acceptance states
At minimum capture and review:
1. healthy standalone project;
2. all ecosystem integrations disconnected;
3. one degraded dependency;
4. active review;
5. blocked Work Order;
6. reconnect/reconciling state;
7. REDUCED graphics mode;
8. WebGPU unavailable/WebGL2 fallback;
9. 3D disabled with full semantic parity.

## Scope lock
Codex/UADS MUST NOT:
- add unrelated product modules;
- implement full agent orchestration;
- implement full RAG/HIVE integration;
- implement UGAS generation;
- build a generic plugin marketplace;
- add Kubernetes/microservices;
- require Redis;
- add authentication intended for future multi-user cloud unless a local access safety requirement is explicitly approved;
- replace the frozen stack without an ADR/correction.

## Implementation package to complete in HP-PLAN-009
- repository/bootstrap map;
- package boundaries;
- contract schemas;
- first PostgreSQL migration boundary;
- UI component map;
- design-token seed;
- exact API/SSE surfaces;
- test matrix;
- performance/accessibility budgets;
- evidence bundle template;
- Context Lock source set;
- Work Order IR;
- AgentTaskGraph recommendation;
- CompileGuard checklist;
- STOP CONDITION.

## Stop condition
HP-PLAN-009 completes only when one bounded Work Order can be compiled from frozen sources with no unresolved architectural decision required to begin the first cockpit slice.