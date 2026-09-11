# Hive Plan Cockpit — Frontend Visual System

Status: PROPOSED FOR FREEZE — HP-PLAN-008

## Design mission
The cockpit must feel like a living engineering command center: dense but readable, visually distinctive, dark, premium, responsive and instrument-like. It should communicate system activity through motion and spatial hierarchy without turning essential information into decoration.

## Visual identity
Working visual language: **Obsidian Glass / Electric Signal**.

Base:
- near-black graphite/obsidian surfaces;
- layered translucent glass panels;
- restrained blur and depth;
- thin luminous borders;
- cyan/blue/violet as primary signal spectrum;
- amber/orange for warnings and elevated risk;
- green only for verified healthy/approved state;
- red only for failure/critical blockers.

Avoid permanently glowing every surface. Light must encode state, focus or flow.

## Main cockpit anatomy
```text
┌──────────────────────────────────────────────────────────┐
│ Global Health / project switcher / search / command bar │
├──────────────┬────────────────────────────┬───────────────┤
│ Projects     │ Main Workspace             │ Live Rail     │
│ agents       │ Chat / planning / review   │ agents        │
│ sources      │ + contextual 3D core       │ CI/review     │
│ releases     │ + dashboards               │ alerts        │
├──────────────┴────────────────────────────┴───────────────┤
│ Event timeline / token-cost / execution status / command │
└──────────────────────────────────────────────────────────┘
```

## The Hive Core 3D object
A central optional 3D visualization represents the current project/system state.

It MAY visualize:
- project nodes;
- active agents;
- dependencies;
- Work Order execution stages;
- RAG/context activity;
- review paths;
- GitHub/CI events;
- token/cost flow;
- failures/blockers.

Energy lines are data-driven, not random decoration. Example: an active Review Agent causes a visible pulse from PR node → EvidenceForge → Review Lead → audit node.

The 3D core is a secondary spatial visualization. Every critical datum also has an accessible DOM representation.

## Rendering stack
- React Three Fiber as React integration layer;
- Three.js `WebGPURenderer` when available;
- automatic WebGL2 fallback;
- glTF 2.0 for authored assets;
- Blender as the primary bespoke 3D asset authoring tool;
- KTX2/Basis textures where appropriate;
- meshopt/Draco candidate compression selected per asset benchmark;
- instancing for repeated particles/nodes;
- LOD and frustum culling;
- demand-driven rendering where scene is idle.

## Adaptive graphics modes
The cockpit MUST have a GraphicsGovernor with at least:
- CINEMATIC: highest fidelity, richer particles/post effects;
- BALANCED: default target;
- EFFICIENT: lower DPR, particles and post effects;
- ACCESSIBLE/REDUCED: minimal motion and optional 3D disable.

Automatic downgrade triggers may include:
- sustained low FPS;
- high frame time;
- hidden tab;
- thermal/power hints when available;
- user preference;
- simultaneous GPU-heavy local AI workload.

## Performance budgets
Initial planning targets, subject to benchmark:
- 60 FPS default on target desktop during normal cockpit interaction;
- never block chat/input while 3D updates;
- main-thread long task budget aggressively monitored;
- dynamic device-pixel-ratio cap;
- lazy-load heavyweight 3D routes/scenes;
- pause/slow animations for background panels;
- no uncontrolled React render loop for per-frame 3D state;
- virtualization for long timelines/logs/project lists.

## Motion language
Motion communicates causality:
- state changes use short spatial transitions;
- approval can collapse/lock a node;
- active work uses directional signal flow;
- warnings pulse slowly rather than flash;
- critical failures interrupt with clear static contrast plus limited motion;
- route transitions use React View Transitions/Motion where useful.

Motion library: Motion for React. Prefer compositor-friendly transforms/opacity, use layout animations deliberately, honor `prefers-reduced-motion`.

## Glassmorphism rules
Glass is a material system, not `backdrop-filter` sprayed everywhere.

Panel tiers:
1. SOLID CORE: high readability areas such as code/review text.
2. GLASS UTILITY: navigation/tool panels.
3. FLOATING GLASS: temporary overlays/popovers.
4. HOLOGRAPHIC: selective status/3D overlays.

Blur strength, transparency, borders and shadow depth are tokenized. Performance mode can reduce blur globally.

## Core screens
V1 visual planning should include:
- Command Center / Portfolio overview;
- Project cockpit;
- Engineering Chat;
- Planning Confidence map;
- Agent room / active team graph;
- Work Order execution graph;
- Auto Review workspace;
- Feature Impact Graph viewer;
- RAG/memory explorer;
- GitHub/CI timeline;
- Token/cost/latency analytics;
- Health/diagnostics center;
- Skills catalog;
- settings/providers/integrations.

## Project cards
Each project card should surface at-a-glance:
- stage;
- health;
- planning confidence;
- active Work Order;
- agents active;
- current PR/review status;
- token/cost trend;
- last checkpoint;
- blockers;
- release progress.

## Chat experience
Chat is a primary workspace, not a small support widget.

Requirements:
- wide readable conversation canvas;
- source/evidence chips;
- expandable agent council outputs;
- visual distinction between proposal, frozen decision, finding, blocker and evidence;
- inline diagrams/architecture visualization;
- downloadable Work Order/correction artifacts when relevant;
- side-by-side source/diff mode;
- command palette and keyboard navigation;
- streamed response with visible agent/tool state without exposing hidden reasoning.

## Data visualization
Use visual encodings intentionally:
- timeline for execution history;
- node graph for agent/dependency/impact relationships;
- sparklines for cost/latency;
- heatmaps for repository temperature/risk;
- Sankey-like flow only where flow volume genuinely matters;
- 3D only when spatial structure adds understanding.

ECharts is the primary rich-chart candidate. Dense time-series panels should benchmark uPlot/lightweight Canvas alternatives.

## Accessibility
- semantic DOM remains primary for critical controls;
- WCAG contrast targets;
- keyboard-first command center;
- focus rings never sacrificed for aesthetics;
- reduced motion;
- non-color status indicators;
- scalable typography;
- 3D scene can be disabled without losing functionality.

## Design implementation strategy
Build the design system before broad feature UI:
- tokens;
- surfaces;
- typography;
- iconography;
- panel primitives;
- status language;
- motion primitives;
- graph/3D primitives;
- command palette;
- telemetry cards.

Then construct the first vertical slice early: project selector + chat + live agent rail + one real telemetry panel + Hive Core placeholder/scene. This gives the operator a visible product very early while backend modules continue to grow.
