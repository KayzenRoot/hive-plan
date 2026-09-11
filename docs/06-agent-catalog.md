# Agent Catalog

Status: FROZEN V1 PLANNING DIRECTION

Hive Plan models a professional software organization through specialized agent roles. Roles are logical responsibilities; multiple roles MAY share the same underlying model/runtime when cost-efficient.

## Planning and product
- Interviewer / Discovery Agent
- Product Planner
- Requirements Engineer
- Software Architect
- Innovation Scout
- Documentation Engineer

## Engineering specialists
- Backend Engineer
- API / Integration Engineer
- Data Engineer / DBA
- Frontend / UI Engineer
- UX Engineer
- Platform / Infrastructure Engineer
- DevOps / Release Engineer
- Security Engineer
- Reliability / Error-Handling Engineer
- Performance Engineer
- Observability Engineer
- QA / Test Engineer
- Migration / Recovery Engineer when applicable

## Governance and delivery
- GitHub Steward
- Work Order Compiler
- Reviewer
- Independent Auditor
- Checkpoint / Continuity Agent
- FinOps / LLM Cost Engineer

## Authority rules
1. Agents propose; canonical state changes only through governed transitions.
2. No single planning agent may unilaterally freeze a high-impact architecture decision.
3. Important architecture/security/data decisions require independent critique.
4. Reviewer and Auditor are logically independent.
5. Executor claims are untrusted until verified.
6. HIGH/CRITICAL findings block progression.
7. Innovation Scout suggestions are classified before entering scope.

## Interviewer behavior
The Interviewer actively challenges ambiguity and asks decision-relevant questions about users, goals, constraints, failure modes, security, data, availability, deployment, UX, performance, cost, recovery, integrations, scale, and success criteria. It MUST avoid interrogation for its own sake: deterministic facts already known from canonical sources are not asked again.

## Innovation Scout behavior
For each meaningful proposal record: problem/opportunity, novelty, expected benefit, maturity, implementation cost, operational risk, security risk, architecture impact, vendor lock-in, measurable hypothesis, recommended experiment, and scope classification (NECESSARY / IMPORTANT / FUTURE / OUT OF SCOPE).
