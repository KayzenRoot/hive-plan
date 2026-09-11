# Review Engine Evals & Regression Gates

Status: PROPOSED FOR FREEZE — HP-PLAN-006

## Purpose
Prove that a faster, more focused review still finds the defects that matter and does not increase false approvals or escaped regressions.

## Golden review corpus
Maintain versioned fixtures including:
- isolated frontend change;
- login/auth change;
- API contract change;
- database migration;
- cache/state change;
- async/concurrency defect;
- dependency/config update;
- cross-module refactor;
- security vulnerability;
- performance regression;
- intentionally noisy PR with unrelated untouched code;
- correction round after a prior review;
- known historical regression replay.

Each fixture records expected changed surface, semantic impact closure, required specialists, expected findings, non-findings and proof channels.

## Core quality metrics
- HIGH/CRITICAL defect recall;
- false-APPROVED rate;
- actionable finding precision;
- duplicate/noise finding rate;
- source/evidence grounding;
- acceptance-criterion proof coverage;
- impacted-node coverage;
- specialist activation precision/recall;
- stale-review publication rate (target zero);
- escaped defect rate after merge.

## Speed/economics metrics
- completion-to-review-start latency;
- review wall-clock p50/p95;
- deterministic-analysis duration;
- semantic/model duration;
- total review tokens/cost;
- files/symbols presented to models vs repository size;
- ContextCapsule reduction ratio;
- specialist count per review;
- confirmed findings per review second/token;
- correction review duration vs initial review.

## Review-scope ablations
Compare:
- full-repository/full-file model review;
- changed-files only;
- changed-symbols only;
- changed-symbols + static dependencies;
- ReviewScope + Feature Impact Graph;
- ReviewScope + FIG + prior failures;
- full proposed focused-review pipeline.

The focused pipeline must reduce review time/context while preserving or improving material-defect recall.

## Multi-agent ablations
Compare:
- one strong reviewer;
- one reviewer + deterministic tools;
- reviewer + always-on specialists;
- conditional specialists from AgentReviewPlan;
- conditional specialists + independent audit for elevated risk.

Always-on multi-agent review is rejected if it increases cost/latency without measurable quality gain.

## Impact-map tests
Inject changes where the actual regression is outside the directly edited file but inside:
- import/call graph;
- route/API consumer;
- auth middleware;
- shared type/schema;
- data migration consumer;
- test fixture/runtime config.

Measure whether Feature Impact Graph/ImpactClosure correctly includes the affected node.

## Noise tests
Seed:
- unrelated legacy TODOs;
- formatting differences;
- pre-existing lint warnings;
- speculative style preferences;
- duplicate static analyzer results.

These must not become blocking findings unless the active change worsens them or policy explicitly requires remediation.

## Finding quality gate eval
A finding counts as useful only if it has enough evidence to reproduce/verify the defect or clearly demonstrates a violated frozen requirement/contract. Reviewer verbosity is not a quality metric.

## Correction-loop eval
For CORRECTION_REQUIRED:
1. compile Correction Delta;
2. apply only targeted corrections in fixture;
3. run delta-first review;
4. verify old resolved findings do not reappear without cause;
5. verify new regression in impacted closure is still detected;
6. compare time/context against full review replay.

## Security/static analysis lane
Benchmark CodeQL/SARIF-compatible and other configured static-analysis adapters separately. Tools are promoted based on language coverage, finding quality, runtime/resource cost and incremental value over existing checks. No scanner result is automatically a blocking defect without severity/policy/evidence normalization.

## Review Blind-Spot Sentinel
After real verified merges, compare later bugs/corrections/incidents to the prior review scope and findings. Classify escapes as:
- missing graph edge;
- missing specialist;
- missed deterministic rule;
- reviewer reasoning miss;
- test/proof gap;
- requirement/spec gap;
- truly novel/unpredictable.

Repeated blind spots create improvement candidates for FIG, TestLens, FailureShield or review policy.

## Promotion gates
Reject any review optimization that materially:
- increases HIGH/CRITICAL misses;
- increases false approvals;
- reduces required acceptance-proof coverage;
- produces stale verdicts;
- hides real defects through over-aggressive scope pruning;
- increases correction loops or escaped regressions without justified quality trade-off.

## Success target
The target is not “review fewer files.” The target is:
`minimum review surface that preserves semantically complete defect coverage for the governed change`.

## Freeze boundary
Freeze golden-corpus, ablation, impact-closure, noise, correction-loop, blind-spot and promotion-gate methodology. Numeric thresholds are calibrated from implementation benchmarks.