# Review Outcome Metrics

Status: FROZEN — HP-PLAN-006

## Primary objective
Optimize review for verified defect prevention, not review volume.

## Cockpit metrics
Per project, increment, reviewer profile and review-engine version track:
- review wall-clock p50/p95;
- completion-to-verdict time;
- semantic context bytes/tokens;
- deterministic evidence reuse ratio;
- specialist agents spawned;
- actionable findings by severity;
- finding precision after correction/triage;
- duplicate/noise suppression;
- HIGH/CRITICAL recall on golden/historical replay;
- false-APPROVED rate;
- correction rounds;
- escaped defects discovered post-merge;
- impacted-node coverage;
- acceptance-criterion proof coverage;
- stale-review cancellations;
- cost per verified review;
- cost per prevented/reproduced defect where measurable.

## Review efficiency scorecard
Do not collapse critical quality into one scalar. Present at least three dimensions separately:
1. QUALITY: escapes, false approvals, proof/impact coverage;
2. SPEED: wall-clock, queue/wait, evidence/model time;
3. ECONOMICS: tokens/cost, cache reuse, specialist/tool cost.

## Regression rule
A faster engine version cannot be promoted if speed gain is obtained by materially increasing false approvals, HIGH/CRITICAL misses or escaped defects.

## Feature Impact Graph learning metrics
- predicted vs verified impacted nodes;
- missing-edge frequency;
- unnecessary-edge expansion;
- graph freshness;
- regression escapes traceable to missing graph edges.

## UADS agent metrics
- agent activation precision;
- unique confirmed findings per agent;
- duplicated findings across agents;
- wall-clock saved by parallelism;
- merge/conflict overhead caused by parallel implementation;
- token/context cost by role.

Agents whose unique yield does not justify cost become candidates for narrower activation policy or deterministic replacement.

## Prompt metrics
- prompt/context size by agent;
- scope violation rate;
- unrelated file edits after execution;
- acceptance/proof completion rate;
- correction delta size vs full Work Order;
- repeated correction recurrence.

## Freeze boundary
Freeze multidimensional review quality/speed/economics telemetry and promotion rules. Exact dashboards and numeric thresholds are calibrated from implementation benchmarks.