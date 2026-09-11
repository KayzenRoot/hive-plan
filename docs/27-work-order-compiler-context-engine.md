# Work Order Compiler & Context Optimization Engine

Status: FROZEN — HP-PLAN-004

## Mission
Compile approved planning into the smallest, freshest, highest-authority execution package that gives an executor enough information to implement correctly without wandering through the repository or receiving irrelevant history.

The Work Order Compiler is not a prompt writer. It is a multi-pass engineering compiler with deterministic analysis first and semantic reasoning only where deterministic evidence is insufficient.

## Quality target
Optimize simultaneously for:
- implementation correctness;
- lowest correction rounds;
- shortest idea-to-verified-merge cycle;
- smallest useful context;
- low LLM/token cost;
- reproducible compilation;
- stale-context prevention;
- reuse of proven patterns and negative knowledge;
- executor/model portability.

## Internal technologies / components
These are Hive Plan internal subsystem names, not external dependencies.

### RepoPulse
Incremental multi-index of repository truth. Maintains Git/blob identity, file metadata, lexical index, syntax outline, symbols, dependency edges and optional semantic embeddings. Unchanged blobs are never reparsed/re-embedded unnecessarily.

### ChangeGraph
Impact graph connecting requirements, ADRs, modules, files, symbols, APIs, data models, migrations, tests and historical PRs. Used to predict change surface and blast radius.

### FailureShield
Negative-knowledge preflight. Retrieves matching prior failures/root causes/corrections and injects only relevant recurrence-prevention constraints or tests into the Work Order.

### TestLens
Test-impact mapper. Selects the smallest safe test set from static dependency paths, file/test conventions, coverage when available, historical PR/test associations and explicit acceptance criteria. High-risk paths still receive broader regression gates.

### ContextCapsule
Content-addressed execution context package. Contains references/fingerprints plus only the snippets/summaries the executor actually needs. Stable content and dynamic content remain separable for caching.

### ExecutorFit
Capability profile/adaptation layer. The canonical Work Order remains executor-neutral; rendering adapts it to Codex or future executors without altering requirements or acceptance semantics.

### CompileGuard
Compile-time quality gate that rejects ambiguous, contradictory, stale, untestable or unverifiable Work Orders before they reach an executor.

## Compiler pipeline
```text
APPROVED PLANNING / INCREMENT
          ↓
0. SOURCE RESOLVE
          ↓
1. REPOSITORY DISCOVERY
          ↓
2. TEXT + STRUCTURAL SEARCH
          ↓
3. SYMBOL / DEPENDENCY GRAPH
          ↓
4. CHANGE-SURFACE PREDICTION
          ↓
5. HYBRID RAG FUSION
          ↓
6. FAILURESHIELD PREFLIGHT
          ↓
7. TESTLENS IMPACT PLAN
          ↓
8. CONTEXT BUDGET + DEDUP
          ↓
9. CONTEXT LOCK / FINGERPRINT
          ↓
10. WORK ORDER IR
          ↓
11. EXECUTORFIT RENDER
          ↓
12. COMPILEGUARD
          ↓
SIGNED/IDENTIFIED WORK ORDER
```

## Pass 0 — Source Resolve
Resolve canonical project truth before repository search:
Checkpoint → Decisions/ADRs → Scope → DoD → Architecture → Requirements/contracts → active issue/increment.

No LLM is used to rediscover facts deterministically present in these sources.

## Pass 1 — Repository Discovery
Use Git-native facts first:
- current base SHA;
- tracked files;
- manifests/lockfiles;
- languages/frameworks;
- package/workspace boundaries;
- build/test/lint commands;
- generated/vendor exclusions;
- code owners/policy files when present.

Discovery results are cached by repository/tree/blob fingerprints.

## Pass 2 — Search cascade
Use the cheapest exact mechanism that can answer the query:
1. exact path/symbol metadata;
2. indexed lexical/regex search;
3. AST/structural search;
4. symbol/dependency traversal;
5. semantic RAG;
6. LLM inference only for remaining ambiguity.

Text and semantic retrieval are complementary. Semantic search never replaces exact symbol/AST/Git evidence where exact evidence exists.

## Pass 3 — Repository outline and symbol graph
Produce compact syntax-aware outlines containing classes/functions/types/routes/components/configuration boundaries rather than sending full source files. Build import/export and dependency relationships when reliably extractable.

The graph is incremental and content-addressed: a changed blob invalidates only dependent nodes/index entries where practical.

## Pass 4 — Change-surface prediction
Predict:
- MUST_TOUCH files/symbols;
- LIKELY_TOUCH files/symbols;
- WATCH_ONLY dependencies;
- expected contracts/API/data impact;
- expected tests;
- blast-radius/risk class.

Predictions are guidance, not permission. The executor may discover additional necessary files but must report deviations in the Completion Manifest.

## Pass 5 — Hybrid retrieval fusion
Retrieve from:
- canonical project sources;
- lexical code search;
- structural/AST search;
- symbol/dependency graph;
- local semantic embeddings;
- execution/history memory;
- validated engineering patterns;
- failure/negative knowledge.

Rank with at least:
- authority;
- exactness/semantic relevance;
- project locality;
- freshness;
- validation strength;
- technology/environment compatibility;
- dependency distance;
- supersession state.

Fusion/reranking algorithm remains benchmarkable and replaceable. Reciprocal-rank-style fusion is a candidate, not a hard dependency.

## Pass 6 — FailureShield
Before Work Order finalization, search previous failures by subsystem, dependency/provider, stack/version, error signature, migration type, architecture pattern, security boundary and performance pattern.

Only high-relevance, compatible failure knowledge becomes a constraint/test. Raw old failures must not pollute every Work Order.

## Pass 7 — TestLens
Compile tests from acceptance criteria and impacted code. Sources may include:
- static dependency links;
- explicit test mappings;
- naming/path conventions;
- coverage data;
- previous PRs that changed the same symbols/files;
- prior regressions;
- security/performance/migration proof obligations.

Never reduce HIGH_ASSURANCE testing solely for speed.

## Pass 8 — Context Budgeter
Every context item receives a class:
- REQUIRED;
- HIGH_VALUE;
- SUPPORTING;
- OMIT.

Budget by task/risk rather than filling the model context window. Prefer symbol-level snippets, structured facts and artifact references over whole documents/files.

Rules:
- deduplicate equivalent facts;
- collapse repeated history;
- preserve source/provenance IDs;
- prefer current canonical versions;
- include only relevant failure patterns;
- use summaries only when the underlying source remains referenceable;
- never truncate acceptance criteria or safety obligations for token savings.

## Content-addressed incremental caches
Cache layers are keyed by canonical identity/fingerprints:
- file metadata by Git blob SHA;
- AST/outline by blob SHA + parser version;
- embeddings by blob/chunk SHA + embedding profile;
- lexical index incrementally updated by changed files;
- symbol graph by source fingerprints;
- retrieval results by query intent + source root;
- compiled ContextCapsule by increment/task + context root;
- executor rendering by Work Order digest + executor profile;
- provider stable-prefix cache when supported.

Critical source changes invalidate dependent artifacts; unchanged blobs should be reused aggressively.

## Work Order Intermediate Representation (WO-IR)
Before rendering a prompt, compile a normalized internal representation containing:
- objective;
- canonical source references;
- context root;
- scope/out-of-scope;
- constraints;
- requirements/architecture rules;
- predicted change surface with confidence;
- relevant prior failures;
- acceptance criteria;
- TestLens plan;
- deliverables/evidence obligations;
- risk/assurance class;
- stop condition;
- unresolved but non-blocking uncertainties.

The canonical JSON Work Order is generated from WO-IR. Human/PDF/Codex renderings are views, not separate truth.

## ExecutorFit
Executor profiles describe capabilities such as:
- repository/tool access;
- terminal/test ability;
- context limits;
- structured-output ability;
- patch/commit/PR capability;
- available UADS/Hades policies;
- supported artifact contracts.

ExecutorFit may change formatting/tool instructions but MUST NOT change objective, scope, acceptance criteria, risk or evidence obligations.

## Correction optimization
For correction rounds:
- reuse unchanged Context Lock/source fingerprints;
- generate Correction Delta instead of full Work Order;
- send only failed criteria/findings, changed evidence and relevant surrounding context;
- invalidate/recompile only impacted ContextCapsule slices.

## CompileGuard
Before release to Codex, reject Work Orders with:
- stale context/base;
- missing canonical source;
- contradictory requirements;
- untestable acceptance criteria;
- unsupported schema/executor profile;
- missing HIGH_ASSURANCE proof obligation;
- nonexistent file/symbol presented as an existing fact;
- unresolved critical assumption;
- secret/sensitive content leakage;
- scope larger than the governed increment;
- context budget dominated by low-authority/redundant material.

## Model routing inside compilation
Most passes are deterministic/local. LLM use is restricted to semantic tasks such as ambiguity resolution, requirement synthesis, difficult change-surface reasoning and final compile critique.

Suggested profiles:
- FAST_CHEAP: extraction/classification/query expansion;
- BALANCED: requirements/context synthesis;
- STRONG: consequential architecture/cross-domain reasoning;
- HIGH_ASSURANCE: configured critical domains/independent critique.

Escalation is policy-driven and measured by evals rather than model prestige.

## Pre-compilation warming
Once an increment approaches planning freeze, Hive Plan may asynchronously prepare local repo indexes, likely dependency neighborhoods and safe retrieval caches. No Work Order becomes executable until freeze/gates pass, but deterministic preparation can reduce interactive latency later.

## Observability
Track per Work Order:
- compilation latency by pass;
- repo-index hit/miss;
- files parsed/reused;
- retrieval candidates vs selected context;
- context tokens/bytes before and after compaction;
- provider cached-token ratio when available;
- predicted vs actual changed files/symbols;
- predicted vs actually needed tests;
- executor exploration/wandering indicators;
- correction rounds;
- repeated failure prevented;
- total time/cost to verified merge.

## Freeze boundary
The architecture above is FROZEN. Specific third-party search, parser, embedding, reranking and indexing backends remain replaceable behind providers and are promoted only by benchmark/eval evidence. No tool name is part of canonical execution semantics.

## Core principle
The best Work Order is not the longest or most detailed. It is the smallest deterministic execution contract that contains every fact, constraint and proof obligation needed for the executor to succeed on the first safe attempt.