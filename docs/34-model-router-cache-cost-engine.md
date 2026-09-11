# Model Router + Cache/Cost Engine

Status: PROPOSED FOR FREEZE — HP-PLAN-005

## Mission
Select the cheapest/fastest execution path that still satisfies the task's quality, risk, privacy and assurance requirements. Cost optimization is subordinate to correctness and review safety.

## Internal components

### RouteGuard
Classifies task type, risk, ambiguity, blast radius, required assurance, tool needs and latency sensitivity. Produces a minimum capability/assurance profile before any provider/model is selected.

### ModelMesh
Provider-neutral registry of model profiles: capabilities, context limits, structured-output/tool support, reasoning/effort controls, observed quality, latency, price, cache behavior, availability and privacy constraints. Static vendor claims are advisory; project evals and telemetry provide operational scores.

### QualityFloor
Defines the minimum acceptable profile by task/risk. A cheaper model cannot be selected if it falls below the floor. HIGH_ASSURANCE work may require independent second-pass critique or a stronger reviewer even when a cheaper draft model is used.

### CacheFabric
Layered cache system keyed by canonical fingerprints, not conversational guesswork.

Layers:
1. deterministic fact/tool cache;
2. repository/retrieval cache;
3. semantic retrieval result cache;
4. compiled ContextCapsule cache;
5. normalized task/result cache where safe;
6. provider prompt/context cache;
7. optional response cache only for deterministic, state-fingerprinted, policy-approved tasks.

### BudgetPilot
Applies per-task/project budgets for tokens, money, latency and retry count. Budgets guide routing but never authorize violating QualityFloor.

### ProviderSentinel
Tracks provider/model health, rate limits, timeouts, error rates, cache hit behavior and latency. Supports circuit breakers, backoff and failover to compatible routes.

### RouteLab
Shadow-routing/eval subsystem. Alternative model/cache strategies can be evaluated without silently changing production routing. Expensive shadow calls are sampled rather than duplicated by default.

## Routing flow
```text
TASK / AGENT REQUEST
      ↓
CAN THIS BE DETERMINISTIC?
      ├─ YES → LOCAL TOOL / CACHE
      ↓ NO
ROUTEGUARD CLASSIFICATION
      ↓
QUALITY FLOOR + PRIVACY POLICY
      ↓
CACHEFABRIC LOOKUP
      ├─ SAFE HIT → VALIDATE FINGERPRINTS → RETURN
      ↓ MISS
MODEL MESH CANDIDATES
      ↓
COST/LATENCY/QUALITY SCORE
      ↓
SELECT ROUTE
      ↓
PROVIDER CACHE-FRIENDLY REQUEST
      ↓
OUTPUT VALIDATION
      ↓
ESCALATE / ACCEPT / BLOCK
      ↓
TELEMETRY + LEARNING
```

## Routing dimensions
At minimum:
- task class: extraction, conversation, discovery, planning, architecture, coding support, review, audit, security, summarization;
- risk/assurance: LOW, STANDARD, ELEVATED, HIGH_ASSURANCE;
- ambiguity/novelty;
- irreversible impact;
- cross-domain complexity;
- required structured/tool capabilities;
- expected context size;
- latency sensitivity;
- privacy/data policy;
- current provider/model health;
- observed project-specific quality;
- marginal cost.

## Draft/critic pattern
For selected consequential tasks, separate generation authority from decision authority:
- cheap/fast model may draft or extract;
- stronger or independently routed model critiques when policy requires;
- deterministic evidence remains primary;
- no model self-assertion upgrades assurance.

This avoids paying frontier-model cost for every token while preserving strong review on high-impact decisions.

## Cache architecture

### Fingerprint rule
Every reusable cache entry includes dependencies such as:
- project/source root;
- checkpoint/decision fingerprints;
- Git base/head where relevant;
- policy version;
- prompt/template version;
- model/provider profile where output depends on it;
- tool/schema version.

A changed critical dependency invalidates the entry deterministically.

### Cache safety classes
- EXACT_SAFE: deterministic output/facts, reusable when fingerprints match.
- SEMANTIC_SAFE: retrieval/rerank result reusable with strict source/query/profile fingerprints.
- ADVISORY: reusable only as input/context, never as canonical answer.
- NO_CACHE: security-sensitive, highly dynamic, non-idempotent or policy-prohibited tasks.

### Provider prompt-cache layout
Keep stable reusable content before dynamic task content when provider semantics reward prefix reuse.
Recommended logical segmentation:
```text
STABLE CORE
- system/engineering constitution
- tool contracts
- source hierarchy
- review protocol
- output schemas

PROJECT-STABLE
- approved invariants
- architecture rules
- executor profile

TASK-DYNAMIC
- current user/task
- current ContextCapsule
- Git/PR/evidence delta
```

Provider-specific breakpoints/keys are adapter behavior, not domain semantics.

## Current provider capability observations
As of planning date, OpenAI GPT-5.6+ exposes prompt-cache keys/options, implicit caching plus up to four explicit breakpoints per request, and a current default/minimum TTL of 30 minutes. Gemini 2.5+ provides implicit context caching by default and also supports explicit cached content in generateContent. Hive Plan must detect provider capabilities instead of assuming one universal caching API.

## Cost control
Track actual rather than estimated cost whenever provider usage metadata permits:
- uncached input;
- cached input;
- cache writes where separately billed;
- output/reasoning tokens;
- tool calls;
- retries/failovers;
- total cost per task/increment/project;
- cost per verified merge.

Cost optimization priorities:
1. eliminate unnecessary LLM calls;
2. reduce irrelevant context;
3. maximize safe local/cache reuse;
4. use the cheapest model meeting QualityFloor;
5. escalate only when policy/evidence justifies it.

## Failover
Failover is capability-aware, not merely model-name substitution. A fallback must satisfy required structured output, tools, context, assurance and privacy constraints. If no compatible route exists, BLOCK rather than silently degrading.

Use bounded retries, exponential backoff/jitter where appropriate, idempotency keys for repeatable provider calls and circuit breakers for unhealthy routes.

## Quality protection
Routing changes must not increase:
- critical planning/review misses;
- false APPROVED verdicts;
- correction rounds;
- repeated known failures;
- source-grounding failures.

Savings that degrade these metrics are rejected.

## Future innovations
- Contextual bandit routing trained on verified outcomes, initially shadow-only.
- Per-project model priors that learn which model/profile performs best for specific task classes.
- Cache Value Predictor that decides whether provider cache writes are economically justified based on expected reuse.
- Route Portfolio for high-uncertainty tasks: cheap parallel candidate generation plus one strong adjudicator when measured payoff exceeds cost.
- Quality Debt Ledger that records routes accepted below preferred quality due to outages/budgets and requires later revalidation where policy allows temporary degradation.

## Freeze boundary
Freeze the provider-neutral architecture, quality floors, layered cache/invalidation semantics, failover safety and eval requirements. Exact model names, prices, routing thresholds and vendor-specific cache settings remain configuration refreshed from current provider data and project evals.