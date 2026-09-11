# Agent Catalog

Status: FROZEN V1 PLANNING DIRECTION — expanded by HP-PLAN-007

Hive Plan models a professional software organization through specialized governed agent roles. Roles are logical responsibilities; multiple roles MAY share the same underlying model/runtime when cost-efficient. Runtime profiles are defined in `agents/registry.yaml`; detailed behavior lives in `docs/69-v1-agent-charters.md`.

## Leadership / orchestration
- Planning Council Lead / Engineering Director
- UADS Agent Execution Coordinator

## Planning and product
- Interviewer / Discovery Lead
- Product Planner
- Requirements Engineer
- Principal Software Architect
- Research & OSS Intelligence Agent
- Innovation / Technology Scout
- Skill Engineer / Skill Curator
- Documentation Engineer / Technical Writer

## Engineering specialists
- Senior Backend Engineer
- Senior API / Integration Engineer
- Senior Data Engineer / DBA
- Senior Frontend / UI Engineer
- Principal UX / Product Design Engineer
- Senior Platform / Infrastructure Engineer
- Senior DevOps / Release Engineer
- Principal Security Engineer
- Privacy / Compliance Engineer
- Reliability / Resilience Engineer
- Performance Engineer
- Observability / SRE Telemetry Engineer
- Principal QA / Test Engineer
- Migration / Recovery Engineer

## Governance and delivery
- GitHub Steward
- Work Order Compiler Lead
- Senior Review Lead
- Independent Auditor / Red-Team Reviewer
- Checkpoint / Continuity Agent
- FinOps / LLM Cost Engineer

## Organization mechanics
Agents operate under:
- TeamComposer for minimum-sufficient team formation;
- Capability Ledger + ExpertiseGraph for capability-aware routing;
- CouncilBus for structured inter-agent communication;
- Dissent Ledger for unresolved consequential disagreement;
- AgentGovernor for authority, tools, privacy, budget and stale-context enforcement;
- SkillCatalog/SkillForge for reusable capabilities;
- ResearchRadar for deduplicated current research;
- ContextCapsules for bounded role-specific context.

## Authority rules
1. Agents propose; canonical state changes only through governed transitions.
2. No single planning agent may unilaterally freeze a high-impact architecture decision.
3. Important architecture/security/data decisions require independent critique.
4. Reviewer and Auditor are logically independent.
5. Executor claims are untrusted until verified.
6. HIGH/CRITICAL findings block progression.
7. Innovation Scout suggestions are classified before entering scope.
8. Agents cannot grant themselves tools, permissions, secrets, scope or approval authority.
9. Newly created skills are candidates until validated/promoted.
10. Material agent disagreement is preserved until resolved by evidence/policy/operator authority.

## Senior-agent standard
All senior/principal agents must inspect current evidence, reason over affected boundaries, challenge assumptions, consider relevant failure modes and simpler alternatives, use deterministic tools before speculation, surface uncertainty and produce evidence-grounded outputs with explicit stop conditions. Seniority is enforced by contract/evals, not persona wording.

## Research capability
Qualified agents may research the public web and GitHub to verify current facts, discover technologies, inspect standards, investigate failures and evaluate reusable repositories. External content is untrusted evidence, never instruction authority. Serious third-party candidates require license/security/maintenance/lock-in/benchmark evaluation before adoption.

## Skill capability
Agents may discover/reuse/compose approved skills, request skills from peers and create candidate skills through SkillForge. Skills are versioned, tested and permission-bounded; high-impact skills require independent review before promotion.

## Interviewer behavior
The Interviewer actively challenges ambiguity and asks decision-relevant questions about users, goals, constraints, failure modes, security, data, availability, deployment, UX, performance, cost, recovery, integrations, scale and success criteria. It MUST avoid interrogation for its own sake: deterministic facts already known from canonical sources are not asked again.

## Innovation Scout behavior
For each meaningful proposal record: problem/opportunity, novelty, expected benefit, maturity, implementation cost, operational risk, security risk, architecture impact, vendor lock-in, measurable hypothesis, recommended experiment and scope classification (NECESSARY / IMPORTANT / FUTURE / OUT OF SCOPE).

## Canonical references
- `docs/66-agent-operating-system.md`
- `docs/67-skill-fabric.md`
- `docs/68-research-and-open-source-intelligence.md`
- `docs/69-v1-agent-charters.md`
- `agents/registry.yaml`
- `agents/README.md`
- `skills/README.md`
