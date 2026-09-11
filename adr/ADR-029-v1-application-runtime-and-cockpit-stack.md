# ADR-029 — V1 Application Runtime and Cockpit Stack

Status: ACCEPTED  
Date: 2026-09-11  
Increment: HP-PLAN-008

## Context
Hive Plan requires a local-first realtime engineering cockpit with dense information, strong visual identity, optional data-driven 3D, excellent responsiveness and a maintainable backend. The stack must support rapid iteration without premature distributed-system complexity.

## Decision
Adopt the following V1 architecture boundaries:

### Frontend
- React 19.3+ with strict TypeScript.
- Vite 8.1+/Rolldown as the primary client build/dev pipeline.
- TanStack Router for application routing.
- TanStack Query for request/server-state lifecycle.
- a small project-owned CockpitProjectionStore for realtime projection state instead of a broad global-state framework by default.
- Tailwind CSS 4.x as utility/token build infrastructure, while visual identity remains project-owned.
- Motion for meaningful transitions/animation.
- React Three Fiber + Three.js WebGPURenderer for the optional data-driven Hive Core, with WebGL2 fallback and 2D/DOM VisualTruth Mirror.
- Base UI and Radix remain benchmark alternatives for primitive layer selection.
- chart engines remain benchmark-driven; avoid shipping two full chart stacks unless workloads justify it.

### Backend/runtime
- Node.js 24 LTS + strict TypeScript.
- Fastify-based HTTP/API runtime unless implementation benchmark reveals a blocker.
- modular monolith + bounded worker processes, not microservices by default.
- REST/HTTP commands and snapshots; SSE as default server-to-client realtime/event/LLM streaming path.
- WebSocket only for a demonstrated bidirectional/realtime need that SSE cannot satisfy cleanly.
- pnpm workspace/repository organization.
- Docker Compose local-first deployment.

### Realtime cockpit
- explicit projection/view models;
- snapshot + watermark-bound delta protocol;
- CockpitProjectionStore + PulseMux + ProjectionFence;
- high-frequency visualization projection separated from business-state projection;
- truthful freshness/degraded/unknown states;
- adaptive graphics through RenderBudget Governor, Frame-Time Circuit Breaker and ResourcePeacekeeper.

## Consequences
Positive:
- fast local development and frontend iteration;
- strong TypeScript end-to-end contract ergonomics;
- low operational complexity;
- 3D can be ambitious without becoming a correctness dependency;
- realtime state remains bounded and testable;
- easy future extraction of services if measured need emerges.

Costs/risks:
- WebGPU ecosystem remains more changeable than ordinary DOM UI;
- SSE needs explicit reconnect/watermark semantics;
- Node workers must avoid blocking event loop on heavy analysis;
- sophisticated cockpit can consume GPU/CPU if not governed.

Mitigations are mandatory through graphics profiles, worker isolation, benchmark gates, VisualTruth Mirror, backpressure and resource coordination.

## Rejected defaults
- Next.js as mandatory central application framework for V1 local cockpit;
- Electron/native desktop shell before browser-local deployment proves insufficient;
- WebSocket-everywhere;
- microservice decomposition at V1 start;
- 3D as the only representation of critical state;
- always-on cinematic rendering regardless of machine pressure.

## Replaceable/TRIAL boundaries
Primitive UI library, chart library, exact Three.js/WebGPU feature set, state-store implementation details and numeric performance budgets remain benchmark-driven.