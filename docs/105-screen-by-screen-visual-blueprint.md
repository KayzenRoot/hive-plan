# HP-PLAN-010 — Screen-by-Screen Visual Blueprint

Status: PROPOSED

## Mission
Define the visual/product composition of the main Hive Plan surfaces before advanced implementation so 3D, glass, motion, charts and engineering truth form one coherent system.

## Global frame
All major screens share:
- CommandHeader: project, global command/voice entry, health, model/quality tier, cost, notifications, graphics profile;
- NavigationRail: Projects, Chat, Brain, Architecture, Agents, Work Orders, Reviews, GitHub, Memory, Skills, Costs, Health, Settings;
- ContextRail: contextual sources, selected artifact, provenance, freshness and active agents;
- TelemetryStrip: delivery, review, cost, RAG/cache, agents, CPU/RAM/GPU and queues;
- VoiceOrb: real listening/transcribing/thinking/speaking state, compact by default;
- ProjectPulse: blockers and important state changes.

## Screen S01 — Project Cockpit
Purpose: answer `what is happening now?`.
Composition:
- hero Hive Core 3D topology;
- project health and current objective;
- active Work Order/review cards;
- HIVE/UADS/UGAS/GitHub system nodes;
- delivery/cost/quality charts;
- blockers and incidents;
- recent decisions/checkpoints.
3D is data-driven and mirrored semantically.

## Screen S02 — Engineering Chat
Purpose: primary conversational workspace.
Composition:
- large rich-response timeline;
- multimodal voice-first composer;
- Context Lens;
- agent council strip;
- rich diagrams/charts/images/artifact cards;
- evidence drawer;
- focus/topic breadcrumb;
- optional compact Hive Core presence.
Long reading surfaces reduce glass and effects automatically.

## Screen S03 — Project Brain
Purpose: explore what the project knows and why.
Composition:
- central Knowledge Constellation / graph;
- canonical source lane;
- verified memory lane;
- failure/success pattern lane;
- DecisionTrail and checkpoint timeline;
- search/retrieval inspector;
- authority/freshness filters;
- selected-node evidence panel.
3D/graph view always has list/tree semantic mirror.

## Screen S04 — Architecture Lens
Purpose: navigate system architecture and impact.
Composition:
- interactive architecture/Feature Impact Graph;
- module/service/data boundaries;
- file/symbol/test links;
- ADR badges;
- risk/ownership overlays;
- predicted versus actual impact;
- architecture drift alerts.
Voice examples: `mostre só o backend`, `quais testes protegem este módulo?`.

## Screen S05 — Agents / Council
Purpose: inspect and govern agent work.
Composition:
- agent roster and capability graph;
- current AgentTaskGraph;
- dependency lanes;
- activity timeline;
- token/cost/latency per task;
- dissent and specialist findings;
- concurrency/resource view;
- UADS execution status.
Avoid humanoid avatars as primary semantics; state and role matter more than decoration.

## Screen S06 — Work Order Studio
Purpose: compile and inspect exact execution contract.
Composition:
- scope/acceptance/STOP panes;
- Context Lock sources;
- MUST_TOUCH / LIKELY_TOUCH / WATCH_ONLY map;
- AgentTaskGraph;
- FailureShield constraints;
- test/evidence obligations;
- CompileGuard status;
- diff between WO revisions;
- authorization gate.

## Screen S07 — Review Command Center
Purpose: make review fast, evidence-first and incisive.
Composition:
- exact PR/base/head snapshot;
- changed-file/Feature Impact map;
- findings by severity/domain;
- diff/code panel;
- CI/tests/static/security evidence;
- ProofGraph;
- blind-spot map;
- specialist disagreement;
- Review Receipt/verdict.
Critical evidence uses solid high-contrast surfaces.

## Screen S08 — GitHub / Delivery
Purpose: visualize source and delivery state.
Composition:
- issues/branches/PRs/releases;
- Work Order identity linkage;
- CI/check status;
- checkpoint and merge history;
- source fingerprint/staleness indicators;
- release readiness.

## Screen S09 — Memory / Retrieval Lab
Purpose: inspect RAG rather than trust it invisibly.
Composition:
- query pipeline;
- candidate chunks;
- lexical/vector/RRF/rerank scores;
- authority/freshness/compatibility;
- selected ContextCapsule;
- negative/failure memory matches;
- retrieval evals and cache metrics.

## Screen S10 — Costs / Performance
Purpose: optimize verified outcome cost.
Composition:
- provider/model routes;
- QualityFloor;
- token/cache cost;
- Rework Tax;
- idea-to-verified-merge time;
- strong-model escalation rate;
- local CPU/RAM/GPU/resource pressure;
- cost anomaly alerts.

## Screen S11 — Health / Diagnostics
Purpose: operational truth.
Composition:
- service dependency topology;
- availability/freshness/authority/latency dimensions;
- incidents and Incident Capsules;
- queue/job state;
- adapter circuit breakers;
- backup/RestoreProof;
- logs/traces with causal IDs.

## Screen S12 — Settings / Studio
Purpose: configure operator experience without mixing preference with truth.
Composition:
- providers/models;
- voice provider and microphone;
- graphics profile;
- motion/accessibility;
- HIVE/UADS/UGAS connections;
- GitHub connection policy;
- local storage/retention;
- privacy/secrets controls;
- visual personalization.

## Responsive behavior
Desktop is primary V1 target. Narrow layouts preserve Chat, critical state, voice, findings and evidence first. Heavy 3D/graphs may move to dedicated full-screen views.

## STOP CONDITION
No screen is implementation-ready until purpose, primary information, authoritative data source, interaction, degraded state, loading/empty/error state, accessibility mirror and performance behavior are explicit.