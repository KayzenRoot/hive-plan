# HP-PLAN-007 Agent System Freeze

Status: FROZEN BY OPERATOR DIRECTION — pending PR audit/merge

## Frozen decisions

### F-007-01 — Agents are authored canonically in Hive Plan
All V1 agent roles, charters and runtime identities are defined in the Hive Plan repository by planning governance. Codex/UADS implementations MUST consume these definitions and MUST NOT invent replacement/ad-hoc agent roles as hidden runtime behavior.

Canonical definitions:
- `agents/registry.yaml`
- `agents/README.md`
- `docs/66-agent-operating-system.md`
- `docs/69-v1-agent-charters.md`

### F-007-02 — Governed senior-team operating model
The 30-agent V1 roster behaves as a professional software organization through TeamComposer, Capability Ledger, ExpertiseGraph, CouncilBus, Dissent Ledger and AgentGovernor. Seniority is enforced by role contract, evidence, tools, failure-mode analysis, quality gates and evals rather than personality text.

### F-007-03 — Minimal sufficient team
Hive Plan chooses one or more agents adaptively. Multi-agent execution is justified only when distinct expertise, independent critique or safe parallelism improves expected verified outcome. The system records coordination overhead and may demote multi-agent patterns that do not beat single-agent baseline.

### F-007-04 — AgentTaskGraph and safe ownership
ExecutorFit may compile a canonical Work Order/Correction Delta into a non-canonical AgentTaskGraph with explicit dependencies, WRITE_SET, READ_SET, WATCH_SET, ContextCapsules, skills, tools, proof obligations, budgets and STOP CONDITION. Unknown write conflicts default to serialization.

### F-007-05 — Skills are reusable governed capabilities
Agents may discover, reuse, compose, request and create candidate skills. SkillForge validates and promotes skills through versioning, tests, security/permission checks, provenance and benchmark evidence. Skills cannot self-grant authority or tools.

### F-007-06 — Research is a first-class capability
Qualified agents may research the current web and GitHub for standards, technology options, prior art, repository due diligence and failure analysis. External material is untrusted evidence, not instructions. Serious third-party adoption requires current evidence, license/security/maintenance/lock-in analysis and governed ADOPT/TRIAL/WATCH/REJECT decision.

### F-007-07 — Inter-agent collaboration is structured
Agents communicate conclusions, facts, findings, evidence, uncertainty, dependencies, requests and proposals through CouncilBus. Material disagreement is preserved in Dissent Ledger and resolved by evidence/policy/operator authority rather than majority vote. Private chain-of-thought is not a collaboration payload.

### F-007-08 — Open-standard compatibility without lock-in
Hive Plan keeps core semantics provider/executor-neutral while designing adapters compatible with useful open ecosystem concepts:
- Agent Skills-style reusable skill packages;
- MCP-compatible tool/data adapters where useful;
- A2A-compatible capability discovery/delegation concepts where useful.
None is a mandatory V1 domain dependency.

### F-007-09 — Research/skill/context efficiency
ResearchRadar deduplicates external research; SkillResolver avoids skill duplication; ContextCapsules avoid sending full project context to every agent; stable agent/skill prefixes are cache-friendly; handoffs transmit deltas/evidence instead of full transcripts.

### F-007-10 — Evidence remains above agent claims
No agent, agent council, skill or executor completion result can replace Git/CI/tests/static evidence or governed canonical promotion. HIGH/CRITICAL unresolved findings and missing mandatory evidence block progression.

## V1 roster
30 governed roles, A-001 through A-030, are defined in `docs/69-v1-agent-charters.md` and machine-registered in `agents/registry.yaml`.

## Implementation constraint
Production implementation is still NOT authorized. When implementation begins, the executor must implement/load the canonical agent definitions rather than designing the team anew.