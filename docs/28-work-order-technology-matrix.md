# Work Order Compiler Technology Adoption Matrix

Status: FROZEN POLICY — HP-PLAN-004

## Rule
No technology is adopted because it is fashionable. It must improve a measured Hive Plan objective and remain replaceable behind an interface where practical.

## Current candidates

| Technology / approach | Role | Initial status | Why | Adoption gate |
|---|---|---|---|---|
| Git native commands/APIs | deterministic repository truth | ADOPT | authoritative, fast, zero LLM cost | correctness tests |
| Microsoft tgrep | hot lexical/regex repository search | TRIAL | persistent trigram index, file watching, strong fit for repeated large-repo queries | beat fallback search on representative large repos without unacceptable RAM/index cost |
| ast-grep | structural AST search, outline, rules | TRIAL → ADOPT candidate | syntax-aware search/rewrite, polyglot Tree-sitter base, useful for agent-oriented outlines | language coverage + latency + correctness benchmark |
| Tree-sitter-compatible parsing | syntax/symbol foundation | ADOPT AS INTERFACE | mature incremental syntax ecosystem; may be consumed through ast-grep or direct adapter | parser compatibility benchmark |
| ripgrep / simple file scan | lexical fallback / small repos | ADOPT FALLBACK | near-zero setup and excellent small-repo behavior | remain fastest/simple under configured threshold |
| local lexical + vector hybrid RAG | semantic/source retrieval | ADOPT ARCHITECTURE | exact + semantic recall, avoids semantic-only misses | retrieval evals |
| local reranker | top-context quality | TRIAL | can reduce irrelevant context before expensive model calls | measurable precision gain per latency/cost |
| content-addressed caches | reuse/invalidation | ADOPT | Git/blob hashes provide natural incremental identity | deterministic invalidation tests |
| symbol/dependency graph | impact/context expansion | ADOPT ARCHITECTURE | supports change surface, tests and dependency neighborhoods | graph correctness/coverage eval |
| coverage/history-based test impact | TestLens | TRIAL | potential CI speed gain without blind test reduction | false-negative regression budget |
| provider prompt caching | stable instruction/source prefix | ADOPT WHEN SUPPORTED | lowers repeated-provider input cost/latency | provider adapter telemetry |
| binary internal transport (CBOR/MessagePack) | future high-throughput internal path | WATCH | unnecessary for local V1 until JSON becomes measured bottleneck | benchmark evidence |
| local open-weight embedding/reranking | optional private retrieval | TRIAL | privacy/cost benefits and local-first fit | hardware-adaptive benchmark |

## tgrep policy
Use an adaptive search backend rather than always-on tgrep.

Suggested decision rule to benchmark:
- small/rarely queried repository → simple fallback search;
- large or repeatedly queried repository → persistent indexed backend;
- backend is hidden behind `LexicalSearchProvider`.

Hive Plan should collect repository file count/bytes, query frequency, index build/update cost, memory and p50/p95 query latency and choose the backend from evidence.

## ast-grep / syntax policy
Use a `StructuralSearchProvider` abstraction. ast-grep is the leading V1 candidate for:
- syntax-aware matching;
- compact source outlines;
- custom architecture/lint patterns;
- symbol/location extraction where reliable;
- safe structural queries that outperform text matching.

Do not force AST parsing on file types/languages with weak grammar support. Fall back to lexical/semantic routes and record reduced confidence.

## Retrieval architecture
Recommended retrieval uses multiple independent signals rather than a single vector search:
```text
EXACT PATH/SYMBOL
      +
LEXICAL SEARCH
      +
AST / STRUCTURAL
      +
DEPENDENCY GRAPH
      +
SEMANTIC VECTOR
      +
CANONICAL/MEMORY SOURCES
      ↓
AUTHORITY + FRESHNESS FILTER
      ↓
FUSION / RERANK
      ↓
CONTEXT BUDGET
```

## Innovation candidates

### Query Portfolio
Instead of one semantic query, compile a tiny portfolio of deterministic and semantic retrieval intents: exact symbols, architecture concept, failure pattern and test neighborhood. Run independent retrieval routes in parallel locally, then fuse results.

### Context Entropy Guard
Detect whether added context contributes new decision-relevant information. Near-duplicate/low-novelty chunks are rejected from the ContextCapsule even if semantically similar.

### Change Surface Feedback Loop
After merge, compare predicted touched files/symbols/tests against actual execution. Feed errors back into ChangeGraph/TestLens scoring and project-specific priors.

### Failure Vaccine
When a validated failure pattern recurs, automatically generate a targeted constraint/test candidate. It becomes mandatory only after policy/compatibility checks; this turns repeated defects into accumulating defenses.

### Spec-to-Test Trace Compiler
Compile each acceptance criterion to one or more expected proof channels (unit/integration/E2E/static/security/benchmark/manual evidence). Work Orders cannot leave an acceptance criterion without a proof strategy unless explicitly waived.

### Context Diff Protocol
Correction rounds transmit only source/evidence/context changes since the previous Work Order/Correction Delta. Stable sections remain referenced by digest, maximizing local/provider cache reuse.

### Repository Temperature Map
Track frequently changing/high-defect/high-risk modules. Change-surface and review depth can be increased for hot/risky areas and reduced for stable, low-risk areas only when evidence supports it.

## Benchmark set before implementation freeze
Measure candidate stacks on at least:
- small repository;
- medium application;
- large/monorepo-style fixture;
- mixed-language fixture.

Metrics:
- cold index/build time;
- incremental update time;
- RAM/disk;
- exact-search latency;
- structural-search latency;
- retrieval precision/recall on known tasks;
- relevant-context ratio;
- context bytes/tokens;
- Work Order compilation latency;
- predicted change-surface precision/recall;
- test-impact false-negative rate;
- downstream Codex correction rounds;
- total time/cost to verified merge.

## Selection principle
Prefer the simplest stack that meets the quality/performance gates. Advanced indexing is enabled where measured workload justifies it rather than becoming mandatory complexity for every project.

## Freeze boundary
The adoption policy, provider abstractions, benchmark gates and statuses above are frozen. Exact backend promotion thresholds remain empirical configuration determined by benchmarks and may change without altering core workflow semantics.