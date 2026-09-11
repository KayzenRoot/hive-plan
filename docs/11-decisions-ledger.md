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

## Open decisions
- Exact framework/runtime stack.
- Exact vector store/database strategy after benchmark.
- Exact UADS/Hades V1 integration contract/version.
- Initial LLM providers/models and routing thresholds.
- Event observation strategy mix (polling vs optional local tunnel/webhook).
- Exact design tokens/brand accent system.
- Exact numeric thresholds/weights used by Planning Confidence and question-priority scoring after evals.
