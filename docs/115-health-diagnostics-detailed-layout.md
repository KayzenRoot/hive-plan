# HP-PLAN-010 — Health / Diagnostics Detailed Layout

Status: PROPOSED

## Mission
Provide operational truth and a fast path from symptom to cause, evidence and recovery.

## Primary zones
- dependency topology;
- multidimensional health matrix;
- active incidents;
- traces/logs/events workbench;
- queues/workers/adapters;
- circuit breakers/retries;
- storage/backup/RestoreProof;
- Incident Capsule / FailureShield promotion.

## Health dimensions
Availability, freshness, latency, integrity, authority, dependency health and degraded capability are separate. UNKNOWN is never green.

## Topology
Nodes represent real services/adapters/stores: web/API/workers/PostgreSQL/artifact store/GitHub/model providers/HIVE/UADS/UGAS. Edges expose dependency and recent failures. 3D topology is optional; semantic matrix is authoritative UI fallback.

## Incident workflow
Symptom -> correlated causal IDs -> affected dependency -> recent transition/config/source change -> evidence -> recovery action -> validation -> Incident Capsule -> verified failure memory candidate.

## Diagnostics workbench
Filter by project/WO/trace/agent/Git SHA/provider/event/effect. Logs are redacted and bounded; large raw logs remain referenced artifacts.

## Recovery
Retry only eligible transient classes. Authentication, validation, stale context, conflicts and integrity errors require appropriate non-retry handling. RestoreProof gates READY after recovery where applicable.

## Voice
`por que está degradado?`, `mostre o trace deste Work Order`, `qual serviço caiu primeiro?`, `o backup foi validado?`.