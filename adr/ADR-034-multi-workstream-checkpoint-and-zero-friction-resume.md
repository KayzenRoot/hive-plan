# ADR-034 — Multi-Workstream Checkpoint and Zero-Friction Resume

Status: ACCEPTED  
Date: 2026-09-11  
Increment: HP-PLAN-010

## Context
Planning, implementation and review may progress in parallel. A single mutable `latest` checkpoint is ambiguous and can resume the wrong workstream.

## Decision
Adopt a project continuity index plus immutable workstream checkpoints:
- `checkpoints/index.json` identifies known workstreams and their latest checkpoint identity/digest/path;
- `checkpoints/history/<checkpoint-id>.json` is immutable history;
- workstream-specific latest pointers may exist as derived convenience views;
- each checkpoint binds project, repository, workstream, source branch/SHA, digest, canonical sources, state, blockers, next action and STOP condition.

Resume phrases such as `continue do chat anterior` resolve through project selection, index/workstream evidence, checkpoint digest/SHA verification and reconciliation against newer GitHub state. Ambiguous consequential resumes fail closed instead of guessing. Competing sessions use expected prior identities and reconcile conflicts rather than last-writer-wins.

## Consequences
- a new chat can safely resume with minimal operator input;
- parallel planning/implementation/review no longer share an ambiguous latest pointer;
- stale checkpoints cannot silently reactivate invalid instructions;
- raw transcripts are not required for durable engineering continuity.

## Rejected alternatives
- one global latest checkpoint for all work;
- replaying entire chat history as the resume mechanism;
- selecting a workstream only by semantic similarity;
- mutable checkpoint history.