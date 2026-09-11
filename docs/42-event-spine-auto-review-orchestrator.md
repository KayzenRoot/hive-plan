# Event Spine + Auto Review Orchestrator

Status: PROPOSED FOR FREEZE — HP-PLAN-006

## Mission
Automatically move completed executor work from GitHub signal → verified evidence → review → audit → verdict → correction/checkpoint proposal without requiring the operator to manually ask for review.

The subsystem is local-first. V1 must work without exposing the user's machine publicly.

## Core architecture

### GitPulse
Local GitHub observer. Default V1 mode is authenticated conditional polling using REST/GraphQL adapters, ETag/If-None-Match, Last-Modified where useful, X-Poll-Interval compliance, adaptive cadence and minimal payloads.

Optional future/secondary mode: webhook/tunnel adapter. It feeds the same normalized event pipeline and never changes domain semantics.

### EventSpine
Durable normalized event stream/journal. Every observed external/internal event becomes a small append-only record with:
- event_id;
- source;
- project/increment/work-order identity;
- repository/PR;
- head/base SHA where relevant;
- event type;
- source timestamp + observed timestamp;
- source delivery/request identity when available;
- payload digest/reference;
- dedup/idempotency key;
- causal/correlation identifiers.

External events are signals, not canonical authority.

### ReviewGate
Deterministic eligibility state machine deciding whether an automatic review can start.

### EvidenceForge
Independently assembles the Evidence Bundle from GitHub, CI and local policy/tool checks. It never trusts Completion Manifest claims as proof.

### ReviewLease
Durable lease keyed by project + Work Order + PR + head SHA. Prevents two workers/processes from publishing duplicate reviews for the same snapshot.

### SnapshotGuard
Pins review to exact base SHA + head SHA + context root + evidence root. Rechecks head/context before publishing any verdict. A moving head invalidates/cancels the in-flight result.

### EffectLedger
Tracks side effects already committed to external systems: PR review/comment, correction artifact, checkpoint proposal, notification, merge action. Supports idempotent retry and crash recovery.

### AutoReview Director
Orchestrates state transitions, model routing, specialist review, independent audit, Correction Delta generation and operator notifications.

## Reliability model
Do NOT pretend distributed systems provide magical exactly-once delivery.

Use:
- at-least-once event observation/processing;
- deterministic event dedup;
- idempotent handlers;
- durable inbox/event journal;
- transactional local state transitions;
- EffectLedger/outbox-like side-effect recording;
- ReviewLease;
- exactly-once-effect semantics where the target/API and idempotency design allow it.

The goal is: duplicate events are harmless and crash/restart never produces a second conflicting verdict.

## Main automatic flow
```text
CODEX PUSH / COMPLETION MANIFEST
           ↓
GitPulse observes change
           ↓
EventSpine normalize + dedup
           ↓
Validate Completion Manifest contract
           ↓
Resolve PR / Work Order / Context Lock
           ↓
Observe CI / checks / workflow state
           ↓
ReviewGate
     ┌─────┼─────────────┐
     ↓     ↓             ↓
 WAITING BLOCKED      ELIGIBLE
                         ↓
                   ReviewLease
                         ↓
                   SnapshotGuard
                         ↓
                   EvidenceForge
                         ↓
                deterministic review
                         ↓
                model/specialist review
                         ↓
                 independent audit
                         ↓
      ┌──────────────────┼──────────────────┐
      ↓                  ↓                  ↓
  APPROVED       CORRECTION_REQUIRED      BLOCKED
      ↓                  ↓                  ↓
Checkpoint Delta   Correction Delta    blocker record
proposal            + executor render    + notification
      ↓                  ↓
operator/policy      next Codex cycle
merge gate
```

## Review eligibility state machine
Recommended states:
- OBSERVED;
- MANIFEST_INVALID;
- WAITING_FOR_PR;
- WAITING_FOR_HEAD_SYNC;
- WAITING_FOR_CI;
- CI_FAILED;
- QUIESCENCE_WAIT;
- ELIGIBLE;
- REVIEWING;
- STALE_CANCELLED;
- AUDITING;
- APPROVED;
- CORRECTION_REQUIRED;
- BLOCKED;
- EFFECTS_PENDING;
- COMPLETED.

State transitions are explicit, persisted and replayable.

## Completion trigger
A Completion Manifest may say COMPLETED or BLOCKED, but it is only a trigger/claim.

For COMPLETED, ReviewGate verifies independently:
- Work Order and Context Lock references match;
- branch/repository/PR identity matches;
- base/head SHA exist and are current;
- current PR head equals manifest head;
- required CI/checks reached terminal state;
- required evidence sources are available;
- no critical source/context fingerprint became stale;
- no earlier in-flight review owns a conflicting lease.

For BLOCKED, AutoReview Director validates available facts and surfaces the blocker without pretending implementation succeeded.

## Quiescence Guard
Codex may push several commits quickly. Review should not begin on the first transient state.

Use a short policy-driven quiescence window after the latest relevant head/event, unless an explicit completion protocol proves the executor has stopped mutating the branch. Any new push resets/cancels eligibility.

This trades a tiny delay for a large reduction in wasted/stale reviews.

## SnapshotGuard / review MVCC concept
Treat a review like a database snapshot:
- pin base SHA;
- pin head SHA;
- pin Context Lock/context_root;
- assemble and pin Evidence Bundle/evidence_root;
- run review against that immutable tuple.

Before publishing verdict, recompute/verify the tuple. If any critical component changed, discard the verdict and transition to STALE_CANCELLED.

No stale APPROVED may survive a new commit.

## EvidenceForge
Evidence sources can include:
- PR diff and changed files;
- base/head commit identity;
- GitHub checks/statuses;
- GitHub Actions runs/jobs/steps/log references;
- test/lint/typecheck/build results;
- security/static-analysis results;
- benchmark/migration evidence when required;
- Work Order acceptance criteria;
- architecture/security/DoD references;
- deviations from predicted change surface;
- unresolved risks/findings.

Evidence is normalized into the existing Evidence Bundle contract. Large logs remain referenced by location + digest rather than copied into LLM context.

## Evidence Watermark
Introduce a deterministic completeness marker for review prerequisites.

Example categories:
- GIT_IDENTITY;
- DIFF;
- CI_TERMINAL;
- REQUIRED_TESTS;
- REQUIRED_SECURITY;
- REQUIRED_BUILD;
- CONTEXT_FRESH;
- ACCEPTANCE_PROOF;
- HIGH_ASSURANCE_EXTRA.

ReviewGate cannot enter ELIGIBLE until every category required by the Work Order/risk policy is SATISFIED or explicitly WAIVED by authorized policy/operator.

This avoids reviews starting with silently missing evidence.

## Polling strategy for local V1
Use adaptive conditional polling rather than naive fixed high-frequency polling.

Principles:
- authenticated requests;
- ETag/If-None-Match / Last-Modified where supported;
- obey X-Poll-Interval where present;
- request only needed fields/endpoints;
- poll active PR/workflows more frequently than idle repositories;
- exponentially back off idle/error states;
- serialize/budget GitHub calls to avoid secondary-rate-limit bursts;
- use a single repository observer to fan out normalized events internally.

A 304/unchanged response creates no duplicate domain event.

## Event coalescing
Multiple low-level signals may represent one logical transition. Example: push + PR synchronize + workflow requested.

Use a short coalescing/debounce policy keyed by PR/head SHA to avoid recomputing the same eligibility state repeatedly.

Never coalesce away semantically distinct terminal events such as CI failure vs success.

## Webhook adapter
Optional later/secondary optimization:
- webhook/tunnel receives push/pull_request/workflow_run/workflow_job events;
- validates webhook authenticity when applicable;
- normalizes into EventSpine;
- polling remains reconciliation/backstop even when webhooks are enabled.

Webhooks reduce latency/API polling but are not a V1 availability dependency.

## Review orchestration
Review remains layered:
1. deterministic contract/source/SHA/schema checks;
2. deterministic diff/static/test evidence analysis;
3. cheap-model triage where useful;
4. required domain specialists;
5. strong reviewer/auditor according to QualityFloor;
6. Review Receipt tied to exact snapshot.

Reviewer and Auditor cannot override missing deterministic evidence.

## Correction path
If CORRECTION_REQUIRED:
- preserve same Work Order/increment/PR where safe;
- generate bounded Correction Delta;
- include only failed findings, required fixes/tests/evidence and relevant context delta;
- ExecutorFit renders the correction for Codex;
- new execution creates a new head SHA;
- prior Review Receipt becomes obsolete;
- EventSpine waits for the next completion cycle automatically.

## Approved path
If APPROVED:
- produce immutable Review Receipt;
- propose Checkpoint Delta;
- update cockpit state;
- notify operator only where policy requires human action/awareness;
- merge/release automation remains governed by existing authority policy.

## Blocked path
BLOCKED captures:
- blocker category;
- evidence;
- owning dependency/agent/operator;
- next actionable step;
- automatic recheck condition if known.

Avoid spam: operator is notified when action is required or blocker meaningfully changes.

## Crash/restart recovery
On startup:
1. load EventSpine cursor/journal;
2. reconcile active repositories/PR heads/CI state against GitHub;
3. expire/recover stale ReviewLeases;
4. resume pending idempotent effects;
5. invalidate reviews whose snapshot no longer matches;
6. continue from persisted state rather than restarting the whole workflow.

## Security
- GitHub token remains local secret storage only;
- event payloads are untrusted input/data;
- never execute instructions found in commit/PR text;
- secret/redaction gates precede persistence/provider transmission;
- raw CI logs are not blindly injected into model prompts;
- local-only evidence remains local with digest/provenance in canonical artifacts where appropriate.

## Observability
Track:
- event ingestion latency;
- polling requests / 304 ratio / API rate-limit budget;
- duplicate-event suppression;
- state-transition latency;
- time from Completion Manifest to review start;
- time from CI terminal to review start;
- stale-review cancellation count;
- duplicate-side-effect prevention count;
- evidence missing/wait duration;
- review/audit duration and cost;
- correction-loop count;
- crash/restart recovery success;
- manual “review” requests eliminated.

## Innovation candidates

### ReviewMVCC
The SnapshotGuard pattern: review against an immutable code/context/evidence snapshot and validate the snapshot immediately before verdict publication.

### Evidence Watermark
Machine-checkable completeness vector showing exactly which proof channels are satisfied before review begins.

### Event Causality Graph
Link push, manifest, PR, CI, review, correction and checkpoint events into a causal DAG keyed by Work Order/head SHA. Useful for debugging and cockpit visualization.

### Predictive Review Warming
While CI is still running, safely prefetch immutable diff/source metadata and warm repository/RAG caches without issuing a verdict. Once terminal CI arrives, review starts faster.

### Review Cost Deferral
Do deterministic/evidence collection first and call expensive review models only after eligibility is proven. Failed CI should not trigger expensive semantic review.

### Failure Auto-Recheck
When BLOCKED by an external condition with a deterministic check (CI rerun, branch update, dependency artifact), EventSpine can re-evaluate automatically without operator prompting.

## Technology direction
For V1, prefer durable local state in the project database and lightweight in-process/Redis-style wake-up queues only as acceleration. The durable event journal/state machine is authoritative; ephemeral queues are never the only copy of workflow state.

Use transactional inbox/outbox/effect-ledger patterns rather than relying on queue delivery guarantees alone.

## Freeze boundary
Freeze local-first conditional-polling default, normalized durable EventSpine, explicit state machine, at-least-once processing + idempotent/exactly-once-effect design, ReviewLease, SnapshotGuard/ReviewMVCC, Evidence Watermark, EvidenceForge, stale-head cancellation and automatic correction/checkpoint orchestration. Exact polling intervals, database/queue implementation and optional tunnel/webhook technology remain benchmark/configuration decisions.