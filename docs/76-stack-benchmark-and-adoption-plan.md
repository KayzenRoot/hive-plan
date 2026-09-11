# Stack Benchmark & Adoption Plan

Status: PROPOSED FOR FREEZE — HP-PLAN-008

## Goal
Technology is promoted by verified outcome, not novelty or popularity.

## Benchmark dimensions
Every candidate receives scores for:
- runtime latency/throughput;
- cold/warm startup;
- dev build/HMR speed;
- memory/CPU/GPU cost;
- implementation complexity;
- local Windows + Docker compatibility;
- type safety/contracts;
- testing/tooling quality;
- security history/update cadence;
- observability;
- failure/recovery behavior;
- maintenance burden;
- portability/lock-in;
- agent/Codex friendliness;
- total Verified Outcome Cost.

## Frontend experiments
### FE-01 Build system
React 19.3 + Vite 8.1/Rolldown baseline.
Compare only if evidence requires alternative.

Measure:
- clean startup;
- HMR;
- full build;
- bundle chunks;
- memory during development;
- source map/debug quality.

### FE-02 Component primitives
Base UI vs Radix candidate slice.
Measure:
- accessibility;
- bundle impact;
- styling freedom;
- popup/focus correctness;
- implementation speed;
- test reliability.

### FE-03 Charts
ECharts vs uPlot/lightweight canvas for high-frequency time-series.
Measure:
- 1k/10k/100k points;
- pan/zoom latency;
- update frequency;
- memory;
- visual capability;
- accessibility/fallback.

### FE-04 3D
Three.js WebGPURenderer + React Three Fiber.
Profiles:
- WebGPU;
- WebGL2 fallback;
- cinematic/balanced/efficient.

Measure:
- FPS/frame time;
- GPU memory proxy metrics;
- CPU main-thread utilization;
- scene startup;
- resize/navigation stutter;
- concurrent chat streaming;
- concurrent local AI/GPU pressure.

## Backend experiments
### BE-01 Fastify baseline
Measure REST, SSE, schema validation, concurrent local clients and event fan-out.

### BE-02 Runtime
Node 24 LTS is baseline. Node 26 may run shadow benchmarks but cannot become production baseline merely because it is newer.

### BE-03 Durable work
Compare:
- explicit Postgres outbox + worker;
- pg-boss.

Scenarios:
- 1/10/100 concurrent Work Orders;
- retries;
- singleton/review leases;
- dependencies;
- crash/restart;
- 10k queued events/jobs;
- duplicate delivery;
- PostgreSQL maintenance stress.

## Retrieval experiments
Compare retrieval stacks:
1. lexical only;
2. lexical + AST;
3. lexical + AST + pgvector;
4. full hybrid + reranker;
5. full hybrid + Feature Impact Graph.

Use real questions from Hive Plan projects and measure:
- recall of required files/symbols;
- irrelevant context ratio;
- token budget;
- first-pass Codex success;
- review findings;
- latency.

## PostgreSQL/vector experiments
PostgreSQL 18 + pgvector baseline.
Evaluate:
- no ANN/exact;
- HNSW;
- IVFFlat where appropriate;
- filtering/selectivity;
- incremental updates;
- vacuum/maintenance;
- backup/restore;
- memory footprint.

Dedicated vector DB enters TRIAL only if pgvector misses explicit thresholds.

## Visual quality gate
Performance cannot be optimized by silently making the UI visually poor.

Create golden cockpit scenes and compare:
- screenshot visual regression;
- animation timing;
- typography/layout consistency;
- glass material quality;
- 3D fidelity by graphics tier.

## Accessibility gate
No technology is promoted if it materially breaks:
- keyboard navigation;
- focus order;
- screen-reader semantics for critical operations;
- contrast;
- reduced motion.

## Agent friendliness gate
Because Codex/UADS will build much of the system, record:
- documentation quality;
- type errors caught early;
- frequency of agent-generated incorrect patterns;
- availability of machine-readable/current docs;
- test/debug feedback quality.

## Adoption lifecycle
`WATCH → TRIAL → ADOPT` or `REJECT`.

Promotion requires benchmark evidence stored in the repository/evidence system. A dependency may be demoted when vulnerabilities, maintenance decline, regressions or better alternatives change Verified Outcome Cost.

## Initial recommendations
ADOPT after smoke benchmark:
- React 19.3;
- Vite 8.1;
- TypeScript strict;
- Node 24 LTS;
- Fastify;
- PostgreSQL 18;
- TanStack Router/Query;
- JSON Schema/AJV.

TRIAL:
- Base UI;
- Three.js WebGPU/R3F;
- ECharts;
- pgvector 0.8.6+;
- pg-boss;
- Tailwind 4.3 custom design layer.

Benchmark-gated optional:
- Redis;
- tgrep;
- dedicated vector DB;
- WebSocket transport;
- advanced post-processing/3D effects.
