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

## Open decisions
- Exact framework/runtime stack.
- Exact vector store/database strategy after benchmark.
- Exact UADS/Hades V1 integration contract/version.
- Initial LLM providers/models and routing thresholds.
- Event observation strategy mix (polling vs optional local tunnel/webhook).
- Exact design tokens/brand accent system.
