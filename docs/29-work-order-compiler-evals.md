# Work Order Compiler Evals & Quality Gates

Status: PROPOSED — HP-PLAN-004

## Purpose
Prevent optimization features from silently making Work Orders slower, larger, more expensive or less accurate. Every compiler/retrieval/routing change must be evaluated against representative engineering tasks.

## Golden task corpus
Maintain versioned fixtures spanning:
- targeted bug fix;
- new API endpoint;
- frontend component/change;
- database migration;
- security-sensitive change;
- refactor across modules;
- dependency upgrade;
- performance optimization;
- infrastructure/configuration change;
- documentation/planning-only change;
- previously failed/regression-prone scenario.

Each fixture records expected relevant sources, likely change surface, required proof channels and known traps.

## Compiler-only metrics
- source-grounding precision;
- required-source recall;
- irrelevant-context ratio;
- duplicate-context ratio;
- stale-source incidence;
- context tokens/bytes;
- compile latency p50/p95;
- cache hit ratio;
- deterministic-pass percentage;
- LLM calls/tokens/cost per compilation;
- change-surface precision/recall;
- TestLens precision/recall;
- FailureShield useful-hit/false-positive rate.

## End-to-end metrics
The primary quality signal is downstream execution, not a pretty Work Order.
Track:
- first-attempt acceptance rate;
- Codex execution duration;
- executor exploratory reads/commands before first relevant edit when observable;
- changed files outside predicted surface;
- correction rounds;
- defects found by review/audit;
- escaped defects;
- CI retry count;
- total LLM tokens/cost;
- total idea-to-verified-merge time;
- human interventions.

## Regression gates
A compiler change is rejected if it materially:
- increases HIGH/CRITICAL review escapes;
- reduces required-source recall below policy threshold;
- increases TestLens false negatives beyond the configured risk budget;
- increases repeated known-failure recurrence;
- increases context size/cost without measurable quality benefit;
- increases correction rounds or time-to-verified-merge without an explicit quality justification.

## Risk-weighted evaluation
LOW/STANDARD work may optimize aggressively for speed/context cost. ELEVATED/HIGH_ASSURANCE work prioritizes recall, independent evidence and proof obligations even when context/tests cost more.

A single global optimization score is forbidden if it hides critical-regression behavior.

## Retrieval ablations
Benchmark retrieval routes independently and in combinations:
- lexical only;
- semantic only;
- lexical + semantic;
- lexical + AST;
- lexical + AST + graph;
- full hybrid + FailureShield;
- full hybrid + reranker.

Measure marginal value of every layer. Remove components whose operational complexity is not justified by measurable improvement.

## Prompt/context ablations
Compare:
- full-file context vs symbol/snippet context;
- no history vs relevant validated experience memory;
- full prior Work Order vs Correction Delta;
- uncached repeated prefix vs cache-friendly stable prefix;
- static token budget vs risk/task-adaptive budget.

## Shadow compilation
Future optimization changes SHOULD first run in shadow mode on real increments: compile an alternative Work Order without sending it to the executor, compare its selected context/change/test predictions against the real outcome, and collect evidence before promotion.

Shadow mode must never duplicate expensive model calls by default; prioritize deterministic/retrieval comparisons and sampled semantic experiments.

## Feedback loop
After each verified merge:
1. compare prediction vs actual change surface;
2. compare TestLens plan vs tests that actually mattered;
3. record useful/false FailureShield hits;
4. record retrieved context used vs ignored where measurable;
5. update project-local priors/temperature map;
6. do not modify canonical policies automatically from one observation.

## Optimization scorecard
Expose in cockpit per project/compiler version:
- first-pass success;
- average correction rounds;
- median verified-merge time;
- context reduction ratio;
- retrieval useful-context ratio;
- repeated-failure prevention;
- cost per verified increment;
- compiler version/regression status.

## Freeze rule
A technology or optimization becomes default only after it beats the simpler baseline on the metrics relevant to its claimed benefit without violating quality/security gates.