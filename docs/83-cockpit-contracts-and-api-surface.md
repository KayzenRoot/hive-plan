# Cockpit Contracts & API Surface

Status: PROPOSED FOR FREEZE — HP-PLAN-009

## Goal
Define the smallest backend and shared-contract surface required for the first truthful cockpit slice.

## Contract rule
All browser-visible runtime state crosses versioned DTOs validated at the API boundary. Frontend components consume projections, not raw persistence models or unrelated endpoint fragments.

## Required shared schemas
- `ProjectSummary`
- `CapabilitySummary`
- `EcosystemConnectionState`
- `AgentActivitySummary`
- `DeliverySummary`
- `ReviewSummary`
- `GitHubSummary`
- `CostContextSummary`
- `HardwareResourceSummary`
- `HealthSummary`
- `ProjectCockpitProjection`
- `CockpitDeltaEnvelope`

## Freshness vocabulary
Every external/derived summary uses one of:
- CURRENT
- STALE
- DEGRADED
- UNKNOWN
- NOT_CONNECTED
- NOT_AVAILABLE

Unknown or unavailable data must never be converted to zero or success.

## Initial REST surface
### `GET /api/v1/system`
Returns service version, build identity, schema compatibility, capabilities and runtime mode.

### `GET /api/v1/projects`
Returns bounded project summaries.

### `GET /api/v1/projects/{project_id}/cockpit`
Returns one complete `ProjectCockpitProjection` snapshot with watermark.

### `GET /api/v1/projects/{project_id}/health`
Returns multidimensional health/dependency summary.

### `GET /api/v1/projects/{project_id}/ecosystem`
Returns HIVE/UADS/UGAS/GitHub connection status with source fingerprints when known.

### `GET /api/v1/projects/{project_id}/activity`
Returns current agent/work-order/review/CI activity summaries.

### `GET /api/v1/projects/{project_id}/cost-context`
Returns only measured token/cost/cache/context values; unsupported metrics use NOT_AVAILABLE.

### `GET /api/v1/projects/{project_id}/events`
SSE stream of `CockpitDeltaEnvelope` events.

## SSE contract
Each event includes:
- `event_id`
- `project_id`
- `projection`
- `base_watermark`
- `next_watermark`
- `event_class`
- `occurred_at`
- `payload`

Client must reconcile if `base_watermark` differs from current watermark.

## Event classes
- CRITICAL_STATE
- STATE_TRANSITION
- TELEMETRY_LATEST
- TELEMETRY_SAMPLE
- DECORATIVE_SIGNAL

Only the last three may be coalesced/dropped according to PulseMux policy. CRITICAL_STATE and STATE_TRANSITION preserve semantic ordering.

## Ecosystem adapter envelope
Each integration returns:
```json
{
  "system": "HIVE|UADS|UGAS|GITHUB",
  "status": "CURRENT|STALE|DEGRADED|UNKNOWN|NOT_CONNECTED|NOT_AVAILABLE",
  "observed_at": "RFC3339 UTC",
  "source_revision": "optional opaque revision",
  "capabilities": [],
  "reason": "optional machine-safe reason"
}
```
No adapter may infer success solely from process existence.

## Security requirements
Projection DTOs must exclude:
- secrets/tokens;
- unrestricted filesystem paths;
- raw environment values;
- hidden reasoning/chain-of-thought;
- unredacted provider payloads;
- arbitrary HTML.

## Contract tests
- schema validation;
- unknown enum/version rejection where required;
- no-secret fixtures;
- stale/unknown propagation;
- wrong-project delta rejection;
- duplicate event idempotency;
- watermark mismatch reconciliation;
- disconnect/reconnect recovery.

## Freeze boundary
Freeze DTO families, endpoint responsibilities, freshness vocabulary, SSE envelope and security exclusions. Exact serialization library and internal handler implementation remain replaceable.