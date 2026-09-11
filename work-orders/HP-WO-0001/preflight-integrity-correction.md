# HP-WO-0001 — Preflight Integrity Correction

Status: AUTHORIZED DETERMINISTIC CORRECTION
Reason: P0 `BLOCKED_STALE_CONTEXT` was triggered by compiled integrity metadata, not by a material source change.
Scope expansion: NONE
Runtime implementation authorization: unchanged

## Root cause
The locked Git blob for `docs/81-cockpit-realtime-projection-contract.md` at base SHA `873240792f4185b8ca96c961d07ce4724fa4912a` is:

`90f68500572844434bccc9e7d9a2f756e433a5f8`

Frozen fingerprint convention:

`SHA256(UTF8("git-blob-sha1:" + blob_sha1))`

Correct fingerprint:

`sha256:c7b5553a16e7729ab4937612315964037041b7cfaa6eaa09a6bc08c911b58aaf`

The compiled Context Lock incorrectly contained:

`sha256:c7b5553a16e7729ab4937612315964037041b7cfaa6eaa9a6bc08c911b58aaf`

The defect is one missing `0` in compiled metadata. Independent verification of the remaining 13 source fingerprints against the locked Git tree found them equal to their declared values.

## Required correction
No canonical source content, acceptance criterion, scope or architecture may change.

1. Recompute all 14 source fingerprints from the Git blob SHA at the locked `git_sha`. Do not trust copied fingerprint text.
2. Confirm that only the `docs/81-*` fingerprint differs from the current Context Lock. If any other source differs, STOP with `BLOCKED_UNEXPECTED_INTEGRITY_DRIFT`.
3. Correct the `docs/81-*` fingerprint.
4. Recompute `context_root` deterministically using the convention below.
5. Recompute the Context Lock `artifact_digest` using the artifact digest convention below.
6. Update the Work Order Context Lock reference to the corrected Context Lock digest, then recompute Work Order `artifact_digest`.
7. Update Implementation Blueprint references and source fingerprints to the corrected Work Order / Context Lock values, then recompute Blueprint `artifact_digest`.
8. Update `codex-execution-prompt.md` identifiers/digests only. Do not alter execution semantics.
9. Produce an integrity receipt listing old/new values and the exact algorithm/tool/runtime used.
10. Re-run P0 from the corrected artifacts. Continue P1-P10 only if P0 is PASS.

## Exact `context_root` convention for this correction
This resolves the byte-level ambiguity left open for implementation vectors while remaining consistent with D-020 / HP-PLAN-003:

1. Use the Context Lock `sources` entries after fingerprints are recomputed.
2. Sort entries ascending by tuple `(repository, path, source_id)` using Unicode code-point/UTF-8 lexical order for these ASCII identifiers.
3. Preserve all source-entry fields exactly: `source_id`, `source_type`, `authority`, `repository`, `path`, `git_sha`, `fingerprint`, `critical`.
4. JCS/RFC-8785 canonicalize the sorted JSON array.
5. Compute SHA-256 over canonical UTF-8 bytes.
6. Store as lowercase `sha256:<64 hex>`.

## Exact artifact digest convention
For each governed JSON artifact corrected here:

1. Parse JSON and reject duplicates/malformed values.
2. Remove the top-level `artifact_digest` member entirely for digest input.
3. JCS/RFC-8785 canonicalize the remaining JSON value.
4. Compute SHA-256 over canonical UTF-8 bytes.
5. Store lowercase `sha256:<64 hex>` back in `artifact_digest`.
6. Re-parse and independently recompute once more; stored and computed values must match exactly.

Do not hash pretty-printed/raw file bytes. Do not replace JCS with ordinary serializer output unless the chosen library is proven JCS compatible for this payload.

## Files authorized to change during integrity correction
- `work-orders/HP-WO-0001/context-lock.json`
- `work-orders/HP-WO-0001/work-order.json`
- `work-orders/HP-WO-0001/implementation-blueprint.json`
- `work-orders/HP-WO-0001/codex-execution-prompt.md`
- `work-orders/HP-WO-0001/blueprint-compileguard-report.md` or a superseding integrity/CompileGuard receipt
- `work-orders/HP-WO-0001/integrity-receipt.json|md`

No application/runtime implementation file is authorized to change until corrected P0 passes.

## FailureShield lesson
Classify this incident as `COMPILED_INTEGRITY_METADATA_TYPO` / `UNVERIFIED_DECLARED_DIGEST`.
Future Work Order compilation must compute fingerprints and digests programmatically, validate them twice, and never hand-transcribe cryptographic identifiers.

## STOP CONDITION
Correction is complete only when:
- all 14 source fingerprints are recomputed from Git;
- exactly the known docs/81 fingerprint correction is required;
- corrected `context_root` is reproducible;
- Context Lock, Work Order and Blueprint artifact digests independently verify;
- all downstream references match;
- corrected CompileGuard/P0 is PASS.

If any semantic field changes or any second unexplained source mismatch appears, STOP. Do not continue implementation.