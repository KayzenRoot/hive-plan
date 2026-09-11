# HP-PLAN-010 — Zero-Friction Checkpoint + Resume Protocol

Status: PROPOSED

## Mission
Allow a new chat/session to continue the project correctly from GitHub with a minimal phrase such as `continue do chat anterior`, without requiring the operator to upload handoff files or manually restate context.

## Core principle
Conversation memory is convenient but non-canonical. GitHub-hosted checkpoint state is the durable resume anchor.

## Checkpoint architecture
Maintain two layers:
1. immutable checkpoint history under `checkpoints/history/`;
2. a small mutable pointer under `checkpoints/latest.json` that identifies the latest valid resume checkpoint.

A checkpoint is a machine-readable continuity package plus a concise human-readable companion.

## Required checkpoint fields
- checkpoint_id;
- schema_version;
- project/repository;
- created_at;
- source_branch;
- source_commit_sha;
- planning_or_implementation_phase;
- active_issue / Work Order / PR where applicable;
- current_objective;
- completed_since_previous;
- canonical_decisions_added_or_changed;
- current architecture/scope references;
- active branches and their purpose;
- known blockers/risks;
- open questions;
- exact next recommended action;
- STOP condition / progression gate;
- critical file/source references with fingerprints;
- pending reviews/corrections;
- active agent/team state when relevant;
- model/tool constraints that materially affect continuation;
- checkpoint digest and supersedes link.

## Resume phrase behavior
When the operator says a bounded continuation phrase such as:
- `continue do chat anterior`;
- `continue de onde paramos`;
- `retome o Hive Plan`;
- `continue o planejamento`;

the ConversationDirector should:
1. identify the active project from explicit selection/session metadata;
2. read `checkpoints/latest.json`;
3. verify referenced checkpoint/digest/source SHA;
4. inspect any newer canonical GitHub state that could supersede it;
5. reconstruct a `SessionResumeCapsule`;
6. show a short resume receipt if useful;
7. continue from `next_recommended_action` without asking the operator to re-upload context already available in canonical sources.

## SessionResumeCapsule
The resume capsule contains only what is needed for safe continuation:
- authoritative checkpoint;
- current source SHA/freshness;
- active objective;
- open work and blockers;
- applicable decisions/ADRs;
- relevant Work Order/review state;
- next action;
- critical context references.
It does not replay the entire old transcript.

## Automatic checkpoint triggers
Create/update a checkpoint after material transitions, including:
- planning round/freeze;
- Work Order authorization;
- implementation completion claim;
- review verdict;
- correction round;
- merge/release;
- major architecture/scope decision;
- chat/session approaching compaction threshold;
- operator explicitly asks for checkpoint/handoff.

A lightweight debounce/coalescing policy prevents one commit per trivial conversational turn.

## Staleness and conflict
If current GitHub state differs materially from the checkpoint, resume enters `RECONCILE_REQUIRED` and explains the delta. Never blindly resume stale instructions.

## Multi-chat concurrency
Checkpoint writes carry expected prior checkpoint ID/digest. Competing sessions cannot silently overwrite each other. Conflicts create a reconciliation checkpoint rather than last-writer-wins ambiguity.

## Privacy
Do not store raw private conversation transcript by default. Persist only engineering state necessary for continuity, with provenance and redaction.

## UX
The user should be able to open a fresh chat and type only `continue do chat anterior`. If the project is already selected/known, no file upload or manual recap is required.

## STOP CONDITION
Freeze only when latest-pointer semantics, immutable history, resume verification, stale/conflict handling, automatic triggers and privacy rules are represented in contracts/tests.