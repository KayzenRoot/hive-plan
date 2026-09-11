# Event Spine + Auto Review Evals

Status: PROPOSED — HP-PLAN-006

## Goal
Prove that automatic observation/review is fast, restart-safe and incapable of publishing stale or duplicate verdicts.

## Golden scenarios
- one clean completion manifest + successful CI;
- completion manifest before PR exists;
- completion manifest before CI completes;
- CI failure;
- multiple rapid pushes;
- new push while review is running;
- duplicate completion manifest/event;
- duplicate webhook/poll observation;
- process crash during Evidence Bundle assembly;
- crash after review but before publishing effect;
- crash after external effect succeeds but before local acknowledgement;
- PR rebased/head changed;
- stale Context Lock;
- malformed/spoofed completion manifest;
- BLOCKED executor result;
- correction loop then success;
- provider/model outage during review;
- GitHub API rate-limit/backoff state;
- optional webhook loss with polling reconciliation.

## Correctness gates
Must prove:
- no review starts before required Evidence Watermark categories are satisfied;
- duplicate events do not create duplicate side effects;
- a changed head/context/evidence root invalidates in-flight/prior verdicts;
- no APPROVED receipt is published for a stale snapshot;
- executor claims never become verified evidence without independent confirmation;
- correction stays tied to the same governed increment unless explicit re-scope occurs;
- restart/reconciliation reaches the same valid state as uninterrupted processing.

## Polling metrics
- conditional request / 304 rate;
- API calls per active and idle repository;
- rate-limit consumption;
- detection latency p50/p95;
- X-Poll-Interval compliance where present;
- adaptive backoff behavior.

## Orchestration metrics
- event-to-normalized-event latency;
- normalized-event-to-state-transition latency;
- CI-terminal-to-review-start latency;
- completion-to-verdict latency;
- stale-review cancellations;
- duplicate event suppression rate;
- duplicate effect prevented count;
- Evidence Watermark wait time by category;
- ReviewLease contention/recovery;
- crash recovery duration;
- manual review trigger count.

## Review-economics metrics
- deterministic preflight cost/latency;
- semantic review/audit calls avoided when CI/evidence is not eligible;
- review tokens/cost per verified increment;
- correction rounds;
- false APPROVED / missed HIGH/CRITICAL findings.

## Fault injection
Inject:
- GitHub 429/403 rate-limit responses;
- transient 5xx/timeouts;
- malformed API payload/reference;
- stale ETag/cursor handling;
- duplicate journal entry attempt;
- database restart;
- worker crash at every side-effect boundary;
- lease expiration/clock skew within supported bounds;
- partial CI/log availability.

## Replay tests
Persist normalized events and state transitions so a test harness can replay a complete increment and verify deterministic state-machine behavior without live GitHub calls.

Replay is for orchestration determinism; external facts are captured as fixtures and remain marked as fixture evidence.

## Promotion gates
Reject an orchestration change if it materially:
- increases stale/duplicate verdict risk;
- loses events or active-state recovery;
- increases GitHub rate-limit pressure without meaningful latency benefit;
- triggers costly model review before deterministic eligibility;
- produces side effects without durable idempotency/effect tracking;
- makes operator intervention more frequent for recoverable conditions.

## Freeze rule
Freeze correctness/fault/replay test classes and the requirement that stale/duplicate approvals are zero-tolerance defects. Numeric latency/poll cadence targets are calibrated from local implementation benchmarks.