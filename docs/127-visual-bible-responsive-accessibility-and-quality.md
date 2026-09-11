# HP-PLAN-010 — Visual Bible: Responsive, Accessibility + Quality Gates

Status: PROPOSED

## Responsive priority
V1 is desktop-first, not desktop-only. Layout adaptation preserves operational priority rather than shrinking everything uniformly.

Priority order under constrained space:
1. active objective/blocker/critical state;
2. Engineering Chat/composer/voice transcript;
3. code/diff/findings/evidence;
4. navigation/context;
5. telemetry;
6. spatial/ambient decoration.

Heavy graphs/3D may move to dedicated full-screen views on narrow layouts.

## Accessibility
Target WCAG 2.2 AA-equivalent product behavior where applicable. Requirements include keyboard navigation, visible focus, semantic landmarks, labels, text alternatives, reduced motion, zoom/text scaling, screen-reader status announcements, captions/transcripts and non-color state encoding.

## Voice accessibility
Voice never replaces text. Transcript is always inspectable. Permission/listening/speaking states are announced and visible. Barge-in/cancel has keyboard/pointer equivalents.

## 3D accessibility
Every critical 3D view has VisualTruthMirror. Camera interaction is optional. No required task depends on spatial perception.

## Quality gates
Visual implementation must pass:
- contrast/readability;
- keyboard journey;
- reduced motion;
- 100/125/150/200% scaling scenarios;
- graphics profile transitions;
- WebGPU/WebGL2/SAFE_2D fallback;
- no semantic state loss;
- representative GPU/resource pressure;
- visual regression golden scenes;
- long-session usability for Chat/Review.

## Golden scenes
At minimum: healthy cockpit, disconnected ecosystem, active review, blocked WO, stale Project Brain, voice listening/transcribing/speaking, review critical finding, GitHub CI failure, RAG degraded, resource pressure auto-degrade, historical mode, SAFE_2D.

## Performance
Measure p50/p95 frame time where applicable, long tasks, input responsiveness, memory trend, draw calls/triangles/texture budget for 3D scenes and heavy-block render latency. Decorative fidelity is reduced before interaction quality.

## Visual acceptance
A screenshot alone is insufficient. Evidence includes interaction recording/automated traces, state fixtures, accessibility output, performance metrics and deterministic golden comparison.

## STOP CONDITION
Visual Bible is implementation-ready only when foundations, components, motion/materials, responsive/accessibility and golden-scene/evidence requirements are mutually consistent.