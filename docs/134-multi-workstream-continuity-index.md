# HP-PLAN-010 — Multi-Workstream Continuity Index

Status: PROPOSED CORRECTION

## Purpose
Resolve checkpoint ambiguity when planning, implementation, review or recovery workstreams advance concurrently.

## Canonical layout
```text
checkpoints/
  index.json
  workstreams/
    <workstream-id>/latest.json
  history/
    <checkpoint-id>.json
```

`history/` remains immutable.
Each workstream gets its own latest pointer.
`index.json` is the project-level continuity directory, not a replacement for immutable checkpoints.

## Workstream identity
Examples:
- `planning/hp-plan-010`
- `implementation/hp-wo-0001`
- `review/hp-wo-0001`
- `release/v0.1.0`

A workstream record includes:
- workstream_id;
- type;
- project_id;
- repository;
- active/inactive/blocked/completed;
- latest_checkpoint_ref;
- issue/work_order/pr refs;
- source branch;
- source SHA;
- last_material_update;
- current objective;
- priority;
- parent/dependency workstreams;
- operator_focus_rank;
- digest.

## Resume resolution
For `continue do chat anterior`:
1. use explicit current project if present;
2. read `checkpoints/index.json`;
3. inspect active workstreams;
4. if exactly one has current operator focus, select it;
5. otherwise use deterministic last-material-focus metadata only when unambiguous;
6. if two or more workstreams are equally plausible and continuation could mutate state, show a compact choice rather than guessing;
7. verify selected workstream latest pointer and checkpoint;
8. reconcile against repository reality;
9. compile SessionResumeCapsule.

Read-only explanation may summarize multiple active workstreams without forcing a selection.

## Local convenience pointer
Runtime may persist local `last_open_project/workstream` UX state. It is advisory only and must match the Git-backed index before consequential continuation.

## Concurrent writes
Index and workstream pointer updates use expected prior digest/version. Conflict creates reconciliation; no last-writer-wins overwrite.

## Workstream lifecycle
OPEN -> ACTIVE -> BLOCKED/WAITING -> ACTIVE -> COMPLETED/ARCHIVED.
A completed stream remains addressable historically but cannot become implicit default continuation unless explicitly requested.

## Cross-workstream dependency
Planning can declare that merge/freeze is blocked by an implementation workstream. Dependency does not collapse their checkpoints into one timeline.

## Current project example
HP-PLAN-010 planning and HP-WO-0001 implementation remain distinct streams. Planning may continue on its branch without pretending HP-WO-0001 implementation state has advanced.

## STOP CONDITION
Freeze when ambiguous parallel continuation, concurrent checkpoint writes, archived streams, stale pointers and cross-workstream dependencies have deterministic tests.