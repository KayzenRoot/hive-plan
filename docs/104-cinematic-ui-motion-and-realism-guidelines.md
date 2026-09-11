# HP-PLAN-010 — Cinematic UI Motion + Realism Guidelines

Status: PROPOSED

## Mission
Define a premium motion/visual language that feels tactile, modern and fluid without becoming visually noisy or obscuring engineering information.

## Design language
Obsidian Glass / Electric Signal evolves into a layered control-room aesthetic:
- graphite/obsidian base;
- frosted/smoked glass at navigation and ambient layers;
- solid surfaces for code, diffs and findings;
- cyan/violet energy for activity and intelligence;
- green/orange/red reserved for operational meaning;
- subtle depth, parallax and physically plausible highlights;
- realistic reflections only on focal surfaces.

## Motion grammar
Every animation must belong to one class:
- NAVIGATION: spatial continuity between workspaces;
- STATE_CHANGE: health/review/agent status transitions;
- CAUSAL_FLOW: visible data/event movement between system nodes;
- FOCUS: draw attention to selected/important object;
- FEEDBACK: acknowledge operator input;
- AMBIENT: low-cost, low-amplitude atmosphere.

If an animation has no semantic or emotional function, remove it.

## Fluidity
Prefer compositor-friendly transforms/opacity for UI motion. Heavy blur, filters, layout thrashing and frequent DOM measurement are budgeted and profiled. Shared-element transitions are used selectively.

## Realism
Use realism where it reinforces quality:
- physically coherent easing/inertia;
- PBR 3D materials;
- depth-aware light and shadow;
- responsive parallax;
- restrained reflections/refractions;
- material transitions that match state changes.

Avoid skeuomorphic clutter, fake gauges, gratuitous holograms and constant background motion.

## Voice visualizer
The voice orb/waveform may use layered glass, volumetric-like gradients and reactive energy, but motion maps to microphone/ASR/TTS state and audio envelope. Idle effects are subtle and cheap.

## Agent presence
Agents appear as lightweight visual presences, not cartoon avatars by default. Presence may use glyphs/nodes/energy signatures tied to role and activity. Optional richer avatars remain future/experimental.

## Transition examples
- opening a project: camera/depth transition into project cockpit;
- starting review: Review node activates and causal flow appears from GitHub/Evidence;
- agent activation: role chip/node materializes with bounded pulse;
- blocker: flow visibly stops, status changes to warning/error, no celebratory motion;
- completion: restrained convergence/checkpoint effect rather than confetti.

## Quality assurance
Visual regression baselines must cover key resolutions, reduced-motion, efficient profile, dark/high-contrast states, text scaling and 3D-disabled mode.

## STOP CONDITION
Freeze only when motion grammar, realism boundaries, performance constraints, accessibility and visual-regression evidence are explicit.