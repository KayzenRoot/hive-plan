# Model Router + Cache/Cost Evals

Status: PROPOSED — HP-PLAN-005

## Goal
Prove that routing and caching lower cost/latency without lowering engineering quality.

## Required evaluation slices
- simple extraction/classification;
- planning/discovery;
- architecture tradeoff;
- Work Order synthesis;
- code-review triage;
- security-sensitive review;
- evidence audit;
- long-context project question;
- repeat request with unchanged canonical state;
- repeat request after critical-source change;
- provider outage/rate-limit scenario.

## Primary metrics
- quality/pass score against golden expectations;
- source-grounding accuracy;
- false-approval rate;
- escalation precision/recall;
- cost per accepted task;
- cost per verified increment;
- latency p50/p95;
- uncached input tokens;
- cached input tokens / cache-hit ratio;
- output/reasoning tokens;
- retries/failovers;
- correction rounds;
- human intervention rate.

## Cache correctness gates
A cache strategy fails if it returns a result after any dependency that should invalidate it changes. Required mutation tests include checkpoint, ADR, Git head, policy profile, prompt/template, model capability profile and source root.

## Routing ablations
Compare at least:
- always-strong baseline;
- always-cheap baseline;
- static task-class router;
- task + risk router;
- task + risk + observed-quality router;
- task + risk + quality + provider-health/cost router.

The chosen router must beat the simpler baseline on operating cost/latency without violating quality floors.

## Shadow routing
Candidate route changes run in shadow mode first where practical. For expensive models, use sampled shadow evaluations rather than doubling every production call.

## Provider cache eval
Measure provider-specific cache effectiveness independently from local caches:
- stable-prefix hit rate;
- cache-write cost when applicable;
- cache-read savings;
- latency delta;
- invalidation/fingerprint correctness;
- break-even reuse count.

## Failover tests
Simulate rate limits, timeout, malformed structured output, partial outage and unavailable preferred model. Verify compatible failover or explicit BLOCK. Silent downgrade below QualityFloor is forbidden.

## Promotion rule
No routing/model/cache policy becomes default until it improves its claimed objective on representative tasks and passes quality/security regression gates. Exact numeric thresholds are established from benchmarks, not guessed during planning.