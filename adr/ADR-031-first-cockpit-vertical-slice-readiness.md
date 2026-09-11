# ADR-031 — First Cockpit Vertical Slice Readiness Boundary

Status: ACCEPTED
Date: 2026-09-11
Increment: HP-PLAN-009

## Context
HP-PLAN-008 froze the V1 runtime, cockpit, realtime and persistence architecture. The next risk is implementation drift: allowing the first Codex/UADS execution to expand scope, invent data, overbuild infrastructure or couple 3D/UX to correctness.

## Decision
The first implementation slice is bounded by HP-WO-0001 and the following rules:
- frontend-first but end-to-end;
- one persisted project cockpit;
- truthful explicit freshness/availability states;
- snapshot + SSE watermark projections;
- PostgreSQL canonical first-slice state;
- optional Hive Core 3D with VisualTruthMirror and graceful fallback;
- read-only/no-mutation HIVE/UADS/UGAS seams in this slice;
- no mandatory Redis/microservices/full RAG/full agent runtime;
- accessibility, reconnect, restart/recovery, performance and security evidence are part of acceptance;
- UADS multi-agent execution is derived from one canonical Work Order and uses conflict-safe ownership.

HP-WO-0001 remains unauthorized until final Context Lock + CompileGuard against canonical main after this planning increment merges.

## Consequences
The first implementation proves the product shell and architectural seams without dragging future subsystems into the slice. The cost is deliberate incompleteness: many features render truthful disconnected/not-available states before later integrations are implemented.

## Guardrails
- no fake metrics or green demo states;
- no critical information may exist only in 3D;
- no external HIVE/UADS/UGAS mutations;
- no silent scope expansion;
- no acceptance without exact-head evidence;
- corrections stay in the same Work Order/PR when safe.