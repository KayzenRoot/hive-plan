# HP-PLAN-010 — Project Brain Detailed Layout

Status: PROPOSED

## Mission
Turn project memory, architecture, evidence and history into an explorable engineering map without obscuring authority.

## Desktop zones
- graph/constellation canvas: dominant center;
- Brain Search + mode bar: top of canvas;
- filter/overlay dock: left-inside canvas or collapsible;
- selected entity inspector: right rail;
- historical/authority timeline: bottom expandable lane.

## Default modes
- KNOWLEDGE: canonical docs, decisions, memory and artifacts;
- ARCHITECTURE: runtime/modules/files/symbols/contracts;
- IMPACT: feature/change/test/review relationships;
- EVIDENCE: ProofGraph and evidence heatmap;
- HISTORY: checkpoint/commit evolution;
- FAILURE_MEMORY: prior failures, causes, fixes and prevention tests.

## Spatial composition
Start clustered by bounded semantic domain rather than random force layout. Stable node identity should preserve approximate position between visits where graph topology has not materially changed.

Zoom levels:
1. PROJECT: domains and major systems;
2. DOMAIN: modules/features;
3. COMPONENT: APIs/schemas/files/tests;
4. DETAIL: symbols/evidence/decisions.
Progressive disclosure prevents visual overload.

## Node inspection
Selecting a node opens an inspector with:
- identity/type;
- authority/freshness;
- short summary;
- source path/SHA/version;
- inbound/outbound typed relations;
- decisions/ADRs;
- tests/evidence;
- active WO/review;
- failure memory;
- actions such as open, compare, ask chat, inspect history.

## Evidence mode
Evidence Heatmap can color/pattern the graph while a legend and list show VERIFIED_DIRECT, VERIFIED_DERIVED, PARTIAL, CONFLICTING, UNVERIFIED and STALE. Clicking a weak region explains exactly what proof is missing.

## History mode
Timeline scrubber changes the graph against explicit checkpoint/SHA snapshots. Current and historical states can be split/overlaid for semantic diff. Historical mode uses persistent banner and disables accidental current-state mutation.

## Architecture Lens
Selecting a feature can reveal:
feature -> entrypoints -> files/symbols -> APIs/data -> tests -> Work Orders -> evidence/findings.
Voice can traverse this path.

## Search
Brain Search supports natural language plus exact source/symbol/path lookup. Search results explain why they matched and their authority/freshness. Semantic similarity alone is never displayed as canonical authority.

## 3D treatment
Use depth primarily for hierarchy/relationship separation. Camera motion is bounded and purposeful. Fog/glow/particles cannot hide labels or edge semantics. In EFFICIENT mode reduce to simpler geometry; SAFE_2D uses graph/tree/table equivalents.

## Acceptance direction
A user must be able to answer `why is this decision true?`, `what depends on this?`, `what evidence proves it?`, `what failed here before?` and `how did this change?` from the Brain without reading raw database records.