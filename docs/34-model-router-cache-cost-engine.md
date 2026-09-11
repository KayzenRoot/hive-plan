# Model Router + Cache/Cost Engine

Status: FROZEN — HP-PLAN-005

## Mission
Select the cheapest/fastest execution path that still satisfies the task's quality, risk, privacy and assurance requirements. Cost optimization is subordinate to correctness and review safety.

Quality/assurance tier semantics and Verified Outcome Cost rules are frozen in `docs/35-quality-floor-routing-policy.md`. Routing/cache regression gates are frozen in `docs/36-routing-cache-evals.md`.

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
Applies per-task/project budgets for tokens, money, latency and retry count. Budgets guide routing but never authorize violating QualityFloor. It SHOULD reserve bounded escalation budget where cheap-first routing is allowed.

### ProviderSentinel
Tracks provider/model health, rate limits, timeouts, error rates, cache hit behavior and latency. Supports circuit breakers, backoff and failover to compatible routes.

### RouteLab
Shadow-routing/eval subsystem. Alternative model/cache strategies can be evaluated without silently changing production routing. Expensive shadow calls are sampled rather than duplicated by default.

### CacheValuePredictor
Estimates whether a provider/local cache write is likely to repay its creation/storage cost from expected reuse, TTL, prefix size and route frequency. It is advisory until validated by evals.

## Routing flow
```text
TASK / AGENT REQUEST
      ↓
CAN THIS BE DETERMINISTIC?
      ├─ YES → LOCAL TOOL / CACHE
      ↓ NO
ROUTEGUARD → ASSURANCE PACKET
      ↓
QUALITY FLOOR + PRIVACY + CAPABILITY GATE
      ↓
CACHEFABRIC LOOKUP
      ├─ SAFE HIT → VALIDATE FINGERPRINTS → RETURN
      ↓ MISS
MODEL MESH ELIGIBLE CANDIDATES
      ↓
VERIFIED OUTCOME COST RANKING
      ↓
SELECT ROUTE
      ↓
PROVIDER CACHE-FRIENDLY REQUEST
      ↓
OUTPUT / SOURCE / SCHEMA VALIDATION
      ↓
ESCALATE / ACCEPT / BLOCK
      ↓
TELEMETRY + OUTCOME LEARNING
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
- marginal cost and expected Rework Tax.

## Draft/critic pattern
For selected consequential tasks, separate generation authority from decision authority:
- cheap/fast model may draft or extract;
- stronger or independently routed model critiques when policy requires;
- deterministic evidence remains primary;
- no model self-assertion upgrades assurance.

This avoids paying strong-model cost for every token while preserving strong review on high-impact decisions.

## Cache architecture

### Fingerprint rule
Every reusable cache entry includes dependencies such as:
- project/source root;
- checkpoint/decision fingerprints;
- Git base/head where relevant;
- policy version;
- prompt/template version;
- model/provider profile where output depends on it;
- tool/schema version;
- privacy class where relevant.

A changed critical dependency invalidates the entry deterministically.

### Cache safety classes
- EXACT_SAFE: deterministic output/facts, reusable when fingerprints match.
- SEMANTIC_SAFE: retrieval/rerank result reusable with strict source/query/profile fingerprints.
- ADVISORY: reusable only as input/context, never as canonical answer.
- NO_CACHE: security-sensitive, highly dynamic, non-idempotent or policy-prohibited tasks.

A cached result can never acquire more authority than the original result. Canonical decisions and final review verdicts still require their governed artifacts/fingerprints.

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

## Provider capabilities
Current provider-specific observations are tracked separately in `docs/37-provider-capability-live-notes.md` because model IDs, cache APIs, TTLs and prices are living configuration rather than frozen architecture.

## Cost control
Track actual rather than estimated cost whenever provider usage metadata permits:
- uncached input;
- cached input;
- cache writes/storage where separately billed;
- output/reasoning tokens;
- tool calls;
- retries/failovers;
- total cost per task/increment/project;
- cost per verified merge;
- Rework Tax / Verified Outcome Cost.

Cost optimization priorities:
1. eliminate unnecessary LLM calls;
2. reduce irrelevant context;
3. maximize safe local/cache reuse;
4. use the cheapest eligible route meeting QualityFloor;
5. escalate only when policy/evidence justifies it;
6. optimize total verified outcome, not isolated API-call price.

## Failover
Failover is capability-aware, not merely model-name substitution. A fallback must satisfy required structured output, tools, context, assurance and privacy constraints. If no compatible route exists, BLOCK rather than silently degrading.

Use bounded retries, exponential backoff/jitter where appropriate, idempotency keys for repeatable provider calls and circuit breakers for unhealthy routes.

Provider/model retirement is treated as configuration/eval invalidation, not an architectural migration.

## Quality protection
Routing changes must not increase:
- critical planning/review misses;
- false APPROVED verdicts;
- correction rounds;
- repeated known failures;
- source-grounding failures;
- stale-cache returns.

Savings that degrade these metrics are rejected.

## Quality Debt
If policy allows a temporary route below the preferred (but still minimum-safe) profile during outage/budget events, it creates a traceable Quality Debt record with revalidation rules. HIGH_ASSURANCE cannot use silent degradation; unavailable required assurance means BLOCK.

## Future innovations
- Contextual-bandit routing trained on verified outcomes, initially shadow-only.
- Per-project model priors that learn which model/profile performs best for specific task classes.
- Cache Value Predictor for economically justified cache writes.
- Route Portfolio for high-uncertainty tasks: cheap parallel candidate generation plus one strong adjudicator only when measured payoff exceeds cost.
- Quality Debt Ledger for explicitly permitted degraded routes requiring later revalidation.
- Model retirement watcher that marks affected ModelMesh profiles stale and launches replacement evals.

## Freeze boundary
Frozen: provider-neutral router/cache architecture, QualityFloor dependency, layered cache/invalidation semantics, capability-aware failover, no-silent-degradation rules, cost telemetry and eval requirements. Exact model names, prices, routing thresholds, budgets and vendor-specific cache settings remain configuration refreshed from current provider data and project evals.