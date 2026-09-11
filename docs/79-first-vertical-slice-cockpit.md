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
- Projects
- Engineering Chat
- Planning / Sources
- Agents
- Work Orders
- Reviews
- GitHub
- Memory / RAG
- Skills
- Costs
- Health / Diagnostics
- Settings

Navigation is data-driven and permission/capability-aware. Disabled/unavailable areas explain why rather than silently disappear.

### 3. Primary engineering workspace
Default mode is Engineering Chat + project context.

The chat surface supports structured cards for:
- decisions;
- ADRs;
- requirements;
- Work Orders;
- Review Receipts;
- findings;
- evidence;
- diagrams;
- GitHub PR/issue state;
- checkpoints;
- agent council summaries;
- blockers.

Critical state is never represented only as prose.

### 4. Hive Core
Optional central/adjacent data-driven 3D visualization.

Initial node families:
- Project;
- HIVE / Memory;
- UADS / Executor;
- UGAS where connected;
- GitHub;
- Work Order;
- Agents;
- Review;
- Evidence;
- Checkpoint.

Edges represent real current relationships/events, not decorative animation.

Rules:
- DOM/2D VisualTruth Mirror is authoritative and always available;
- WebGPU preferred when supported;
- WebGL2 fallback;
- no 3D dependency for navigation or critical understanding;
- RenderBudget Governor controls DPR, particles, post-processing and animation density;
- Frame-Time Circuit Breaker degrades graphics automatically;
- ResourcePeacekeeper yields GPU/CPU budget to local AI/UGAS/HIVE workloads.

### 5. Live system rail
Compact realtime surface for:
- agents active / queued / blocked;
- current Work Order;
- review state;
- CI/check state;
- GitHub events;
- current blockers;
- backend/API/database health;
- HIVE/UADS/UGAS connection health;
- recent errors/warnings.

Only actionable/meaningful transitions animate strongly.

### 6. Bottom telemetry strip
- idea-to-verified-merge timer where active;
- Work Order state;
- QualityFloor/model tier;
- tokens in/out/cached;
- current/estimated cost;
- RAG/cache hit indicators;
- active agents count;
- CPU/RAM/GPU pressure;
- event/review queue health.

## Data truth model
UI reads from explicit projection/view models generated from canonical backend state. Components MUST NOT reconstruct business truth independently from unrelated endpoints.

Projection families:
- ProjectCockpitProjection
- AgentActivityProjection
- DeliveryProjection
- ReviewProjection
- CostProjection
- HealthProjection
- EcosystemProjection

Every projection includes:
- projection_version;
- generated_at;
- source_watermark / revision;
- freshness state;
- degraded/stale reason where applicable.

## Realtime
V1 default: initial HTTP snapshot + SSE delta stream.

`CockpitProjectionStore` applies deltas atomically. `ProjectionFence` rejects deltas older than the active watermark. `PulseMux` coalesces high-frequency non-critical telemetry before React rendering.

Event classes:
- CRITICAL_STATE: never sampled/coalesced away.
- STATE_TRANSITION: ordered and durable enough for projection recovery.
- TELEMETRY_LATEST: latest-value coalescing allowed.
- TELEMETRY_SAMPLE: sampled/downsampled.
- DECORATIVE_SIGNAL: may be dropped entirely under pressure.

Disconnect behavior:
1. UI marks stream degraded.
2. retains last-known state with age.
3. reconnects with bounded backoff.
4. requests fresh snapshot before trusting missed deltas when watermark gap exists.
5. never fabricates green/healthy state during unknown connectivity.

## Frontend architecture
Recommended initial stack:
- React 19.3+;
- TypeScript strict;
- Vite 8.1+/Rolldown;
- TanStack Router;
- TanStack Query for request/server-state lifecycle;
- a thin project-owned projection store for realtime cockpit state;
- Base UI or Radix selected by benchmark;
- Tailwind CSS 4.x as token utility/build layer, not visual identity;
- Motion for meaningful UI transitions;
- React Three Fiber + Three.js WebGPURenderer for optional Hive Core;
- ECharts/uPlot split only if benchmark justifies two chart engines.

Do not add a general global state library unless the slice demonstrates a real unmet need.

## Visual system
Working visual language: Obsidian Glass / Electric Signal.

Principles:
- dark graphite/obsidian base;
- depth through layered surfaces, not excessive blur;
- restrained cyan/blue/violet system-energy spectrum;
- semantic colors reserved for state meaning;
- high-density information remains legible;
- code/diff/evidence surfaces favor clarity over glass effects;
- motion conveys state transition, causality or hierarchy;
- cinematic effects are progressively enhanced and degradable.

## Performance budgets
Budgets are benchmark targets to validate during implementation, not arbitrary guarantees.

Primary desktop target on representative local machine:
- interaction should remain responsive under simultaneous SSE updates;
- 3D must not block chat/navigation/input;
- main-thread long tasks are treated as defects when they materially affect interaction;
- no unbounded event-driven React rerender storms;
- memory growth under a long cockpit session is measured;
- graphics profile degradation occurs before UI usability degrades.

Benchmark profiles:
1. 3D disabled baseline.
2. REDUCED.
3. EFFICIENT.
4. BALANCED.
5. CINEMATIC.
6. local AI/GPU pressure simulation.
7. high-event-rate simulation.

Measure FPS/frame time, input latency, long tasks, heap, GPU pressure where observable, network event rate, React commits, dropped/coalesced telemetry and recovery behavior.

## Accessibility
- keyboard-first cockpit navigation;
- visible focus;
- semantic DOM even when 3D is active;
- reduced-motion compliance;
- no color-only status encoding;
- screen-reader labels for state and controls;
- zoom/high-density layout resilience;
- critical data available outside canvas.

## Backend slice
The vertical slice needs only the bounded backend surface necessary to prove the cockpit:
- health/version/capabilities;
- project summary;
- ecosystem connections summary;
- agent activity summary;
- delivery/review/GitHub summary;
- cost/context/cache summary;
- hardware/resource summary;
- SSE projection stream.

No fake metrics. Unsupported metrics return explicit NOT_AVAILABLE/NOT_CONNECTED states.

## Persistence slice
- PostgreSQL stores canonical project/runtime state required by the slice.
- projection state is derived/rebuildable.
- telemetry retention is bounded.
- large evidence/log payloads use content-addressed artifact storage.
- Redis is not required for correctness.

## Security slice
- localhost bind by default;
- secrets never emitted to projections/logs;
- CSP and secure browser headers;
- untrusted project/research content rendered as data, not executable markup;
- no unsafe HTML rendering paths;
- no arbitrary filesystem access from frontend;
- all mutations pass backend authority/policy checks.

## Test portfolio
- projection reducer/unit tests;
- stale/out-of-order delta tests;
- disconnect/reconnect tests;
- browser integration test for startup/navigation/chat shell;
- visual-state fixtures;
- accessibility automation plus targeted manual checks;
- graphics fallback tests;
- performance/event-storm benchmark;
- backend contract tests;
- Postgres restart/recovery test;
- no-fabricated-state negative tests.

## Evidence required
- exact Git head;
- build/type/lint/test results;
- browser screenshots/video for required visual states;
- accessibility report;
- performance benchmark report for graphics profiles;
- event-storm/reconnect evidence;
- backend/API contract evidence;
- restart/recovery proof;
- secret scan/security checks.

## Stop condition
The slice is accepted only when it is visually representative of the product direction, uses real backend/projection data, remains usable with 3D disabled/degraded, survives reconnect/restart scenarios, meets agreed performance/accessibility gates, and produces enough observability/evidence for Hive Plan to review itself.