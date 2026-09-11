# UI/UX — Hive Plan Command Cockpit

Status: V1 DESIGN DIRECTION

## Experience goal
A premium dark engineering cockpit that feels alive, information-rich, fast, and controlled without becoming visually noisy. The interface should communicate system state at a glance and make the active engineering workflow obvious.

## Visual language
- Dark-first.
- Glassmorphism used selectively for depth, not as decoration everywhere.
- Deep neutral background, luminous accent system, restrained bloom/glow.
- Fine grid/noise/technical textures at very low contrast.
- Animated data-flow/energy lines only where they communicate active relationships or state.
- Motion is purposeful, low-latency, and can be reduced/disabled.
- 3D assets are optional progressive enhancement; no critical control depends on WebGL/3D.

## Primary layout
```text
┌──────────────────────────────────────────────────────────────────┐
│ Hive Plan | Project | Environment | Health | Cost | Search      │
├──────────────┬────────────────────────────────┬──────────────────┤
│ PROJECTS     │ ENGINEERING CHAT / PLANNING   │ LIVE PROJECT     │
│              │                                │ BRAIN            │
│ Hive         │ discussion / diagrams          │ WO / PR / CP     │
│ UADS         │ agent council / decisions      │ risks / CI       │
│ UGAS         │ Work Order preview              │ agents / cost    │
│ Neryn        │                                │ evidence         │
├──────────────┴────────────────────────────────┴──────────────────┤
│ ACTIVITY / EVENT RAIL: GitHub · CI · Agents · Review · Tokens  │
└──────────────────────────────────────────────────────────────────┘
```

## Cockpit modules
- Project Fleet: health/progress/current increment for all managed projects.
- Engineering Chat: discussion, interviewer, planning council, diagrams, approvals.
- Project Brain: canonical sources, decisions, checkpoint, active context package.
- Work Orders: current/history/correction deltas/download/export.
- GitHub Control: repositories, PRs, issues, branches, releases, checks.
- Review Center: evidence, findings, severity, reviewer/auditor verdicts.
- Agent Operations: active role, task, queue, latency, escalations.
- Token & Cost Center: provider/model/project/agent/WO cost, cache hits, token flows.
- Reliability Center: errors, retries, dead-letter events, health, recovery.
- Security Center: token/provider status, policy violations, sensitive-context blocks.
- Architecture Studio: Mermaid/diagram rendering and visual system maps.

## Frontend-first development rule
Once implementation starts, an early vertical slice of the cockpit is prioritized so the operator can observe the system evolving. New backend capabilities SHOULD expose relevant cockpit state as they are implemented.

## Accessibility/performance
- Keyboard-first navigation for major actions.
- WCAG-conscious contrast despite glass effects.
- Reduced-motion mode.
- Progressive enhancement for GPU-heavy visuals.
- Virtualized long feeds and logs.
- Avoid continuous expensive animations while window is unfocused.

## Visual technology policy
3D/Blender/UGAS-generated assets may enhance identity, but visual fidelity cannot compromise responsiveness, observability clarity, or local hardware stability.
