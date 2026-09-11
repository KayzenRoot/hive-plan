# HP-PLAN-010 — Visual Bible: Motion, Materials + Lighting

Status: PROPOSED

## Motion system
Motion tokens are semantic rather than arbitrary durations.
- MICRO: hover/focus/press feedback;
- FAST: local state change;
- STANDARD: panel/card transition;
- FOCUS: graph/camera focus;
- CAUSAL: observed system flow;
- AMBIENT: optional low-frequency environmental motion.

Use physically plausible easing/springs. Repeated operational tasks must not wait for cinematic animation. Input remains responsive while transitions run.

## Motion semantics
NAVIGATION: spatial continuity.
STATE_CHANGE: explicit old -> new state.
CAUSAL_FLOW: observed event/dependency propagation.
FOCUS: guide attention.
FEEDBACK: acknowledge input.
AMBIENT: atmosphere only, first to degrade.

No perpetual motion in dense reading surfaces. Reduced motion removes nonessential movement and substitutes fades/static state.

## Materials
Primary material families:
- OBSIDIAN_GRAPHITE: matte/semi-matte structural base;
- SMOKED_GLASS: utility/nav overlays;
- CLEAR_SIGNAL_GLASS: rare focused controls/voice surfaces;
- ANODIZED_METAL: hero 3D structural objects;
- EMISSIVE_SIGNAL: bounded state/data energy;
- SOLID_EVIDENCE: opaque high-contrast technical surface.

PBR parameters are authored as reusable material presets. Avoid physically impossible combinations unless deliberately stylized and benchmarked.

## Lighting
Use environment/key/fill/rim hierarchy. Dynamic lights are scarce and meaningful. Emissive state can influence appearance without requiring expensive dynamic lighting everywhere.

Critical text/UI cannot depend on 3D illumination. Lighting exposure remains stable enough that operational colors preserve meaning.

## Effects
Candidate effects: restrained bloom, depth cues, selective reflection/refraction, soft volumetric-like gradients, particles and energy trails. Each effect has semantic purpose, quality tiers and measured GPU cost.

## VoiceOrb
Material stack can combine glass shell, internal emissive field and waveform/deformation. States are bound to real VoiceProvider events. Audio amplitude influences bounded deformation; random motion may exist only as subtle idle breathing in high graphics profiles.

## Event flow
Energy trails between Hive Core nodes appear only for real event windows and decay deterministically. They do not imply throughput values unless data actually maps to visual intensity.

## Performance contract
Every expensive material/effect defines CINEMATIC, QUALITY, BALANCED, EFFICIENT and SAFE_2D behavior. ResourcePeacekeeper can reduce effects without changing semantic state.

## STOP CONDITION
Motion/material/light presets require visual golden scenes, performance measurements and accessibility/reduced-motion alternatives before freeze.