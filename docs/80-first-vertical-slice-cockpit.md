# First Vertical Slice — Cockpit Foundation

Status: PROPOSED FOR FREEZE — HP-PLAN-008

## Purpose
Build the first implementation slice as a real end-to-end control surface, not a mock dashboard. The slice must prove frontend architecture, realtime projection, backend/API boundaries, persistence, observability, adaptive 3D, accessibility, GitHub integration seams and evidence collection together.

## User outcome
On startup, the operator can open one project cockpit and immediately see truthful current state, interact with the engineering chat shell, inspect active agents/work, observe GitHub/review/CI health, inspect cost/context health, and understand system status without terminal work.

## Screen composition
### 1. Global command header
- Hive Plan identity and current project selector.
- Command/search palette entry.
- Global health indicator.
- active model/quality tier summary.
- token/cost session summary.
- notifications/blockers indicator.
- graphics profile control: CINEMATIC / BALANCED / EFFICIENT / REDUCED.

### 2. Left navigation rail
Projects; Engineering Chat; Planning/Sources; Agents; Work Orders; Reviews; GitHub; Memory/RAG; Skills; Costs; Health/Diagnostics; Settings.

Navigation is data-driven and capability-aware. Disabled/unavailable areas explain why rather than silently disappear.

### 3. Primary engineering workspace
Default mode is Engineering Chat + project context. Structured cards support decisions, ADRs, requirements, Work Orders, Review Receipts, findings, evidence, diagrams, PR/issue state, checkpoints, council summaries and blockers. Critical state is never represented only as prose.

### 4. Hive Core
Optional data-driven 3D visualization. Initial node families: Project, HIVE/Memory, UADS/Executor, UGAS where connected, GitHub, Work Order, Agents, Review, Evidence and Checkpoint. Edges represent real relationships/events, not decorative animation.

Rules:
- DOM/2D VisualTruth Mirror is authoritative and always available;
- WebGPU preferred when supported;
- WebGL2 fallback;
- no 3D dependency for navigation or critical understanding;
- RenderBudget Governor controls DPR, particles, post-processing and animation density;
- Frame-Time Circuit Breaker degrades graphics automatically;
- ResourcePeacekeeper yields GPU/CPU budget to local AI/UGAS/HIVE workloads.

### 5. Live system rail
Realtime surface for agents, Work Order, review, CI, GitHub, blockers, backend/database health, HIVE/UADS/UGAS connection state and recent errors/warnings. Only actionable/meaningful transitions animate strongly.

### 6. Bottom telemetry strip
Idea-to-verified-merge timer; Work Order; QualityFloor/model tier; tokens in/out/cached; current/estimated cost; RAG/cache hits; active agents; CPU/RAM/GPU pressure; event/review queue health.

## Data truth model
UI reads explicit projection/view models generated from canonical backend state. Components MUST NOT reconstruct business truth independently from unrelated endpoints.

Projection families:
- ProjectCockpitProjection
- AgentActivityProjection
- DeliveryProjection
- ReviewProjection
- CostProjection
- HealthProjection
- EcosystemProjection

Every projection includes version, generated_at, source watermark/revision, freshness and degraded/stale reason when applicable.

## Realtime
V1 default: initial HTTP snapshot + SSE delta stream. CockpitProjectionStore applies deltas atomically. ProjectionFence rejects older/mismatched watermarks. PulseMux coalesces high-frequency non-critical telemetry before React rendering.

Event classes: CRITICAL_STATE, STATE_TRANSITION, TELEMETRY_LATEST, TELEMETRY_SAMPLE, DECORATIVE_SIGNAL.

Disconnect behavior: mark degraded, retain last-known state with age, reconnect with bounded backoff, reconcile snapshot when watermark continuity is uncertain, never fabricate healthy state.

## Frontend architecture
Recommended initial stack:
- React 19.3+;
- TypeScript strict;
- Vite 8.1+/Rolldown;
- TanStack Router;
- TanStack Query;
- thin project-owned realtime projection store;
- Base UI or Radix after benchmark;
- Tailwind CSS 4.x as token/build layer;
- Motion for meaningful transitions;
- React Three Fiber + Three.js WebGPURenderer for Hive Core;
- ECharts/uPlot split only if benchmark justifies two engines.

Do not add a general global state library unless the slice proves a real unmet need.

## Visual system
Obsidian Glass / Electric Signal: dark graphite/obsidian, layered depth, restrained cyan/blue/violet energy spectrum, semantic state colors, high legibility, clear code/diff/evidence surfaces, motion only when it conveys state/causality/hierarchy, cinematic effects progressively enhanced and degradable.

## Performance benchmark profiles
1. 3D disabled baseline.
2. REDUCED.
3. EFFICIENT.
4. BALANCED.
5. CINEMATIC.
6. local AI/GPU pressure simulation.
7. high-event-rate simulation.

Measure FPS/frame time, input latency, long tasks, heap, observable GPU pressure, network event rate, React commits, dropped/coalesced telemetry and recovery behavior.

## Accessibility
Keyboard-first navigation; visible focus; semantic DOM with 3D active; reduced-motion compliance; no color-only status; screen-reader labels; zoom/high-density resilience; critical information outside canvas.

## Backend slice
Bounded API surface: health/version/capabilities, project summary, ecosystem connections, agent activity, delivery/review/GitHub, cost/context/cache, hardware/resource summary and SSE projection stream. Unsupported metrics return explicit NOT_AVAILABLE/NOT_CONNECTED.

## Persistence slice
PostgreSQL stores canonical state needed by the slice; projections are derived/rebuildable; telemetry retention bounded; large evidence/log payloads use content-addressed artifact storage; Redis not required for correctness.

## Security slice
localhost by default; no secrets in projections/logs; CSP/security headers; untrusted content rendered as data; no unsafe HTML; no arbitrary filesystem access from frontend; mutations pass backend authority/policy checks.

## Test portfolio
Projection reducer tests, stale/out-of-order delta tests, reconnect tests, browser startup/navigation/chat-shell integration, visual-state fixtures, accessibility checks, graphics fallback, event-storm/performance benchmark, backend contracts, PostgreSQL restart/recovery, no-fabricated-state negative tests.

## Evidence required
Exact Git head, build/type/lint/test results, screenshots/video for required visual states, accessibility report, graphics-profile benchmark, event-storm/reconnect evidence, backend contract evidence, restart/recovery proof and secret/security checks.

## Stop condition
Accepted only when visually representative, powered by real backend/projection data, usable with 3D disabled/degraded, resilient to reconnect/restart, within agreed performance/accessibility gates and observable enough for Hive Plan to review itself.