# HP-PLAN-010 — Project Brain Visual + Architecture Lens

Status: PROPOSED

## Project Brain visual metaphor
Use a restrained `Knowledge Constellation`: nodes are real project entities and edges are typed relationships. It must feel spatial and alive without becoming an abstract starfield.

Node families:
- canonical docs / ADRs / checkpoints;
- requirements / acceptance criteria;
- modules / files / symbols / APIs / schemas;
- Work Orders / PRs / reviews / evidence;
- agents / skills;
- verified failure and success patterns;
- external research references.

## Truth encoding
Visual attributes may encode only validated state:
- node size: bounded importance/centrality metric;
- glow/intensity: current activity or focus;
- border/state: authority/freshness;
- edge animation: real recent causal/event flow;
- warning halo: blocker/staleness/conflict;
- muted/ghosted: historical/superseded/derived.
A legend is mandatory.

## Architecture Lens overlays
Toggleable overlays:
- SYSTEM: runtime/module topology;
- CHANGE_IMPACT: predicted/actual affected surface;
- TEST_COVERAGE: tests protecting components;
- DECISIONS: ADR/decision ownership;
- RISK: security/reliability/performance hotspots;
- REVIEW: findings and proof coverage;
- MEMORY: relevant failure/success patterns;
- DELIVERY: current WO/PR/CI state;
- COST: expensive model/tool/resource paths.

## Evidence Heatmap
Evidence coverage is computed from ProofGraph/source mappings, not model confidence. States:
- VERIFIED_DIRECT;
- VERIFIED_DERIVED;
- PARTIAL;
- CONFLICTING;
- UNVERIFIED;
- STALE;
- NOT_APPLICABLE.
The same state is represented by text/icon/pattern as well as color.

## Conversational Time Travel
Historical mode pins repository/checkpoint/time boundary and reconstructs derived views against that boundary. UI changes unmistakably:
- persistent HISTORICAL MODE banner;
- historical SHA/checkpoint/time;
- current-state mutation actions disabled or require explicit exit;
- historical answers cite historical sources;
- comparison with current state is an explicit operation.

## Selection behavior
Selecting any node opens:
1. identity and type;
2. canonical/derived authority;
3. freshness;
4. linked decisions;
5. implementation files/symbols;
6. tests/evidence;
7. related Work Orders/reviews;
8. known failures;
9. conversational actions.

## Voice navigation
Bounded commands include `abra este módulo`, `mostre dependências`, `volte um nível`, `compare com o checkpoint anterior`, `mostre riscos`, `quais testes cobrem isso?` and `explique este caminho`.

## Scale/performance
Use progressive disclosure, graph clustering, viewport culling, LOD and server/worker-side graph preparation. Never render the entire repository as thousands of animated nodes by default.

## Semantic mirror
Every graph state can be represented as searchable/filterable tree/table/path lists. Graph layout is a view, not canonical state.

## STOP CONDITION
Freeze only when node/edge semantics, overlays, evidence heatmap, historical mode, selection model, semantic mirror and scale strategy are testable.