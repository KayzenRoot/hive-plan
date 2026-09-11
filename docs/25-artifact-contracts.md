# Machine-Readable Artifact Contracts

Status: PROPOSED FOR FREEZE — HP-PLAN-003

## Purpose
Hive Plan must move planning, execution, evidence, review and continuity between agents/tools without relying on prose interpretation. The canonical interchange layer is a set of small, versioned, machine-readable artifacts validated deterministically before any LLM is asked to reason about them.

## Technology baseline
- Canonical format: JSON.
- Validation: JSON Schema Draft 2020-12.
- Canonicalization for evidence identifiers: JSON Canonicalization Scheme (JCS/RFC 8785 compatible processing).
- Canonical digest: SHA-256 of the canonicalized payload excluding the artifact's own digest field.
- Timestamps: RFC 3339 UTC.
- Git identity: full commit SHA, never branch name alone for evidence.
- Schema evolution: explicit `schema_version` with compatibility rules.
- Extensions: namespaced `extensions` object; unknown top-level fields are rejected in governed artifacts.

JSON is chosen as the canonical persisted/interchange form because it is language-neutral, easy for Codex and APIs to emit, cheap to validate locally, diffable in Git and broadly supported. Faster binary encodings may be used internally later, but cannot replace the canonical evidence representation without a new decision.

## Common envelope
Governed artifacts share these concepts where applicable:
- `artifact_type`
- `schema_version`
- `artifact_id`
- `project_id`
- `increment_id`
- `created_at`
- `producer`
- `risk_class`
- `context_lock_id`
- `artifact_digest`
- `extensions`

`artifact_id` is stable for the logical artifact. Corrections/new revisions receive their own revision identity rather than silently overwriting evidence already referenced by a review receipt.

## Canonical fingerprint model
A Context Lock contains an ordered set of source fingerprints such as:
- repository
- path/object identity
- source class
- Git SHA/blob SHA or equivalent deterministic version
- authority class

Hive Plan sorts and canonicalizes these entries and computes a `context_root` digest. This produces a compact stale-context check. If any critical source fingerprint changes, the recomputed root differs and dependent Work Orders/reviews are marked STALE.

Evidence Bundles use the same principle to compute an `evidence_root` over verified evidence references. A Review Receipt binds at minimum:
`project + increment + reviewed head SHA + context_root + evidence_root + policy/schema versions + verdict`.

This makes an APPROVED verdict impossible to safely reuse after code, evidence or canonical context changes.

## Contract set

### Project Manifest
Deterministic identity and lifecycle state for a project. It points to the canonical repository/default branch, lifecycle stage, checkpoint, current release line, risk profile, memory/executor/review profiles and implementation authorization.

### Context Lock
Immutable snapshot descriptor for the canonical sources and Git base used to compile a Work Order or perform a governed review.

### Work Order
The executable contract sent to Codex or another executor. It carries objective, context references, scope/out-of-scope, constraints, requirements, architecture rules, acceptance criteria, required tests, deliverables, evidence obligations, stop condition and relevant prior-failure constraints.

### Completion Manifest
Executor-produced event artifact. It may declare `COMPLETED` or `BLOCKED` and references the Work Order, branch, base/head SHA and claimed checks. It is a trigger only, never proof.

### Evidence Bundle
Hive Plan/CI assembled collection of independently verifiable evidence: diff identity, checks, tests, build/lint/typecheck/security/benchmark results as applicable, artifacts/log references, changed files and unresolved risks.

### Review Receipt
Immutable review/audit result tied to exact context/evidence/code fingerprints. Verdicts are `APPROVED`, `CORRECTION_REQUIRED` or `BLOCKED`.

### Correction Delta
Minimal change contract for the same Work Order/PR after review failure. It contains only findings, changed constraints, required fixes/tests/evidence and the next stop condition. It must not silently broaden scope.

## Authority boundaries
- Completion Manifest: CLAIM/TRIGGER authority only.
- Evidence Bundle fields backed by deterministic tools: VERIFIED FACT authority.
- Review Receipt: GOVERNANCE verdict scoped only to its exact fingerprints.
- Work Order: EXECUTION contract, not permission to override canonical sources.
- Project Manifest / Checkpoint / ADRs: canonical authority according to Source Hierarchy.

## Validation pipeline
```text
artifact received
  ↓
JSON parse
  ↓
JSON Schema validation
  ↓
secret/redaction gate
  ↓
identity/link integrity checks
  ↓
JCS canonicalization
  ↓
SHA-256 digest verification
  ↓
Git/context fingerprint verification
  ↓
policy/state-machine validation
  ↓
eligible for workflow transition
```

An LLM is not called to answer questions that this pipeline can decide deterministically.

## Compatibility rules
- `schema_version` follows semantic contract versioning.
- PATCH: clarification/validation tightening that does not invalidate valid prior artifacts unexpectedly.
- MINOR: backward-compatible optional capability.
- MAJOR: incompatible field/meaning/state transition change.
- Readers SHOULD support the current major version and configured previous compatible versions during migration.
- An unsupported major version is BLOCKED, never guessed.
- Schema migration creates a traceable migrated artifact and preserves the original digest/reference.

## Extension rule
Provider/executor-specific data goes under namespaced extensions, for example:
`extensions.codex`, `extensions.github`, `extensions.uads`.

Core workflow semantics cannot depend exclusively on an extension unless that dependency is declared by policy. This keeps Hive Plan executor/model agnostic.

## Security and privacy
- Secrets, raw tokens and credentials are forbidden in governed artifacts.
- Secret scanning/redaction runs before persistence/publication/provider transmission.
- Logs/evidence should store references and hashes when raw content is sensitive or unnecessarily large.
- Artifact producers must not copy entire prompts/transcripts when structured facts suffice.
- Public-repository policy may mark individual evidence references `local_only` while retaining non-sensitive digest/provenance metadata in Git.

## Performance and token optimization
- Validate artifacts locally without LLM calls.
- Pass artifact IDs/digests rather than repeating full payloads when both sides already possess the artifact.
- Compile context from references on demand.
- Cache schema validators.
- Cache resolved artifacts by digest.
- Use Correction Deltas rather than regenerating full Work Orders.
- Keep Evidence Bundles structured so reviewers receive only failed/suspicious areas plus required surrounding context.
- Store large logs/artifacts out-of-band and reference them by URI/path + digest.

## Future-proofing
The contract layer is independent from UI, LLM vendor, executor, vector store and GitHub authentication mechanism. Future executors, SaaS deployment or additional model providers consume the same domain contracts.

Potential future technology, not required for V1:
- Ed25519 signatures for multi-user/non-local provenance.
- transparency/append-only audit log for enterprise deployment.
- CBOR/MessagePack internal transport for high-throughput deployments while retaining canonical JSON evidence.

## Freeze gate
HP-PLAN-003 is not complete until every required artifact has a schema, representative valid/invalid examples are planned for tests, cross-artifact links are unambiguous, stale-context behavior is deterministic and the contract suite can evolve without silently reinterpreting old evidence.
