# Cockpit Design Tokens & Component Contract

Status: PROPOSED FOR FREEZE — HP-PLAN-009

## Mission
Translate the frozen Obsidian Glass / Electric Signal direction into implementation-ready tokens, components, states and visual acceptance rules without coupling the product identity to a third-party component library.

## Token layers
1. **Foundation** — spacing, radius, typography, elevation, motion, breakpoints.
2. **Semantic state** — success, warning, danger, info, stale, degraded, unknown, blocked.
3. **Surface** — solid-core, glass-utility, floating-glass, holographic.
4. **Signal** — cyan/blue/violet activity spectrum.
5. **Density** — compact, standard, expanded.
6. **Graphics profile** — cinematic, balanced, efficient, reduced.

## Color semantics
Semantic colors are reserved for meaning. Decorative signal colors must not impersonate health state.

Required state tokens:
- `state.success`
- `state.warning`
- `state.danger`
- `state.info`
- `state.stale`
- `state.degraded`
- `state.unknown`
- `state.blocked`

Required neutral tokens:
- `surface.canvas`
- `surface.panel`
- `surface.panelRaised`
- `surface.overlay`
- `surface.code`
- `border.subtle`
- `border.active`
- `text.primary`
- `text.secondary`
- `text.muted`

Signal tokens:
- `signal.cyan`
- `signal.blue`
- `signal.violet`

## Typography
- UI sans family selected for readability at dense information scale.
- Monospace family reserved for code, SHAs, IDs, metrics and exact values.
- minimum contrast targets follow WCAG AA for ordinary text.
- numeric telemetry should use tabular numerals where available.

## Surface classes
### SOLID_CORE
Use for:
- code;
- diffs;
- evidence;
- security findings;
- dense tables;
- destructive confirmations.

### GLASS_UTILITY
Use for:
- navigation;
- compact cards;
- status chips;
- secondary rails.

### FLOATING_GLASS
Use for:
- overlays;
- command palette;
- transient detail panels.

### HOLOGRAPHIC
Use sparingly for:
- Hive Core overlays;
- agent/activity visualization;
- non-critical ambient signal layers.

## Component primitives
The first slice needs these project-owned components regardless of Base UI/Radix choice:
- `AppShell`
- `CommandHeader`
- `ProjectSwitcher`
- `NavigationRail`
- `EngineeringWorkspace`
- `ChatSurface`
- `StructuredArtifactCard`
- `LiveSystemRail`
- `TelemetryStrip`
- `StatusBadge`
- `HealthMatrix`
- `AgentActivityList`
- `ReviewStatusCard`
- `GitHubStatusCard`
- `CostContextCard`
- `EcosystemStatusCard`
- `HiveCorePanel`
- `VisualTruthMirror`
- `EmptyState`
- `DegradedState`
- `ErrorState`
- `SkeletonState`

## State completeness rule
Every component that fetches or projects runtime data MUST have explicit states for:
- loading;
- current;
- stale;
- degraded;
- unknown;
- not connected;
- not available;
- empty;
- error;
- blocked when semantically relevant.

No component may collapse UNKNOWN into healthy or empty.

## Motion contract
Motion is semantic and bounded.
Allowed causes:
- state transition;
- hierarchy change;
- causal flow;
- focus change;
- arrival/removal of actionable information.

Motion must reduce under `prefers-reduced-motion` and REDUCED graphics profile.
Decorative motion may be dropped entirely under ResourcePeacekeeper pressure.

## 3D/Hive Core visual contract
- 3D uses the same semantic status vocabulary as DOM UI.
- color cannot be the only status channel.
- node/edge state must map to accessible labels in VisualTruthMirror.
- no hidden interactions that exist only in canvas.
- cinematic effects never delay critical state updates.

## Acceptance states
At minimum, visual evidence must capture:
1. healthy standalone project;
2. HIVE/UADS/UGAS disconnected;
3. active review;
4. blocked Work Order;
5. degraded external dependency;
6. stale projection;
7. reconnect/reconciling;
8. reduced-motion/graphics mode;
9. 3D disabled.

## Freeze boundary
Freeze semantic tokens, surface classes, required component inventory, component-state completeness, motion semantics and VisualTruthMirror requirements. Exact font family, primitive library and numeric token values remain implementation benchmark/design review decisions.