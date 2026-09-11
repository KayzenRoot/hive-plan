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

## Open decisions
- Exact framework/runtime stack.
- Exact vector store/database strategy after benchmark.
- Exact UADS/Hades V1 integration contract/version.
- Initial LLM providers/models and routing thresholds.
- Event observation strategy mix (polling vs optional local tunnel/webhook).
- Exact design tokens/brand accent system.
- Exact numeric thresholds/weights used by Planning Confidence and question-priority scoring after evals.
- Byte-level digest golden vectors and validator runtime selection at implementation time.
- Exact Work Order compiler backend thresholds, retrieval fusion/reranker and local embedding profiles after benchmark.