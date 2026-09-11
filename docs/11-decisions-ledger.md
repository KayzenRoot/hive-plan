# Decisions Ledger

Only approved decisions are recorded as canonical. Superseding a frozen decision requires a new entry that references the old one and explains impact.

## D-001 — Product identity
**Decision:** Project name is Hive Plan; part of the Hive Project ecosystem.  
**Status:** FROZEN.

## D-002 — V1 deployment model
**Decision:** Local-first, single-user, Docker/Compose.  
**Status:** FROZEN.

## D-003 — Canonical truth
**Decision:** GitHub is the canonical source of approved project truth; chat/model memory is non-canonical.  
**Status:** FROZEN.

## D-004 — Executor boundary
**Decision:** Codex remains the external implementation executor in V1; Hive Plan owns planning, governance, Work Orders, observation, review, audit, and continuity.  
**Status:** FROZEN.

## D-005 — Memory/RAG
**Decision:** Hive V1 is the preferred MemoryProvider, with embedded local RAG fallback behind an interface.  
**Status:** FROZEN.

## D-006 — LLM economics
**Decision:** Cheap/fast model profiles are default; stronger models are escalated by risk/complexity/assurance. Cache/RAG/delta-context optimization is mandatory.  
**Status:** FROZEN.

## D-007 — GitHub authentication
**Decision:** V1 uses local token/PAT-based GitHub integration suitable for one internal operator.  
**Status:** FROZEN.

## D-008 — Automatic review
**Decision:** Executor completion manifests trigger observation; they are never accepted as evidence. Eligible reviews start automatically after current head/CI conditions are met.  
**Status:** FROZEN.

## D-009 — Professional agent organization
**Decision:** Planning/review operates through specialized professional roles with independent critique/audit for consequential decisions.  
**Status:** FROZEN.

## D-010 — UI direction
**Decision:** V1 provides a dark, highly technological command cockpit with real-time/near-real-time project, agent, GitHub, review, health, token/cost, and progress telemetry. Frontend vertical slice is prioritized early in implementation.  
**Status:** FROZEN.

## D-011 — Context-first interviewing
**Decision:** The Interviewer must inspect canonical/project/tool context before asking questions and must not repeat deterministically known or already approved facts. Question rounds are adaptive and short, prioritized by decision impact, uncertainty, irreversibility, risk, and dependency reach.  
**Status:** FROZEN.

## D-012 — Planning confidence and explicit assumptions
**Decision:** Hive Plan maintains a domain Planning Confidence Map backed by evidence/unknowns plus an explicit Assumption Register. Model self-confidence alone is never accepted as planning evidence; critical assumptions must be resolved before freeze.  
**Status:** FROZEN.

## D-013 — Decision pressure testing
**Decision:** Consequential decisions undergo pressure testing for failure modes, alternatives, reversibility, scale, dependency loss, adversarial input, data recovery, observability, security boundaries, and simpler alternatives. Elevated/high-assurance decisions require independent critique.  
**Status:** FROZEN.

## D-014 — Discovery stop condition
**Decision:** Discovery stops when the current decision/increment is sufficiently specified: no unresolved critical unknowns, high-risk unknowns are resolved or explicitly mitigated, blocking contradictions are cleared, required specialists have responded, success criteria are testable, and remaining unknowns are documented as non-blocking.  
**Status:** FROZEN.

## D-015 — Agent authority model
**Decision:** Agents have governed authority levels (observe, propose, review, authorize under policy, operator). Material canonical changes cannot be silently promoted by one agent. Scope expansion, destructive/irreversible operations, policy exceptions, and contested high-impact decisions require operator authority.  
**Status:** FROZEN.

## D-016 — Innovation governance
**Decision:** Innovation Scout suggestions are always classified NECESSARY, IMPORTANT, FUTURE, or OUT OF SCOPE and include benefit, maturity, implementation/operational cost, risk, lock-in, reversibility, evidence, and an ADOPT/TRIAL/WATCH/REJECT recommendation. Suggestions never silently expand active scope.  
**Status:** FROZEN.

## D-017 — Operational learning memory
**Decision:** RAG/memory must preserve not only canonical decisions but also verified execution facts, successful engineering patterns, failure/negative knowledge, root causes, corrections, and validation evidence. Every consequential retrieved memory retains provenance, authority, validation and supersession metadata; semantic similarity alone never makes a memory authoritative. Prior matching failures are checked before finalizing Work Orders so recurrence-prevention constraints/tests can be injected when relevant.  
**Status:** FROZEN.

## D-018 — Verified-throughput delivery flow
**Decision:** The governed delivery unit uses a stable increment/Work Order ID across issue, Context Lock, branch, Work Order, execution manifest, PR, evidence, Correction Deltas, review receipt, checkpoint and lessons. Review is layered deterministic-first, then cheap-model triage, domain specialists, and strong-model audit only when justified. Corrections stay in the same increment/PR when safe. Speed is measured primarily as total `idea → verified merge` time and rework/escaped-defect reduction, not raw code-generation throughput.  
**Status:** FROZEN.

## D-019 — GitHub governance and release lifecycle
**Decision:** Hive Plan uses short-lived increment branches off `main`, governed planning and implementation PRs, issue/milestone objects with stable identities, explicit freeze/unfreeze semantics, SemVer-compatible versioning, immutable release tags, evidence-based patch/hotfix flows, SHA-based canonical promotion, deterministic repository-health signals, public-repository secret/sensitive-data gates, and automatic low-risk GitHub stewardship. Long-lived GitFlow-style branches are avoided by default; `release/*` is used only when evidence shows release preparation requires it.  
**Status:** FROZEN.

## D-020 — Deterministic artifact contracts
**Decision:** Core Hive Plan workflow artifacts use versioned canonical JSON contracts validated with JSON Schema Draft 2020-12 before LLM reasoning. Canonical identities use JCS-compatible canonicalization plus SHA-256; governed reviews bind to exact Git head, context root and evidence root. Completion manifests are triggers/claims only, while Evidence Bundles provide verified facts and Checkpoint Deltas govern canonical promotion. Unsupported major contract versions are blocked rather than guessed, and executor/provider-specific data is isolated in namespaced extensions.  
**Status:** FROZEN.

## D-021 — Work Order Compiler architecture
**Decision:** Work Order generation is a deterministic-first, multi-pass compiler rather than prose generation. The frozen architecture includes canonical source resolution, incremental content-addressed repository indexing, exact/lexical/AST/symbol/dependency/semantic retrieval, ChangeGraph impact prediction, FailureShield negative-knowledge preflight, TestLens proof planning, risk-adaptive ContextCapsules, WO-IR, ExecutorFit rendering and CompileGuard. Specific third-party search/parser/embedding/reranking backends remain replaceable behind provider interfaces and are promoted only by benchmark/eval evidence. Compiler quality is governed by downstream verified outcomes such as first-pass success, correction rounds, context cost, defects and total idea-to-verified-merge time.  
**Status:** FROZEN.

## D-022 — QualityFloor and verified-outcome routing
**Decision:** Model routing uses provider-neutral tiers T0 DETERMINISTIC, T1 FAST_CHEAP, T2 BALANCED, T3 STRONG and T4 HIGH_ASSURANCE. Hard quality/capability/privacy/health eligibility is applied before price or latency optimization. The router optimizes expected Verified Outcome Cost rather than single-call API price, including measured Rework Tax, retry/latency/defect/human-intervention cost. HIGH_ASSURANCE cannot silently degrade; if no eligible route exists the workflow blocks. Temporary degradation where explicitly permitted creates traceable Quality Debt. Model self-confidence never upgrades assurance; acceptance/escalation is evidence-driven.  
**Status:** FROZEN.

## D-023 — Provider-neutral Model Router and CacheFabric
**Decision:** Hive Plan uses a provider-neutral ModelMesh with RouteGuard, QualityFloor, CacheFabric, BudgetPilot, ProviderSentinel and RouteLab. Cache layers are fingerprint-bound and cannot acquire more authority than their source. Provider prompt/context caches are exploited through adapters while domain semantics remain vendor-independent. Failover is capability/privacy/assurance aware; incompatible fallbacks block instead of silently degrading. Routing/cache policies are promoted only through quality, stale-cache, failure and Verified Outcome Cost evals.  
**Status:** FROZEN.

## D-024 — Event Spine and immutable auto-review snapshots
**Decision:** Local V1 observes GitHub through efficient authenticated conditional polling by default, with optional webhook/tunnel adapters feeding the same normalized durable EventSpine. Event processing is at-least-once with deterministic deduplication, idempotent handlers, ReviewLease and EffectLedger for exactly-once-effect behavior where practical. Auto-review eligibility requires complete evidence; reviews are pinned to exact base/head SHA, context root and evidence root through SnapshotGuard/ReviewMVCC and are cancelled as stale when those identities change. Completion claims are signals only, never evidence.  
**Status:** FROZEN.

## D-025 — Focused senior review, Feature Impact Graph and conditional UADS specialists
**Decision:** Review scope is the actual diff plus its risk-governed semantic impact closure, not the whole repository. Hive Plan maintains a provenance-backed Feature Impact Graph mapping features/requirements to files, symbols, contracts, data, tests, runtime components and historical failures, updated from predicted and verified outcomes. Deterministic tools run first; UADS specialist agents are conditionally spawned with non-overlapping scope only for affected risk domains; a STRONG Senior Review Lead adjudicates normalized evidence-grounded findings. Review comments without actionable failure conditions/evidence are suppressed, and correction reviews are delta-first while preserving impacted regression coverage.  
**Status:** FROZEN.

## D-026 — Governed Agent OS and AgentTaskGraph
**Decision:** Hive Plan uses TeamComposer, Capability Ledger, ExpertiseGraph, CouncilBus, Dissent Ledger, AgentGovernor and an executor-neutral AgentTaskGraph with explicit dependencies, read/write/watch sets, ContextCapsules, proof obligations and STOP conditions. Multi-agent execution is used only when verified value exceeds coordination cost; executors may not invent canonical roles or silently change project semantics. ADR-026.  
**Status:** FROZEN.

## D-027 — Skill Fabric, ResearchRadar and open interoperability
**Decision:** Reusable agent procedures are governed through SkillCatalog/SkillForge/SkillResolver/SkillFitness; current technology/OSS research uses ResearchRadar and evidence-based ADOPT/TRIAL/WATCH/REJECT lifecycle. External research is untrusted evidence, never instruction authority. MCP/A2A-compatible adapters may be used without becoming canonical vendor dependencies. ADR-027.  
**Status:** FROZEN.

## D-028 — HIVE/UGAS/UADS principal ecosystem specialists
**Decision:** Extend the canonical agent catalog with A-031 Principal HIVE Systems Specialist, A-032 Principal UGAS Production Systems Specialist and A-033 Principal UADS Orchestration Specialist. HIVE owns context/memory intelligence, UADS owns engineering orchestration, UGAS owns multimodal production and Hive Plan retains planning/governance/review authority. ADR-028.  
**Status:** FROZEN.

## D-029 — V1 application runtime and cockpit stack
**Decision:** V1 uses React 19.3+ strict TypeScript, Vite/Rolldown, TanStack Router/Query, project-owned projection state, Tailwind 4 infrastructure, Motion, optional R3F/Three WebGPU with WebGL2 + VisualTruthMirror fallback; backend uses Node.js 24 LTS, Fastify, modular monolith + bounded workers, REST/snapshots + SSE, pnpm and Docker Compose. Replaceable UI/chart/runtime detail remains benchmark-bound. ADR-029.  
**Status:** FROZEN.

## D-030 — PostgreSQL-first persistence and recovery
**Decision:** PostgreSQL 18 is the canonical transactional datastore; pgvector is the default V1 vector extension behind an adapter; durable PostgreSQL-backed jobs/outbox are preferred; Redis is optional/non-canonical; large immutable artifacts use a local content-addressed store with PostgreSQL metadata; recovery requires paired backup metadata and RestoreProof. ADR-030.  
**Status:** FROZEN.

## D-031 — First cockpit vertical slice readiness boundary
**Decision:** HP-WO-0001 is frontend-first but end-to-end: one persisted cockpit, truthful availability/freshness states, snapshot+SSE watermark projections, PostgreSQL state, optional Hive Core with VisualTruthMirror, read-only HIVE/UADS/UGAS seams, and accessibility/reconnect/recovery/performance/security evidence. It may not pull full RAG, full agent runtime, mandatory Redis, microservices or external ecosystem mutations into the slice. ADR-031.  
**Status:** FROZEN.

## D-032 — Project Brain authority and MemoryProvider
**Decision:** Project Brain is the governed context substrate behind Engineering Chat. Retrieval rank never overrides source authority; HIVE is the preferred MemoryProvider with embedded local fallback; conversation context is non-canonical; verified failure/success memory remains provenance/compatibility bound; canonical changes pass through the Artifact Promotion Gate. ADR-032.  
**Status:** FROZEN.

## D-033 — Voice-first governed Engineering Chat
**Decision:** Engineering Chat is a voice-first, multimodal, source-grounded workspace using provider-neutral voice adapters and typed fallback. Natural-language actions resolve into governed typed ActionPlans; high-impact actions retain authority/confirmation requirements regardless of voice confidence; rich responses use validated semantic blocks and canonical artifact promotion remains governed. ADR-033.  
**Status:** FROZEN.

## D-034 — Multi-workstream checkpoint and zero-friction resume
**Decision:** Project continuity uses a workstream-aware checkpoint index, immutable checkpoint history and digest-bound pointers. Resume phrases verify project/workstream/checkpoint/SHA/digest against GitHub and reconcile newer state before continuing; consequential ambiguity fails closed. Parallel sessions cannot silently overwrite continuity state. ADR-034.  
**Status:** FROZEN.

## D-035 — Governed Implementation Blueprint and bounded executor
**Decision:** Complex Work Orders compile a governed Implementation Blueprint with G0-G3 guidance, exact scope/change surface/contracts/tests/evidence, a FROZEN/BOUNDED/OPEN_LOCAL/ESCALATE decision budget and evidence-backed Blueprint Deviations. Scope expansion, contract drift, invalidated tests or stale Context Locks cannot be hidden as local executor choices. Review binds exact Work Order, Context Lock, Blueprint and execution head. ADR-035.  
**Status:** FROZEN.

## D-036 — Cinematic, truthful and public-ready visual architecture
**Decision:** Hive Plan uses Obsidian Glass / Electric Signal with Hive Core and VoiceOrb as signature systems. Cinematic rendering may never fabricate operational truth or become the only representation of critical state; VisualTruthMirror/accessibility and adaptive graphics are mandatory. Future public-product seams are preserved without adding billing, public auth, multi-tenancy or marketplace scope to V1. ADR-036.  
**Status:** FROZEN.

## Open decisions
- Exact UADS/Hades V1 invocation/version details after implementation handshake evidence.
- Initial production LLM providers/models and numeric routing thresholds after current-provider evaluation.
- Exact polling cadence and optional webhook/tunnel implementation after benchmark.
- Exact primitive UI library, chart renderer and detailed graphics budgets after implementation bake-offs.
- Exact design-token values, fonts and brand accent tuning after contrast/display/golden-scene validation.
- Exact voice provider promotion order after Portuguese-BR quality/resource/privacy bake-off.
- Exact numeric thresholds/weights used by Planning Confidence and question-priority scoring after evals.
- Byte-level digest golden vectors and validator runtime selection at implementation time.
- Exact Work Order compiler retrieval thresholds, fusion/reranker and local embedding profiles after benchmark.
- Exact ModelMesh tier assignments, routing weights/budgets and safe-result cache eligibility after evals/current-provider refresh.
- Exact review impact-expansion thresholds, static-analysis portfolio and UADS model-per-agent assignments after review evals.
- Exact Blueprint guidance-depth thresholds and semantic-validator implementation after blueprint-efficiency evals.
