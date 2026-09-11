# HP-WO-0001 — Codex Integrity Correction Prompt

## ROLE
You are performing a bounded deterministic repair of the HP-WO-0001 governance artifacts after P0 correctly blocked on integrity mismatch.

Do NOT redesign the product. Do NOT change architecture, scope, acceptance criteria, endpoints, persistence policy, visual policy, agent ownership or evidence thresholds. This task repairs only cryptographic/fingerprint metadata and then resumes the already-authorized execution if P0 becomes valid.

## READ FIRST
Read completely:
1. `work-orders/HP-WO-0001/preflight-integrity-correction.md`
2. `work-orders/HP-WO-0001/context-lock.json`
3. `work-orders/HP-WO-0001/work-order.json`
4. `work-orders/HP-WO-0001/implementation-blueprint.json`
5. `work-orders/HP-WO-0001/codex-execution-prompt.md`

## KNOWN ROOT CAUSE
Locked source:
`docs/81-cockpit-realtime-projection-contract.md`

Locked blob SHA:
`90f68500572844434bccc9e7d9a2f756e433a5f8`

Fingerprint algorithm:
`SHA256(UTF8("git-blob-sha1:" + blob_sha1))`

Expected correct fingerprint:
`sha256:c7b5553a16e7729ab4937612315964037041b7cfaa6eaa09a6bc08c911b58aaf`

Current invalid value is missing one `0`.

## EXECUTE
### C0 — Safety
- Synchronize repository.
- Stay on `feat/hp-wo-0001-cockpit-foundation`.
- Working tree must be clean before repair.
- Do not alter runtime/application implementation files during C0-C6.

### C1 — Recompute source fingerprints
For every one of the 14 Context Lock sources:
- resolve the blob SHA at that source's locked `git_sha`;
- calculate fingerprint programmatically;
- compare declared vs calculated.

Expected outcome: exactly ONE mismatch, `docs/81-*`, with the expected correct fingerprint above.

If zero mismatches, more than one mismatch, source missing, or a locked source content identity differs unexpectedly, STOP with `BLOCKED_UNEXPECTED_INTEGRITY_DRIFT` and list exact evidence.

### C2 — Correct Context Lock
Correct only the bad source fingerprint.

Recompute `context_root` exactly as defined in `preflight-integrity-correction.md`:
- sort source entries by `(repository, path, source_id)`;
- JCS/RFC-8785 canonicalize the sorted full source-entry array;
- SHA-256 UTF-8 canonical bytes;
- lowercase `sha256:<hex>`.

Then recompute `context-lock.json` top-level `artifact_digest`:
- remove top-level `artifact_digest` from digest input;
- JCS canonicalize full remaining artifact;
- SHA-256;
- restore digest;
- independently recompute once to prove equality.

### C3 — Repair downstream Work Order identity
In `work-order.json`:
- update only the referenced Context Lock digest to the corrected one;
- do not change objective/scope/out-of-scope/requirements/architecture/constraints/AC/tests/deliverables/evidence/STOP;
- recompute Work Order `artifact_digest` using the same top-level self-digest exclusion rule;
- independently verify it.

### C4 — Repair Blueprint identity
In `implementation-blueprint.json`:
- update Work Order ref digest;
- update Context Lock ref digest;
- update the docs/81 source fingerprint wherever represented;
- do not alter semantic implementation guidance unless a field contains only a now-stale digest/reference;
- recompute Blueprint `artifact_digest` by JCS/SHA-256 self-digest exclusion;
- independently verify it.

### C5 — Repair rendered prompt + CompileGuard
Update only identifiers/digests/fingerprint references in `codex-execution-prompt.md`. Do not rewrite its implementation plan.

Supersede or update CompileGuard evidence so it states:
- prior PASS was invalidated by integrity compilation defect;
- all 14 fingerprints were programmatically checked;
- exactly docs/81 differed;
- Context Lock/Work Order/Blueprint digests now independently verify;
- no semantic/scope change occurred;
- corrected P0 result.

Create `work-orders/HP-WO-0001/integrity-receipt.md` containing:
- before/after docs/81 fingerprint;
- all 14 source check result summary;
- old/new context_root;
- old/new Context Lock digest;
- old/new Work Order digest;
- old/new Blueprint digest;
- exact JCS/hash implementation/library/runtime;
- files changed;
- statement `SEMANTIC_CHANGE: NONE`;
- statement `SCOPE_EXPANSION: NONE`.

### C6 — Commit governance repair
Commit only the authorized governance/integrity files.

Recommended commit message:
`fix(hp-wo-0001): repair context lock integrity chain`

### C7 — Re-run strict P0
Now run the original P0 again from `codex-execution-prompt.md`.

P0 must prove:
- branch correct;
- all source fingerprints fresh;
- Context Lock digest valid;
- Work Order digest valid;
- Blueprint digest valid;
- all cross-artifact references consistent;
- no semantic scope drift.

If any fails, return `STATUS: BLOCKED` and do not touch application/runtime files.

### C8 — Resume original HP-WO-0001 automatically
If and only if corrected P0 is PASS, continue the original `codex-execution-prompt.md` from P1 through P10 without asking the operator for another prompt.

All original AC-01..AC-15, evidence requirements and STOP CONDITION remain unchanged.

## OUTPUT
At completion return:
1. `INTEGRITY_CORRECTION: PASS | BLOCKED`
2. exact correction commit SHA
3. old/new fingerprint and all new digests
4. P0 result
5. if P0 PASS, normal HP-WO-0001 execution result from the original output contract
6. if blocked, exact failed deterministic check

## STOP CONDITION
Never bypass or weaken P0. Never treat this correction as permission to change semantics. If the cryptographic chain cannot be made reproducible from repository truth, stop rather than continue implementation.