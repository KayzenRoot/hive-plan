# Planning & Delivery Flow

Status: FROZEN — HP-PLAN-002

## Goal
Create the fastest safe path from approved planning to verified code without losing traceability, quality, or recoverability.

## Core flow

```text
IDEA / CHANGE REQUEST
        ↓
DISCOVERY
        ↓
PLANNING DECISION
        ↓
ISSUE = planning increment
        ↓
CONTEXT LOCK
        ↓
WORK ORDER
        ↓
BRANCH
        ↓
CODEX EXECUTION
        ↓
PR + COMPLETION MANIFEST
        ↓
CI / EVIDENCE
        ↓
AUTO REVIEW
        ↓
AUDIT
   ┌────┼───────────────┐
   ↓    ↓               ↓
APPROVED CORRECTION    BLOCKED
   ↓      REQUIRED       ↓
CHECKPOINT   ↓        OPERATOR / DEPENDENCY
   ↓      SAME PR
MERGE
   ↓
LESSON EXTRACTION
   ↓
RAG / EXPERIENCE MEMORY
```

## Unit of work
The primary governed unit is a stable increment ID, e.g. `HP-WO-0042`.
The same ID follows the work across:
- issue
- branch
- Work Order
- execution manifest
- evidence bundle
- PR
- correction deltas
- review receipt
- checkpoint delta
- lesson/failure records

This prevents fragmented context and makes retrieval deterministic.

## Issue policy
One issue represents one decisionable/deliverable increment, not a dumping ground for an entire version.

Minimum issue fields:
- increment ID
- objective
- risk class
- scope / out of scope
- dependencies
- linked requirements/ADRs
- acceptance criteria
- current lifecycle state
- linked branch/PR/Work Order/checkpoint

Large goals remain epics/milestones and are decomposed into increments small enough to review objectively.

## Branch policy
Recommended default:
- `plan/<id>-<slug>` for planning-only changes
- `feat/<id>-<slug>` for product features
- `fix/<id>-<slug>` for defects
- `infra/<id>-<slug>` for infrastructure
- `sec/<id>-<slug>` for security changes
- `docs/<id>-<slug>` for documentation-only changes

Rules:
- branch starts from known base SHA;
- Context Lock records base SHA;
- no unrelated changes;
- no force-push/history rewriting by default;
- stale base or changed critical source triggers reconciliation.

## Work Order compilation
Work Orders are generated only after required planning gates pass.
They contain exactly the context necessary to execute the increment, including prior matching failure patterns when relevant.

Before finalizing a Work Order, Hive Plan performs:
1. canonical source check;
2. dependency check;
3. prior-error / negative-knowledge search;
4. architecture/security/data obligations check;
5. Context Lock fingerprinting;
6. acceptance-test compilation;
7. token/context minimization.

## Execution acceleration
The system should reduce Codex time by providing:
- exact files/symbols likely involved when deterministically discoverable;
- canonical constraints instead of entire project history;
- known working patterns from RAG;
- prior failure warnings;
- explicit tests to run;
- explicit stop condition;
- exact deliverable/evidence schema;
- no repeated generic instructions already enforced by UADS/Hades or repository policy.

## Pull request policy
A PR is the evidence boundary for an increment.
It must link the stable increment ID and include:
- base/head SHA
- changed files
- implementation summary
- tests/lint/typecheck/build/security checks as applicable
- Evidence Bundle
- completion manifest
- risks / deviations
- proposed checkpoint delta

## Automatic review gate
Hive Plan starts review only when:
- completion manifest is present;
- PR head matches manifest head;
- required CI has completed;
- Context Lock is not stale;
- required evidence is available.

If head changes during review, the review is invalidated and restarted against the new head.

## Review optimization
Use a layered review funnel:

### Layer 0 — deterministic checks
No LLM where Git/AST/static analysis/tests can answer reliably.

### Layer 1 — cheap model triage
Classify changed domains, likely risk, missing evidence, suspicious areas, and required specialist reviews.

### Layer 2 — specialist review
Invoke only required domains: architecture, security, data, reliability, performance, frontend, etc.

### Layer 3 — strong-model audit
Used for high-impact ambiguity, cross-domain reasoning, contested findings, or HIGH_ASSURANCE work.

This reduces cost and latency while preserving stronger reasoning where it has the highest value.

## Correction loop
`CORRECTION REQUIRED` never creates a fresh unrelated task when correction safely remains inside the original increment.

Generate only:
- `Correction Delta 01`, `02`, etc.;
- exact failed acceptance criteria/findings;
- changed constraints/evidence;
- required tests;
- stop condition.

Corrections stay on the same branch/PR unless the current branch is unsafe or architecturally invalid.

## Merge gate
Merge is eligible only after:
- objective review obligations satisfied;
- no known HIGH/CRITICAL defects;
- required CI green;
- head SHA still matches reviewed SHA;
- checkpoint delta is valid;
- canonical documentation impact is reconciled.

## Post-merge learning
After merge/release outcome is known:
- extract proven reusable patterns;
- extract failures/root causes/corrections;
- update experience memory;
- compare estimated vs actual cost/time;
- record review escapes/regressions if later discovered.

## Speed metrics
Measure, per increment:
- planning cycle time
- Work Order compile latency
- Codex execution time
- CI time
- review latency
- correction rounds
- time-to-merge
- human interventions
- tokens/cost
- escaped defects
- repeated failures prevented

Speed optimization must target total `idea → verified merge` time, not just code-generation speed.

## Frozen quality rule
The fastest workflow is the one that minimizes rework. Hive Plan optimizes for `verified throughput`, not raw commits per hour.
