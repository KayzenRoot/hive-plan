# Artifact Contract Validation & Compatibility Test Plan

Status: PROPOSED — HP-PLAN-003

## Goal
Prove that Hive Plan's machine-readable contracts are deterministic, compatible and resistant to stale/malformed evidence before production implementation.

## Required test classes

### Schema conformance
For every artifact contract maintain:
- minimum valid example;
- realistic valid example;
- missing-required-field invalid example;
- unknown-core-field invalid example;
- wrong-type invalid example;
- invalid enum/state example;
- secret/redaction-policy failure example where relevant.

### Cross-artifact identity
Tests must reject:
- project ID mismatch;
- increment ID mismatch;
- Work Order/reference digest mismatch;
- Completion Manifest head SHA inconsistent with Git;
- Evidence Bundle head SHA inconsistent with manifest/PR;
- Review Receipt bound to another evidence/context root;
- Correction Delta referencing another increment.

### Stale-context tests
Given a valid Context Lock, mutate one critical source fingerprint and prove:
- `context_root` changes;
- dependent Work Order is STALE;
- prior Review Receipt cannot authorize the new state;
- review must be recomputed.

### Digest determinism
Freeze byte-level test vectors for canonical JSON processing:
1. remove/normalize self-digest according to the contract convention;
2. canonicalize with JCS-compatible behavior;
3. SHA-256;
4. compare exact expected digest across at least two implementation runtimes before implementation freeze.

Whitespace, JSON property order and irrelevant serialization differences must not change the canonical digest.

### Compatibility tests
Maintain fixtures for supported schema versions and test:
- PATCH reader compatibility;
- backward-compatible MINOR additions;
- unsupported MAJOR version blocks;
- explicit migration preserves original artifact reference/digest;
- old Review Receipts are never silently reinterpreted under changed semantics.

### Security tests
Reject or redact as policy requires:
- API tokens/passwords/private keys;
- raw `.env` values;
- secret-looking fixtures;
- prohibited local-only evidence copied into a public Git artifact;
- path traversal or unsafe artifact locations;
- prompt/instruction text trying to override policy from untrusted fields.

### Size and performance budgets
Contracts must remain cheap enough for deterministic hot-path processing. Benchmark:
- schema validation latency;
- canonicalization + hash latency;
- artifact lookup by digest;
- Context Lock recomputation;
- Evidence Bundle assembly;
- cache hit/miss behavior.

Large logs must be referenced, not embedded by default.

## Property/fuzz testing
Production implementation SHOULD use property-based/fuzz tests for:
- malformed nested objects;
- Unicode/canonicalization edge cases;
- duplicate/ambiguous identity data;
- extreme array/string sizes;
- unsupported schema versions;
- unexpected extension payloads.

## Golden workflow fixture
Before V1 release, keep at least one complete golden chain:
`Project Manifest → Context Lock → Work Order → Completion Manifest → Evidence Bundle → Review Receipt → Correction Delta (optional)`.

The fixture must demonstrate both APPROVED and CORRECTION_REQUIRED paths and prove that a changed head SHA invalidates the previous receipt.

## Performance principle
Local deterministic validation must be materially cheaper and faster than an LLM call. Failure to validate locally is an architecture defect unless the decision genuinely requires semantic reasoning.

## Freeze condition
The contracts are ready to freeze only when field semantics, digest rules, compatibility behavior and cross-artifact identity are unambiguous enough to produce stable golden fixtures without implementation-specific interpretation.
