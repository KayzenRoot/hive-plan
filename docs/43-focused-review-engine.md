# Focused Senior Review Engine

Status: PROPOSED FOR FREEZE — HP-PLAN-006

## Mission
Review exactly what changed, everything materially affected by that change, and nothing else unless risk/evidence justifies expansion. Optimize for defect detection per unit of time/token while preserving high recall for consequential regressions.

## Core rule
The review unit is not the repository. It is the immutable review snapshot plus the semantic impact closure of the change.

`ReviewScope = ActualDiff ∪ DirectlyImpacted ∪ ContractImpacted ∪ RiskRequired ∪ AcceptanceProof`

Unrelated code is excluded by default.

## Internal components

### ReviewScope Compiler
Builds the exact review surface from:
- base/head diff;
- changed symbols, imports and exports;
- call/dependency graph;
- API/schema/route/config changes;
- Feature Impact Graph;
- Work Order predicted surface;
- acceptance criteria;
- prior failures/regressions;
- risk/assurance policy.

Each candidate file/symbol is classified:
- MUST_REVIEW;
- IMPACT_REVIEW;
- PROOF_ONLY;
- WATCH;
- EXCLUDE.

### DiffLens
Creates a compact semantic diff: changed functions/types/routes/components/config keys/contracts rather than blindly sending complete files to an LLM.

### ImpactClosure
Expands from changed nodes only until the relevant semantic boundary is closed. Expansion reasons are explicit and traceable. Depth is risk-adaptive rather than globally fixed.

### FindingGate
Rejects noisy findings unless they are actionable and evidence-grounded. A publishable finding requires:
- severity;
- affected file/symbol/contract;
- concrete failure condition or violated rule;
- evidence/proof path;
- impact;
- recommended fix or correction criterion;
- confidence source, where relevant.

Style/preferences are not defects unless a frozen policy/DoD requires them.

### SeniorReview Lead
Acts as adjudicator. It does not reread everything by default. It consumes deterministic evidence plus specialist findings, checks missing coverage/contradictions, deduplicates results and decides APPROVED / CORRECTION_REQUIRED / BLOCKED under the Review Receipt policy.

## Review pipeline
```text
IMMUTABLE REVIEW SNAPSHOT
          ↓
DIFF + CHANGED SYMBOLS
          ↓
REVIEW SCOPE COMPILER
          ↓
FEATURE IMPACT GRAPH EXPANSION
          ↓
DETERMINISTIC TOOL FAN-OUT
          ↓
SPECIALIST REVIEW SLICES (only if needed)
          ↓
FINDING GATE + DEDUP
          ↓
SENIOR REVIEW LEAD
          ↓
INDEPENDENT AUDIT when policy requires
          ↓
REVIEW RECEIPT
```

## Fast path
For LOW/STANDARD changes with good deterministic evidence:
1. contract/SHA/context validation;
2. diff/symbol impact closure;
3. targeted lint/type/static/test evidence;
4. one focused reviewer pass;
5. finding gate;
6. verdict.

Do not invoke every specialist for every PR.

## Deep path
Escalate when the change touches auth/security, money/signing, migrations/data integrity, public APIs/contracts, concurrency, recovery, broad dependency hubs, repeated-failure areas, or HIGH_ASSURANCE scope.

Deep path may add security/data/platform/performance/reliability specialist slices plus independent audit.

## Deterministic-first tooling
Prefer machine evidence before semantic review:
- Git diff, changed filenames and SHAs;
- AST/structural diff and symbol graph;
- compiler/typechecker/linter;
- unit/integration/E2E tests selected by TestLens;
- static security rules;
- SARIF-compatible findings normalization;
- CodeQL where supported/available and justified;
- additional static analyzers behind adapters.

GitHub CodeQL can identify errors/vulnerabilities and supports data-flow/path analysis for supported languages. GitHub code scanning can also ingest third-party SARIF, so Hive Plan should normalize static-analysis findings rather than hard-code one scanner.

## Review attention budget
Spend semantic reasoning in this order:
1. violated acceptance criterion;
2. behavioral regression risk;
3. security/data-loss risk;
4. public contract compatibility;
5. error/recovery paths;
6. concurrency/state correctness;
7. performance only where change surface/risk indicates it;
8. maintainability/design only when material to correctness/DoD.

Cosmetic comments are suppressed unless explicitly required.

## Historical intelligence
For every changed/impacted node, query:
- previous defects;
- previous correction deltas;
- hot/fragile modules;
- similar accepted PRs;
- regressions caused by similar changes;
- known test gaps.

Historical similarity is advisory until compatible with current stack/version/context.

## Example: login change
If a Work Order changes login behavior, the scope compiler may expand to:
- login UI/state;
- auth endpoint/handler;
- session/token/cookie code;
- validation and error mapping;
- route guards/middleware;
- user/session persistence only if coupled;
- CSRF/CORS/cookie/security configuration;
- auth contract/API types;
- affected tests and downstream protected-route behavior.

Unrelated billing/search/media code remains excluded.

## Finding severity
- CRITICAL: exploitable/irreversible/systemic failure, data compromise/loss, unsafe privileged action.
- HIGH: production-breaking or major security/integrity regression.
- MEDIUM: real functional/reliability defect with bounded impact.
- LOW: minor correctness/maintainability issue that still violates an explicit requirement/policy.
- INFO: evidence/advisory, never blocks alone.

No APPROVED verdict with unresolved HIGH/CRITICAL findings.

## Noise suppression
- duplicate findings collapse into one root finding with multiple evidence paths;
- pre-existing findings outside the review scope are not attributed to the increment unless the change worsens them;
- speculative concerns without an executable condition/evidence remain internal reviewer notes;
- formatting/style is delegated to deterministic formatters/linters.

## Speed optimizations
- analyze changed symbols before full files;
- reuse RepoPulse/ChangeGraph/TestLens caches;
- parallelize independent deterministic checks;
- parallelize specialist slices only after ReviewScope is frozen;
- pass specialists only their slice + relevant contracts/history;
- cache immutable evidence by head SHA/tool version;
- reuse unchanged specialist evidence on correction rounds where valid;
- correction review is delta-first, not a full replay, while regression gates still cover impacted closure.

## Review completeness
A review is complete only if:
- every MUST_REVIEW node has an evidence/reviewer disposition;
- every acceptance criterion has proof status;
- all required specialist slices completed;
- no critical impact edge is unexplored;
- head/context/evidence fingerprints are still current;
- findings passed FindingGate/dedup;
- required audit completed.

## Innovation candidates

### Semantic Review Closure
Graph-bounded computation of the minimal semantically complete review surface.

### Defect Yield Budget
Measure useful confirmed findings per review second/token and use this to remove low-value review steps without lowering escape-rate gates.

### Regression Echo
When a finding matches a known past defect, automatically surface the previous root cause/test and check whether the old prevention mechanism failed.

### Review Blind-Spot Sentinel
Compare predicted review surface against actual post-merge defects/corrections to learn missing graph edges or weak specialist policies.

## Freeze boundary
Freeze focused semantic review, graph-bounded impact closure, deterministic-first analysis, risk-adaptive depth, FindingGate, SeniorReview Lead, no-noise rules and delta-first correction review. Exact analyzers and numeric expansion thresholds remain benchmark/configuration decisions.