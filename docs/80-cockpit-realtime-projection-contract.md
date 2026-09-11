# Cockpit Realtime Projection Contract

Status: PROPOSED FOR FREEZE — HP-PLAN-008

## Goal
Keep the cockpit truthful, smooth and recoverable under changing GitHub, agent, review, cost, RAG and system-health state without turning every backend event into a React rerender.

## Projection authority
Canonical truth remains in governed backend state and external verified sources. Cockpit projections are derived read models only.

The UI MUST distinguish:
- CURRENT
- STALE
- DEGRADED
- UNKNOWN
- NOT_CONNECTED
- NOT_AVAILABLE

UNKNOWN is never rendered as healthy.

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

Never coalesce away:
- blockers;
- approvals/rejections;
- Work Order lifecycle changes;
- review verdicts;
- CI state transitions;
- security/recovery events;
- connection loss/recovery;
- canonical checkpoint changes.

May coalesce latest-value telemetry:
- CPU/GPU/RAM utilization;
- token counters;
- queue depths;
- transient progress percentages where source semantics permit;
- frame/graphics telemetry.

## Backpressure
If client rendering falls behind:
1. decorative signals drop first;
2. sampled telemetry frequency decreases;
3. latest-value telemetry collapses to most recent;
4. state transitions remain ordered;
5. critical events remain intact;
6. if ordering/watermark integrity cannot be guaranteed, force snapshot reconciliation.

## ProjectionFence
ProjectionFence prevents:
- old event overwriting newer state;
- one project applying another project's delta;
- stale execution epoch becoming current;
- old PR head/review result replacing current head;
- invalid ecosystem connection status being promoted from stale probes.

## Reconnect
Reconnect uses bounded exponential backoff with jitter. On reconnect, the server/client negotiate last known watermark if supported. If the gap cannot be proven complete, refresh the snapshot.

## UI rendering policy
React components subscribe to narrow projection slices. High-frequency telemetry should not cause unrelated panels to rerender. Canvas/3D consumes a throttled visualization projection separate from business-state projection.

## Persistence and recovery
Projection caches can be discarded. Backend projections must be rebuildable from canonical state plus durable workflow/event records needed for recovery.

Do not introduce event sourcing as a product-wide requirement merely to power the UI. Use append-only/durable events where workflow recovery/audit requires them, plus ordinary canonical relational state where simpler.

## Observability
Track:
- snapshot generation latency;
- delta rate by class;
- coalesced/dropped counts;
- reconnect count;
- watermark reconciliation count;
- client projection lag;
- React commit rate for key surfaces;
- SSE disconnect duration;
- stale/degraded exposure duration;
- projection build errors.

## Security
Projection payloads are allowlisted DTOs and must not expose provider secrets, raw environment values, tokens, private chain-of-thought, unrestricted filesystem paths or unredacted sensitive logs.

## Test gates
- deterministic reducer tests;
- out-of-order event rejection;
- duplicate/idempotency behavior;
- wrong-project/wrong-epoch rejection;
- event burst/backpressure;
- disconnect/reconnect;
- stale snapshot recovery;
- critical event preservation;
- no-secret projection fixture;
- 3D consumer throttling isolation.

## Freeze boundary
Freeze snapshot+delta/watermark semantics, explicit freshness states, PulseMux event classes/backpressure, ProjectionFence, reconnect reconciliation and separation between business projection and visualization projection. Exact internal state library and numeric coalescing intervals remain benchmark-driven.