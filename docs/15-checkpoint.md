# Checkpoint

Checkpoint ID: HP-CP-0017  
Status: PLANNING ACTIVE  
Canonical branch target: `main`  
Last canonical planning merge: `a1830a317c1fd5bef77409b5bc00426ec85d6c75` (`HP-PLAN-006`)  
Active planning increment: `HP-PLAN-007`  
Active planning branch: `docs/hp-plan-007-uads-agent-contract`

## Frozen foundation
- Product identity/V1 mission, local-first single-user Docker deployment and GitHub canonical truth.
- Hive V1 preferred MemoryProvider with embedded local-RAG fallback.
- Codex remains external executor; Hive Plan owns planning/governance/Work Orders/review/audit/continuity.
- Context-first discovery, Planning Confidence, Assumption Register, Decision Pressure Test and governed agent authority.
- Operational learning memory with verified successes, failures, corrections and provenance.
- Short-lived GitHub branches, governed PR/release lifecycle and verified-throughput objective.
- Versioned JSON artifact contracts, deterministic fingerprints, Review Receipts and Checkpoint Deltas.
- Work Order Compiler: RepoPulse, ChangeGraph/FIG, FailureShield, TestLens, ContextCapsule, ExecutorFit and CompileGuard.
- QualityFloor T0–T4, Verified Outcome Cost/Rework Tax, provider-neutral ModelMesh/CacheFabric and no silent HIGH_ASSURANCE downgrade.
- EventSpine/GitPulse, ReviewMVCC/SnapshotGuard, EvidenceForge/Watermark, ReviewLease/EffectLedger and stale-review cancellation.
- Focused Senior Review: actual diff + semantic impact closure, conditional UADS specialists, FindingGate, SARIF-normalized analyzers and delta-first corrections.

## Newly frozen in HP-PLAN-007
- **30 canonical V1 agent roles** authored in Hive Plan, A-001 through A-030; Codex/UADS must implement/load these definitions rather than inventing hidden roles.
- Agent Operating System with TeamComposer, Capability Ledger, ExpertiseGraph, CouncilBus, Dissent Ledger and AgentGovernor.
- Seniority by contract/evidence/evals, not persona wording.
- Minimal-sufficient-team policy: one agent by default unless distinct expertise, independent assurance or safe parallelism creates verified value.
- AgentTaskGraph with explicit dependencies, WRITE_SET/READ_SET/WATCH_SET, ContextCapsules, skills/tools, proof obligations, budgets and STOP CONDITION.
- Dynamic ConcurrencyGovernor and conflict-safe serialization when mutable ownership safety cannot be proven.
- SkillCatalog/SkillForge/SkillResolver/SkillFitness: agents may discover, reuse, compose, request and create candidate skills, but skills require validation/promotion and cannot self-grant permissions/authority.
- ResearchRadar + Research/OSS Intelligence protocol: web/GitHub research is first-class but external content is untrusted evidence, not instruction authority.
- OSS/technology due diligence covers license, maintenance, security, lock-in, benchmark evidence and ADOPT/TRIAL/WATCH/REJECT classification.
- Structured inter-agent collaboration and explicit Dissent Ledger; majority vote cannot replace technical evidence.
- Portable/open-standard direction: Agent Skills-style packages, MCP-compatible tool adapters and A2A-compatible discovery/delegation concepts may be used behind adapters without becoming mandatory V1 domain dependencies.
- Stable agent prompt envelope + bounded dynamic ContextCapsules for caching/token efficiency.

## Canonical/proposed HP-PLAN-007 artifacts
- `docs/65-uads-agent-execution-contract.md`
- `docs/66-agent-operating-system.md`
- `docs/67-skill-fabric.md`
- `docs/68-research-and-open-source-intelligence.md`
- `docs/69-v1-agent-charters.md`
- `docs/70-intelligent-team-composition.md`
- `docs/71-hp-plan-007-agent-system-freeze.md`
- `agents/registry.yaml`
- `agents/README.md`
- `skills/README.md`
- `skills/_template/SKILL.md`
- Issue #14.

## Completed planning increments
- HP-PLAN-001 — Interviewer + Planning Protocol.
- HP-PLAN-002 — delivery lifecycle, operational memory and GitHub governance.
- HP-PLAN-003 — machine-readable artifact contracts.
- HP-PLAN-004 — Work Order Compiler & Context Optimization Engine.
- HP-PLAN-005 — Model Router + Cache/Cost Engine.
- HP-PLAN-006 — Event Spine + Auto Review + Focused Senior Review.

## Open decisions
- Exact UADS/Hades V1 invocation/version/capability handshake and adapter transport.
- Exact worktree/workspace isolation supported by UADS/Hades.
- Exact Team Utility scoring weights/concurrency ceilings after evals.
- Exact durable database/journal/wake-up queue implementation after stack/data ADR.
- Exact polling/quiescence thresholds and review analyzer portfolio after benchmarks.
- Initial model/provider mappings and numeric routing budgets after current-provider evals.
- Exact Work Order retrieval fusion/local embedding/reranker choices after benchmarks.
- Data/persistence/vector-store decision.
- Technology stack ADR.
- Detailed cockpit design system and interaction model.
- Numeric Planning Confidence thresholds and artifact digest golden vectors.

## Blockers
None for HP-PLAN-007 objective audit/merge or continued planning.

## Implementation authorization
NOT GRANTED. Production code remains blocked until planning freeze audit authorizes the first implementation Work Order.

## Proposed next increment after HP-PLAN-007
Design the **Technology Stack + Data/Persistence Architecture ADR** and benchmark plan, including application runtime/frameworks, relational/event/cache/vector/search storage, local hardware constraints, migrations/backups, security, observability and replaceable adapters. This will resolve several deferred implementation choices before frontend/backend coding begins.