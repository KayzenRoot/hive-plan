# HP-PLAN-010 — Project Cockpit Detailed Layout

Status: PROPOSED

## Mission
Make the cockpit answer status, risk and next action in seconds while retaining a premium spatial identity.

## Desktop composition
Use a 12-column adaptive grid inside the global frame.
- Header: 64–72 px target band.
- Navigation rail: compact 72–88 px collapsed, expandable.
- Main hero zone: ~7/12 columns.
- Operational rail: ~5/12 columns.
- Bottom telemetry: compact persistent strip.
Exact pixels remain implementation-token decisions and must pass density/usability tests.

## Hero zone — Hive Core
The Hive Core occupies the dominant visual field without covering operational truth. Initial node set: Project, GitHub, HIVE, UADS, UGAS, Agents, Review, Evidence/Checkpoint.

Camera behavior:
- calm three-quarter default view;
- no constant orbit;
- gentle focus transition when selecting a node;
- user pan/zoom bounded;
- `Reset View` always available;
- reduced-motion uses near-instant transitions.

Real state visualization:
- connection lines pulse only for actual recent event flow;
- active review creates bounded flow GitHub -> Review -> Evidence;
- blocker marks the responsible node/path;
- disconnected ecosystem node remains present but dormant and labeled;
- stale state visually differs from unavailable state.

## Operational rail
Stacked glass/solid hybrid cards:
1. Current Objective / active increment;
2. Work Order status;
3. Review/CI state;
4. Blockers & incidents;
5. Ecosystem status;
6. Recent decision/checkpoint.
Cards can expand into their dedicated screens.

## Metric shelf
Below or adjacent to hero depending viewport:
- idea-to-verified-merge;
- current WO elapsed time;
- QualityFloor/model route;
- token/cache/cost;
- review findings by severity;
- RAG/cache health.
Only metrics with valid source/freshness render as numbers.

## Ambient behavior
Subtle depth, particles and volumetric-like cues are allowed in CINEMATIC/QUALITY. They reduce before semantic content when resource pressure rises.

## Primary interactions
- click/voice node -> focus + contextual summary;
- double action/open -> dedicated screen;
- `o que está bloqueando?` -> highlight blocker path;
- `o que mudou desde ontem/checkpoint?` -> delta overlay;
- `mostre atividade dos agentes` -> agent overlay;
- `modo foco` -> hide secondary telemetry.

## Empty/degraded
Standalone with all integrations disconnected remains visually complete and useful. No fake activity. Empty active-WO state offers planning/navigation, not simulated work.

## Acceptance direction
A new operator should identify project state, active work, blockers and system connectivity within a short usability task without interacting with the 3D graph.