# HP-PLAN-010 — Checkpoint Artifact Contract

Status: PROPOSED

## Mission
Define a compact, machine-readable, source-grounded checkpoint so a new chat/session can resume safely with only `continue do chat anterior` and repository access.

## Canonical layout
`checkpoints/latest.json` is a mutable pointer only.
`checkpoints/history/<checkpoint-id>.json` is immutable after publication.

## Required checkpoint fields
- checkpoint_id;
- schema_version;
- project_id;
- repository;
- created_at UTC;
- source_branch;
- source_commit_sha;
- project_phase;
- current_objective;
- active_issue_ids;
- active_work_order_ids;
- active_pr_ids;
- active_branches;
- canonical_sources[] with path, blob/git identity, authority and freshness;
- frozen_decisions[];
- unresolved_decisions[];
- blockers[];
- completed_since_previous[];
- remaining_scope[];
- known_risks[];
- failure_patterns_relevant[];
- next_recommended_action;
- stop_condition;
- context_lock_state;
- last_verified_github_watermark;
- resume_policy;
- digest.

## Resume policy
`resume_policy` includes:
- SAFE_CONTINUE when repo/source fingerprints still match;
- RECONCILE_REQUIRED when noncritical changes exist;
- STALE_CONTEXT_LOCK when critical source fingerprints changed;
- BLOCKED when canonical truth cannot be established.

## SessionResumeCapsule
The runtime compiles the checkpoint into a smaller resume capsule containing only facts needed for the next turn. It must preserve exact IDs, SHAs, decisions, blockers and STOP condition losslessly.

## Update triggers
Create a new immutable checkpoint after:
- planning freeze/unfreeze;
- Work Order authorization;
- implementation completion manifest;
- review verdict;
- correction round completion;
- merge/release;
- consequential architecture/decision change;
- chat/session handoff when material state changed.

Do not checkpoint every conversational sentence.

## Reconciliation
Before resuming, compare checkpoint source SHA/fingerprints against repository reality. If changed:
1. classify changed files/sources by authority and dependency reach;
2. recompute impacted decisions/WO/context lock;
3. produce a reconciliation delta;
4. only then compile a fresh resume capsule.

## Failure behavior
Missing/invalid digest, missing canonical source, wrong project, unsupported schema major or conflicting latest pointers fail closed.

## Human-readable projection
The UI may show a short `Where we are / Done / Remaining / Blockers / Next` summary, but the JSON artifact remains source for deterministic resume.