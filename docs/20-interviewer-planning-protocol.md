# Interviewer + Planning Protocol

Status: PROPOSED FOR FREEZE — HP-PLAN-001

## Purpose
The Interviewer is the discovery lead for Hive Plan. Its job is not to ask many questions; its job is to reduce uncertainty, expose contradictions, surface hidden requirements, and prepare evidence-backed planning decisions with the least unnecessary interaction and LLM spend.

## Operating principles
1. Context first, questions second.
2. Never ask for facts already available from canonical sources or deterministic tools.
3. Ask only decision-relevant questions.
4. Prefer 3–5 high-value questions per round.
5. Challenge weak assumptions and unsafe/over-complex proposals.
6. Escalate to specialists by domain/risk instead of pretending one agent is expert in everything.
7. Record assumptions explicitly.
8. Separate ideas from approved scope.
9. Stop discovery when sufficient certainty exists for the next governed decision, not when every imaginable detail is known.
10. Every consequential planning conclusion must be traceable to source, assumption, decision, or operator input.

## Discovery state machine
```text
USER IDEA
  ↓
SOURCE CHECK
  ↓
KNOWN-FACT MAP
  ↓
UNCERTAINTY / CONTRADICTION MAP
  ↓
QUESTION PRIORITIZATION
  ↓
SHORT INTERVIEW ROUND
  ↓
SPECIALIST ESCALATION (when needed)
  ↓
ASSUMPTION + RISK UPDATE
  ↓
IDEAS / TECHNOLOGY OPTIONS
  ↓
DECISION PRESSURE TEST
  ↓
PLANNING CONFIDENCE MAP
  ↓
STOP CONDITION CHECK
  ├─ insufficient → next short round
  └─ sufficient   → Planning Council synthesis → operator approval → freeze/ADR
```

## Source check order
Before asking questions, resolve the current project truth using the repository Source Hierarchy. At minimum inspect the approved checkpoint, relevant ADRs/decisions, scope, DoD, architecture, requirements, Git state, active Work Order/PR if any, and RAG-retrieved supporting sources.

## Question priority
Questions are ranked by expected decision value. A reference heuristic is:

`priority = impact × uncertainty × irreversibility × risk × dependency_reach`

The implementation may normalize/scalar-weight these dimensions, but the rule is invariant: high-impact unknowns are asked before low-impact preferences.

### Question classes
- Goal / user / business outcome
- Scope and non-goals
- Constraints and operating environment
- Data and persistence
- Security / privacy / compliance
- Failure modes / resilience / recovery
- Architecture / integration / dependency boundaries
- Performance / scale / capacity
- UX / accessibility / frontend behavior
- Testing / verification / observability
- Deployment / operations / release
- Cost / LLM economics / infrastructure
- Migration / compatibility / rollback
- Success criteria / Definition of Done

## Adaptive interviewing
The Interviewer MUST NOT execute a fixed questionnaire. It chooses the smallest useful next question set from unresolved high-value uncertainties. Low-impact styling/preferences are deferred until they become relevant.

## No-repeat contract
Before asking, the Interviewer checks whether the answer exists in canonical sources, prior operator-approved decisions, structured project state, or deterministic tool output. If present, it reuses the fact and cites its source internally rather than asking again.

## Specialist escalation
The Interviewer invokes specialists when a domain threshold is crossed. Examples:
- sensitive/privileged data → Security + Data
- migration/persistence change → Data + Migration/Recovery + Reliability
- public API/third-party integration → API/Integration + Security + Reliability
- high-cost inference path → FinOps/LLM + Performance
- large architecture change → Architect + relevant domain specialists + independent critic
- HIGH_ASSURANCE domain → independent review is mandatory

The operator still interacts with one conversational surface; specialist outputs are synthesized and de-duplicated by the Interviewer/Planning Council.

## Critical challenge behavior
The Interviewer is not an agreement engine. When a proposal creates disproportionate complexity, risk, cost, coupling, security exposure, or scope expansion, it MUST present the concern, evidence/reasoning summary, safer/simpler alternatives, and reversibility trade-offs before asking for a decision.

## Assumption Register
Any assumption material enough to affect planning is explicit.

Minimum fields:
- Assumption ID
- statement
- source/reason
- confidence
- impact if wrong
- affected domains
- validation method
- owner
- status: OPEN / VALIDATED / REJECTED / SUPERSEDED

Critical assumptions cannot remain OPEN at freeze.

## Planning Confidence Map
Hive Plan maintains domain-level confidence based on evidence quality and unresolved uncertainty, not model self-confidence alone.

Suggested domains:
- Product
- Scope
- Architecture
- Security
- Data
- Infrastructure
- Reliability
- Performance
- Observability
- QA/Test
- UX/UI
- Integrations
- Deployment/Release
- Cost/FinOps
- Recovery/Migration

Each domain exposes at least:
- confidence score/band
- unresolved critical unknowns
- evidence/source coverage
- blocking contradictions
- responsible specialist

The score is an operator aid, never a substitute for explicit blocking conditions.

## Decision Pressure Test
Before freezing a consequential decision, Hive Plan tests it against:
- What can make this fail?
- Which alternatives were considered and why rejected?
- How expensive is reversal?
- What happens at 10× expected scale?
- What happens when a key dependency is unavailable?
- What happens under malformed/adversarial input?
- What data can be lost/corrupted and how is it recovered?
- What observability proves the design is healthy?
- What security boundary changes?
- What is the simplest viable alternative?

For HIGH/ELEVATED impact decisions, an independent critic must attempt to falsify the preferred option.

## Innovation lane
The Innovation Scout may introduce new technologies or original ideas during discovery, but every proposal is tagged:
- NECESSARY
- IMPORTANT
- FUTURE
- OUT OF SCOPE

Each meaningful proposal records expected benefit, maturity, implementation cost, operational cost, security risk, lock-in, reversibility, evidence level, and recommendation (ADOPT / TRIAL / WATCH / REJECT). Suggestions never silently expand active scope.

## Stop condition
Discovery for the current decision/increment may stop only when:
- critical unknowns = 0
- high-risk unknowns = 0 or explicitly accepted with mitigation
- blocking contradictions = 0
- scope/non-goals are clear enough for the next step
- success criteria are testable
- required specialist domains have responded
- critical assumptions are validated/rejected
- architecture feasibility is sufficient for the decision
- relevant security/data/recovery obligations are known
- Planning Confidence Map is above configured thresholds for required domains
- remaining unknowns are explicitly non-blocking

The goal is `sufficiently specified`, not `infinitely specified`.

## Planning Council synthesis
After stop conditions are met, the Planning Council produces a compact Decision Packet containing:
- problem / objective
- canonical context used
- requirements and constraints
- proposed decision
- considered alternatives
- trade-offs
- assumptions
- risks and mitigations
- specialist findings
- confidence map snapshot
- scope classification
- tests/evidence required later
- proposed canonical changes
- operator decisions still required

Only after governed approval may the result update ADRs/Decisions/Scope/Requirements/Architecture/Checkpoint.

## Cost-control rules
- deterministic/source lookup before LLM
- retrieve only relevant RAG slices
- stable cached system/policy prefixes
- cheap model for extraction/classification/routing by default
- stronger model only for complexity/risk thresholds
- specialist calls batched/de-duplicated where safe
- no repeated question or analysis when source state is unchanged
- cache planning artifacts by canonical-source fingerprints
- invalidate dependent analysis when a critical fingerprint changes

## UX behavior
The cockpit should show the interview as a living planning state: current question round, unresolved high-impact unknowns, specialists consulted, assumptions, confidence map, new-technology proposals, pending decisions, and the exact reason discovery can or cannot stop.
