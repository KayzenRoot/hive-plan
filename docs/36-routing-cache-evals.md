# Routing, Cache & Cost Evals

Status: PROPOSED FOR FREEZE — HP-PLAN-005

## Purpose
Prove that routing and cache optimizations reduce total verified-delivery cost/latency without degrading planning, implementation or review quality.

## Golden routing corpus
Maintain representative tasks for:
- low-risk extraction/classification;
- engineering chat;
- discovery interview;
- requirements synthesis;
- architecture decision;
- Work Order compilation;
- bug/root-cause analysis;
- code/PR review;
- security review;
- HIGH_ASSURANCE audit;
- repeated task with high cache reuse;
- stale-context/cache invalidation scenario;
- provider outage/rate-limit scenario.

## Primary metrics
Quality:
- required-source recall;
- source-grounding precision;
- planning decision defect rate;
- false-APPROVED rate;
- HIGH/CRITICAL miss rate;
- first-pass executor success;
- correction rounds;
- escaped defects.

Economics:
- uncached input cost;
- cached input/cache-write/storage cost;
- output/reasoning cost;
- retry/failover cost;
- total model cost per verified increment;
- total Verified Outcome Cost including rework proxies.

Latency:
- p50/p95 route-decision latency;
- first-token/response latency where available;
- total task latency;
- time to verified merge.

Cache:
- hit ratio per cache layer;
- useful-hit ratio;
- stale-hit prevention rate;
- invalidation precision;
- cache bytes/tokens avoided;
- provider cached-token ratio;
- cache creation cost vs realized reuse.

## Routing ablations
Compare at minimum:
- strongest model always;
- cheapest model always;
- static task→tier mapping;
- QualityFloor + cost/latency ranking;
- QualityFloor + ReworkTax;
- draft/critic routing;
- project-local priors;
- shadow contextual-bandit candidate.

A more complex router is promoted only if it provides measurable value over simpler policies.

## Cache ablations
Compare:
- no local cache;
- deterministic/repository cache only;
- retrieval cache;
- ContextCapsule cache;
- safe normalized result cache;
- provider prompt caching;
- CacheValuePredictor policy.

Every cache layer must demonstrate either latency/cost benefit or deterministic correctness value sufficient to justify complexity.

## Stale-cache adversarial tests
Mutate independently:
- checkpoint;
- ADR/decision;
- architecture rule;
- requirement;
- Git SHA/file content;
- prompt/policy version;
- schema/tool version;
- privacy class.

Prove that affected cache entries are invalidated while unrelated content remains reusable where safe.

## Provider-failure tests
Simulate:
- timeout;
- rate limit;
- malformed structured output;
- provider 5xx;
- partial/stream interruption;
- model retirement/unavailability;
- context-limit mismatch;
- provider cache miss spike;
- degraded latency.

Expected behavior:
- bounded retry with idempotency where appropriate;
- circuit breaker;
- compatible failover only;
- no quality-floor bypass;
- BLOCK when no eligible route remains.

## QualityDebt tests
For tasks that permit temporary degradation, prove:
- debt is explicitly recorded;
- affected artifact/decision is traceable;
- expiration/revalidation policy exists;
- debt cannot silently apply to HIGH_ASSURANCE tasks.

## Shadow routing
New routing policies first run in shadow mode when feasible. Prefer replay/offline evaluation from captured structured task/evidence metadata. Live duplicate provider calls are sampled and budget-limited.

## Promotion gates
A routing/cache change is rejected if it materially:
- increases false approvals or HIGH/CRITICAL misses;
- increases correction rounds or escaped defects without explicit justified trade-off;
- reduces required-source recall below policy;
- returns stale cache state;
- silently downgrades assurance;
- increases Verified Outcome Cost despite reducing single-call API cost;
- creates unacceptable latency variance or provider fragility.

## Outcome feedback
After each verified increment, record route/economic outcomes using stable task/model/provider/cache profile identifiers. This dataset is used for evals and priors, never to silently rewrite canonical quality policies.

## Future research lane
Contextual-bandit or learned routing may be evaluated after sufficient verified outcomes exist. It remains SHADOW/TRIAL until it beats the deterministic QualityFloor baseline and respects every safety/quality constraint.

## Freeze rule
Freeze the eval dimensions, stale-cache/provider-failure test requirements and quality-regression gates. Numeric thresholds are calibrated from benchmark/eval data rather than guessed during planning.