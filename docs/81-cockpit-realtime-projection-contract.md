# Cockpit Realtime Projection Contract

Status: PROPOSED FOR FREEZE — HP-PLAN-008

## Goal
Keep the cockpit truthful, smooth and recoverable under changing GitHub, agent, review, cost, RAG and system-health state without turning every backend event into a React rerender.

## Projection authority
Canonical truth remains in governed backend state and external verified sources. Cockpit projections are derived read models only.

The UI MUST distinguish CURRENT, STALE, DEGRADED, UNKNOWN, NOT_CONNECTED and NOT_AVAILABLE. UNKNOWN is never rendered as healthy.

## Snapshot envelope
```json
{
  "projection": "ProjectCockpitProjection",
  "schema_version": "1.0",
  "project_id": "...",
  "watermark": "...",
  "generated_at": "RFC3339 UTC",
  "freshness": "CURRENT",
  "data": {}
}
```

## Delta envelope
```json
{
  "event_id": "...",
  "projection": "ProjectCockpitProjection",
  "base_watermark": "...",
  "next_watermark": "...",
  "event_class": "STATE_TRANSITION",
  "occurred_at": "RFC3339 UTC",
  "payload": {}
}
```

A delta whose base watermark does not match the active projection cannot be blindly applied. The client triggers reconciliation/fresh snapshot.

## PulseMux
PulseMux batches/coalesces safe high-frequency events before they reach presentation state.

Never coalesce away blockers, approvals/rejections, Work Order lifecycle changes, review verdicts, CI state transitions, security/recovery events, connection loss/recovery or canonical checkpoint changes.

May coalesce latest-value telemetry such as CPU/GPU/RAM utilization, token counters, queue depths, transient progress percentages where source semantics permit and frame/graphics telemetry.

## Backpressure
If client rendering falls behind:
1. decorative signals drop first;
2. sampled telemetry frequency decreases;
3. latest-value telemetry collapses to most recent;
4. state transitions remain ordered;
5. critical events remain intact;
6. if ordering/watermark integrity cannot be guaranteed, force snapshot reconciliation.

## ProjectionFence
ProjectionFence prevents old events overwriting newer state, cross-project deltas, stale execution epochs, old PR/review results and stale ecosystem probes becoming current truth.

## Reconnect
Reconnect uses bounded exponential backoff with jitter. On reconnect, negotiate last-known watermark where supported. If gap completeness cannot be proven, refresh snapshot.

## UI rendering policy
React components subscribe to narrow projection slices. High-frequency telemetry must not rerender unrelated panels. Canvas/3D consumes a throttled visualization projection separate from business-state projection.

## Persistence and recovery
Projection caches can be discarded. Backend projections must be rebuildable from canonical state plus durable workflow/event records required for recovery. Do not adopt event sourcing product-wide merely to power the UI.

## Observability
Track snapshot latency, delta rate by class, coalesced/dropped counts, reconnects, watermark reconciliations, client projection lag, React commit rate, SSE disconnect duration, stale/degraded exposure duration and projection build errors.

## Security
Projection DTOs are allowlisted and must not expose secrets, raw environment values, tokens, hidden chain-of-thought, unrestricted filesystem paths or unredacted sensitive logs.

## Test gates
Deterministic reducer tests, out-of-order rejection, duplicate/idempotency behavior, wrong-project/wrong-epoch rejection, event burst/backpressure, reconnect, stale snapshot recovery, critical-event preservation, no-secret fixture and 3D throttling isolation.

## Freeze boundary
Freeze snapshot/delta/watermark semantics, explicit freshness states, PulseMux event classes/backpressure, ProjectionFence, reconnect reconciliation and separation between business and visualization projections. Exact internal state library and numeric coalescing intervals remain benchmark-driven.