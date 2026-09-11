# HP-PLAN-010 — Icon, Chart + Diagram Visual Language

Status: PROPOSED

## Icon system
Use one coherent engineering icon family through an adapter so the library can change without product-wide rewrites. Custom Hive Plan glyphs are reserved for product-specific concepts: Hive Core, Project Brain, Work Order, Context Lock, Evidence, Checkpoint, FailureShield, QualityFloor and ecosystem systems.

Rules:
- consistent optical weight;
- 16/20/24px primary sizes;
- filled/duotone only for selected/high-signal state;
- labels/tooltips for unfamiliar concepts;
- status always icon + text where consequential;
- no emoji as canonical UI iconography.

## Charts
Charts communicate measured data only. Every chart carries title, unit, source/freshness and accessible table/summary.

Visual families:
- line/area: time series;
- bar/stacked bar: comparison/composition;
- scatter: correlation/outliers;
- heatmap: coverage/latency/activity;
- bounded donut: simple composition only;
- timeline/Gantt-like: delivery/task spans;
- sparklines: compact telemetry;
- gauge: exceptional bounded semantics only.

Avoid 3D charts, perspective distortion and decorative gradients that impair reading.

## Diagram grammar
Mermaid is preferred deterministic/versionable diagram representation for sequence, flow, state, ER and architecture sketches. Interactive graphs use a separate validated graph spec.

Node shape communicates category; edge style communicates relation type; color is secondary. Every diagram has a textual summary and exportable source/spec.

## Graph language
Graph views share canonical primitives: entity node, cluster, typed edge, direction marker, state halo, authority ring, evidence badge, selection/focus and historical ghost.

## Evidence Heatmap
Heatmap uses both color and pattern/icon states. No red/green-only interpretation.

## Branding glyph
Hive Plan branding should avoid literal cartoon bee imagery. Preferred direction: abstract hexagonal/network/intelligence motif with a subtle `H/P` or hive topology signature, capable of becoming app icon, favicon and 3D Hive Core seed.

## Commercial readiness
The visual language must remain recognizable in screenshots, demos, landing pages and future plan tiers without introducing paywall-specific visual clutter into engineering truth surfaces.