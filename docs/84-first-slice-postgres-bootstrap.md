# First Slice PostgreSQL Bootstrap

Status: PROPOSED FOR FREEZE — HP-PLAN-009

## Goal
Define the minimum canonical schema required for the first cockpit slice while avoiding premature domain modeling.

## Authority rule
PostgreSQL stores only canonical state required by the slice. High-frequency telemetry, 3D presentation state and browser projection caches are not canonical tables by default.

## Minimum tables
### `projects`
Purpose: registered Hive Plan projects.
Fields conceptually include:
- `id`
- `slug`
- `name`
- `repository_owner`
- `repository_name`
- `repository_default_branch`
- `created_at`
- `updated_at`

### `project_runtime_state`
Purpose: current canonical runtime/cockpit state that must survive restart.
Includes:
- `project_id`
- `state_revision`
- `active_increment_id`
- `active_work_order_id`
- `current_checkpoint_id`
- `updated_at`

### `ecosystem_connections`
Purpose: persisted configuration/last verified state metadata for HIVE/UADS/UGAS/GitHub.
Includes:
- `project_id`
- `system`
- `configured`
- `last_verified_status`
- `source_revision`
- `last_verified_at`
- `last_error_class`
No secrets are stored in this table.

### `workflow_events`
Purpose: bounded durable event/recovery journal for important state transitions used by cockpit reconciliation and workflow recovery.
Includes:
- monotonic/ordered event identity;
- project ID;
- event class/type;
- occurred_at;
- state revision/watermark;
- compact validated payload/reference.
Not a full event-sourcing mandate.

### `agent_activity`
Purpose: current bounded activity state for canonical/declared agents.
Includes:
- project ID;
- agent ID;
- task/work-order association;
- lifecycle state;
- started/updated/completed timestamps;
- evidence/status reference where relevant.

### `review_state`
Purpose: current review snapshot identity and lifecycle.
Includes:
- project ID;
- work order/increment;
- base SHA/head SHA;
- context root;
- evidence root;
- lifecycle/verdict;
- started/completed timestamps.

### `cost_ledger`
Purpose: measured provider/model/token/cost records for the first slice.
No fabricated estimates are inserted as actual cost. Estimated values, if later supported, require explicit kind.

### `artifact_refs`
Purpose: references to large immutable artifacts stored outside relational rows.
Includes:
- digest;
- project ownership;
- artifact kind;
- size;
- sensitivity;
- provenance;
- relative CAS locator/reference;
- created_at.

## Derived/not-yet-required
Do NOT create V1-first-slice canonical tables for:
- full RAG corpus;
- embedding vectors;
- complete AgentTaskGraph history;
- UGAS production graph;
- HIVE internal memory schema;
- UADS internal sidecar state;
- full telemetry timeseries;
- 3D scene state.
Those belong to later slices or external-system adapters.

## Integrity rules
- foreign keys for project-owned records;
- unique constraints on stable identities;
- explicit enums/check constraints where practical;
- timestamps in UTC;
- no plaintext secrets;
- review identity fields must not be nullable once review is active;
- external-system status records carry freshness timestamps.

## Migration policy
First migration creates only the minimum tables/indexes needed by the first vertical slice.
Migration must be:
- reproducible from empty database;
- idempotency-safe through migration tooling;
- covered by upgrade test;
- covered by fresh-install test;
- followed by restart/recovery test.

Exact TypeScript migration/query library remains benchmark-driven under ADR-030.

## Seed policy
Development fixtures may create one clearly-marked local sample project only in test/dev profiles. Production/runtime startup must not silently seed fake projects or healthy integrations.

## Backup boundary
Even in the first slice, schema version and artifact-store epoch/reference metadata must be included in backup/restore evidence.

## Freeze boundary
Freeze table responsibilities, authority boundaries and minimum integrity rules. Exact column types/indexes/library syntax are implementation details selected in the Work Order after library benchmark.