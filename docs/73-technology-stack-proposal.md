# HP-PLAN-008 — Technology Stack Proposal

Status: PROPOSED FOR FREEZE

## Objective
Choose a local-first implementation stack that maximizes development speed, runtime performance, reliability, visual quality, replaceability and long-term maintainability without premature microservice complexity.

## Architecture shape
V1 SHOULD be a modular monolith plus worker processes, all in one monorepo and deployed with Docker Compose.

```text
Browser Cockpit
  ↓ HTTP/SSE
API / Orchestrator
  ├─ planning domains
  ├─ review domains
  ├─ GitHub integration
  ├─ model routing
  ├─ RAG/context
  └─ event orchestration
       ↓
PostgreSQL + pgvector
       ↓
Durable workers / local artifact store
```

Independent process boundaries MAY exist for workers or GPU/local-AI adapters, but canonical domain contracts must remain process-neutral.

## Frontend primary stack
- React 19.3+
- TypeScript strict mode
- Vite 8.1+ / Rolldown
- TanStack Router for type-safe file routing
- TanStack Query for server-state caching/invalidation
- Base UI primitives for accessible low-level components
- Tailwind CSS 4.3+ for tokens/utilities, with a custom Hive Plan design system rather than stock component aesthetics
- Motion 13+ for micro-interactions, layout/view transitions and gesture animation
- Three.js WebGPURenderer + React Three Fiber for 3D/WebGPU with WebGL2 fallback
- Zustand or equivalent tiny store only for ephemeral local UI state
- Apache ECharts candidate for rich dashboard charts; benchmark against uPlot for dense time-series panels

## Why Vite rather than Next.js for V1
Hive Plan is a local application with a dedicated backend and does not need public SEO/SSR as a core requirement. Vite keeps the client boundary simple, reduces framework-specific server coupling, provides very fast development/build behavior and is a natural host for WebGPU/Three.js-heavy cockpit UI.

Next.js remains WATCH/TRIAL for future hosted/multi-user editions. It is not rejected as a technology; it is simply not the default architectural center of local V1.

## Backend primary stack
- Node.js 24 LTS for production runtime stability
- TypeScript strict mode
- Fastify for low-overhead HTTP API
- AJV / JSON Schema Draft 2020-12 validation aligned with Hive Plan artifact contracts
- SSE as default server-to-client live event/token stream
- WebSocket adapter only for flows that prove a bidirectional low-latency requirement
- OpenTelemetry instrumentation at service boundaries

Node 26 MAY be used in development trials, but V1 baseline SHOULD remain current LTS until compatibility/evals justify promotion.

## Monorepo
Recommended:
```text
apps/
  cockpit-web/
  api/
  worker/
packages/
  contracts/
  design-system/
  agent-runtime/
  context-engine/
  github-adapter/
  telemetry/
  test-kit/
```

Use pnpm workspaces initially. Add Turborepo/Nx only if benchmark evidence shows meaningful CI/dev gains beyond Vite/pnpm caching.

## Realtime strategy
Default path:
- REST/HTTP for commands and queries
- SSE for agent/review/project timelines and streamed LLM output
- resumable event cursor IDs
- client reconnect/backoff
- server-side event journal as authority

This keeps transport complexity lower than an always-on WebSocket architecture while preserving a realtime-feeling cockpit.

## Testing baseline
- Vitest for unit/component logic
- Testing Library for accessible UI behavior
- Playwright for E2E, visual regression and critical cockpit flows
- contract tests for JSON Schema artifacts
- integration tests against disposable PostgreSQL
- performance budgets for first render, interaction latency, animation FPS and event delivery

## Adoption classification
ADOPT candidate:
- React 19.3
- Vite 8.1/Rolldown
- TypeScript
- Node 24 LTS
- Fastify
- PostgreSQL 18
- JSON Schema/AJV
- TanStack Router/Query

TRIAL before freeze:
- Base UI vs Radix primitives
- ECharts vs uPlot by panel class
- pg-boss vs minimal in-house durable orchestration/outbox
- Redis presence in standalone V1
- WebGPU renderer performance profiles on target hardware

WATCH:
- Next.js 16.x for hosted/multi-user edition
- Node 26 for later LTS migration
- dedicated vector database for future scale

## Anti-complexity rules
- no mandatory Kubernetes in V1;
- no service mesh;
- no microservice split without measured deployment/ownership need;
- no second canonical datastore for convenience;
- no frontend dependency that owns the product visual identity;
- no 3D effect may be required to read critical system state.
