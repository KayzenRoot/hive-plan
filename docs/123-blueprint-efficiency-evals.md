# HP-PLAN-010 — Blueprint Efficiency Evals

Status: PROPOSED

## Mission
Prove that richer Hive Plan blueprints reduce verified delivery cost rather than merely shift tokens from executor to planner.

## Core experiment
For representative tasks, compare prompt profiles:
A. baseline short prompt;
B. G1 structural blueprint;
C. G2 algorithmic blueprint;
D. G3 near-executable blueprint.
Use equivalent repository state and acceptance criteria.

## Primary metrics
- total tokens planner + executor + review + correction;
- executor tokens;
- wall-clock idea-to-verified-merge;
- first-pass acceptance rate;
- correction rounds;
- files touched outside predicted surface;
- contract drift incidents;
- test failures caused by implementation mistakes;
- architecture deviations;
- review findings by severity;
- human intervention;
- Verified Outcome Cost;
- escaped defect rate when measurable.

## Secondary metrics
- repo exploration commands/tool calls;
- duplicate context read;
- CompileGuard rejection rate;
- blueprint compile latency;
- context cache hit rate;
- FailureShield prevention hit rate;
- predicted vs actual file/symbol/test surface accuracy.

## Task corpus
Include:
- localized CRUD/UI change;
- state machine;
- API contract change;
- DB migration;
- SSE/realtime reconnect;
- security-sensitive change;
- performance optimization;
- bug with known FailureShield memory;
- multi-module integration;
- visual/3D feature with runtime performance constraints.

## Quality guard
A cheaper run is never a win when acceptance quality, security, resilience or evidence degrades below the required QualityFloor.

## Adaptive policy
RouteLab learns which task classes benefit from G0/G1/G2/G3. Do not use G3 everywhere: excessive blueprint detail can increase planning cost and become stale/noisy.

## Success hypothesis
The preferred profile minimizes expected Verified Outcome Cost while meeting the same QualityFloor and evidence obligations. The system may spend more tokens in planning if that reliably reduces larger executor/rework/review costs.

## Reporting
Dashboard should show savings against baseline with confidence/sample size, not unsupported marketing percentages.