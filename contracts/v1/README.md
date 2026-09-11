# Hive Plan Artifact Contracts v1

Canonical governed artifacts are JSON validated against JSON Schema Draft 2020-12.

## Files
- `common.schema.json`
- `project-manifest.schema.json`
- `context-lock.schema.json`
- `work-order.schema.json`
- `completion-manifest.schema.json`
- `evidence-bundle.schema.json`
- `review-receipt.schema.json`
- `correction-delta.schema.json`

## Canonical digest
For canonical evidence identity, remove the `artifact_digest` value from the digest input according to the implementation convention, canonicalize the remaining JSON using JCS-compatible canonicalization, then compute SHA-256. The exact byte-level test vectors must be frozen before implementation.

## Rules
1. Schema validation precedes LLM reasoning.
2. Unknown core fields are rejected; provider-specific data belongs in `extensions`.
3. Secrets are forbidden.
4. Full Git SHAs are used for governed evidence.
5. Unsupported major schema versions are BLOCKED rather than guessed.
6. Review receipts are scoped to exact code/context/evidence fingerprints.

These schemas are planning contracts in HP-PLAN-003. Production validator code is not yet authorized.
