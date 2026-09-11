# Execution Completion & Auto Review Protocol

## Goal
Remove the manual 'faça o review' step while increasing, not reducing, review rigor.

## Completion signal
Codex/executor writes a machine-readable completion manifest under a governed path such as:

```text
.hive-plan/executions/WO-XXXX.json
```

Minimum fields: Work Order ID, status (`COMPLETED` or `BLOCKED`), base SHA, head SHA, PR reference, claimed checks, evidence references, executor/runtime metadata, timestamp.

The manifest is an untrusted signal only.

## Trigger condition
A review becomes eligible when:
1. a new valid completion/block manifest is observed;
2. referenced PR/head SHA exists and is current;
3. required CI for that head reaches a terminal state, or the Work Order explicitly defines no CI requirement;
4. the event has not already been processed (idempotency key = project + WO + head SHA + review policy version).

## Review acquisition
Hive Plan independently fetches/verifies:
- base/head SHA and ancestry;
- changed files and diff/patch;
- PR metadata and unresolved review threads;
- required checks and workflow outcomes;
- test/lint/typecheck/build evidence;
- migration/security/benchmark/recovery evidence when applicable;
- active Work Order and acceptance criteria;
- Scope, Architecture, Requirements, Security, DoD, ADRs and current Checkpoint.

## Review pipeline
```text
Completion Signal
      ↓
Eligibility Gate
      ↓
Evidence Collector
      ↓
Deterministic Validators
      ↓
Risk Classifier
      ↓
Specialist Review(s)
      ↓
Independent Auditor
      ↓
APPROVED | CORRECTION REQUIRED | BLOCKED
```

## Verdict behavior
### APPROVED
- record audit evidence;
- propose canonical Checkpoint Delta;
- update PR/project state;
- advance only after policy conditions are satisfied.

### CORRECTION REQUIRED
- keep the same Work Order and PR where safe;
- create `Correction Delta N` limited to verified findings;
- generate a Codex-ready correction prompt/artifact;
- wait for a new head SHA and completion signal;
- never recursively approve its own correction without a fresh review.

### BLOCKED
- record exact blocker and evidence;
- do not create speculative implementation work;
- surface the minimum operator/technical action required to unblock.

## Reliability protections
- Idempotent event processing.
- Durable event/outbox log.
- Debounce rapid pushes so stale heads are not reviewed.
- Cancellation/supersession when PR head changes during review.
- Retry with bounded exponential backoff for provider/API failures.
- Dead-letter state for repeatedly failing review jobs.
- Immutable review receipt containing policy version, source fingerprints, SHAs, model/provider IDs, tool evidence hashes, and verdict.

## Security
Repository content and completion manifests are untrusted input. Prompt-injection filtering and canonical-source authority rules apply before any LLM call or privileged GitHub action.
