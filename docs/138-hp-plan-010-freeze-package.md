# HP-PLAN-010 — Pre-Freeze Package

Status: PRE-FREEZE / NOT YET MERGED
Issue: #23
Planning branch: `docs/hp-plan-010-engineering-chat-project-brain`

## Scope
This package closes the conceptual planning phase for Engineering Chat + Project Brain and defines the mechanical gates required before canonical freeze/merge.

## Included architecture families
- Engineering Chat + Project Brain authority/retrieval;
- MemoryProvider with HIVE preferred and embedded local fallback;
- operational/failure memory;
- voice-first and rich multimodal interaction;
- ConversationDirector, ActionRouter and agent council;
- continuity/focus/checkpoint/resume;
- rich visual response renderer;
- Obsidian Glass / Electric Signal visual bible;
- Hive Core + VoiceOrb cinematic systems;
- future-public product seams without SaaS scope expansion;
- Implementation Blueprint Compiler and low-cost executor profile;
- multi-workstream continuity;
- blueprint deviations and evidence-bound execution.

## Machine-readable contracts added
- `contracts/v1/checkpoint-index.schema.json`
- `contracts/v1/workstream-checkpoint.schema.json`
- `contracts/v1/implementation-blueprint.schema.json`
- `contracts/v1/blueprint-deviation.schema.json`

## Initial fixtures
Positive and intentionally invalid fixtures are stored under `contracts/v1/fixtures/` for checkpoint index, implementation blueprint and blueprint deviation. Additional workstream-checkpoint and semantic-policy fixtures remain required before final freeze.

## Freeze gates
### F1 Schema resolution
All new schemas resolve against `common.schema.json` under JSON Schema Draft 2020-12 and reject unsupported major versions/unknown core fields.

### F2 Positive fixtures
Every new schema has at least one valid representative fixture.

### F3 Negative fixtures
Every new schema has fixtures proving rejection of missing required fields, unknown core fields, unsupported schema major and invalid enum/digest/timestamp/reference values where applicable.

### F4 Semantic invariants
Validation beyond JSON Schema proves:
- active workstream references a listed workstream;
- checkpoint path/id resolves and project/repository match;
- immutable checkpoint history is not mutated;
- resume selection fails closed when ambiguous;
- blueprint project/increment/work-order/context-lock identities agree;
- blueprint scope cannot silently exceed Work Order scope;
- FROZEN decisions cannot be changed by executor output;
- material deviation triggers recompile/escalation according to policy;
- exact-head review binds to the blueprint/work-order/context-lock digests used for execution.

### F5 Security/privacy
No secrets/raw audio/private transcript are required in checkpoint/blueprint artifacts. External/untrusted content cannot modify authority or tool policy.

### F6 Evals
Resume, long-chat compaction, wrong-workstream selection, stale context, HIVE offline, Redis loss, prompt injection, voice ambiguity, low-cost executor comparison and visual degradation have explicit eval plans.

### F7 Decision ledger
New decisions for multi-workstream continuity and governed implementation blueprints are recorded as canonical decision candidates before merge.

### F8 Parallel-work reconciliation
Before merging HP-PLAN-010, re-read current `main` and HP-WO-0001 state. If HP-WO-0001 changed critical sources, reconcile/rebase and revalidate planning assumptions. Do not invalidate or mutate its implementation branch from this planning package.

### F9 Final checkpoint
Create immutable planning checkpoint with exact branch head, source fingerprints, issue #23, remaining blockers, next action and STOP condition; update continuity index only after validation.

## Current verdict
`PRE_FREEZE_READY_WITH_MECHANICAL_GATES`

No unresolved conceptual HIGH/CRITICAL architecture gap is known in HP-PLAN-010. Final freeze is intentionally withheld until F1-F9 are evidenced, especially schema/semantic fixture validation and parallel-work reconciliation.

## STOP CONDITION
Do not label HP-PLAN-010 FROZEN and do not merge it to `main` until F1-F9 are PASS or an explicitly authorized, documented exception exists.