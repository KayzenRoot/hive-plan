# HP-PLAN-010 — Conversational Agent Council + Artifact Promotion

Status: PROPOSED

## Mission
Let Engineering Chat automatically assemble the smallest useful expert team for each conversation turn, expose useful participation to the operator, and convert validated conclusions into governed project artifacts without turning agent conversation into source truth.

## Conversation orchestration
`ConversationDirector` receives user input, current project, Project Brain context, risk/ambiguity classification and tool needs. It asks `TeamComposer` for the minimum specialist set.

Examples:
- visual frontend request -> Frontend + UX, optionally Performance;
- auth/login change -> Security + Backend/API + Frontend + QA;
- database migration -> Data + Backend + Recovery + QA;
- HIVE question -> A-031 HIVE specialist;
- UGAS production -> A-032 UGAS specialist;
- UADS execution/orchestration -> A-033 UADS specialist;
- novel technology decision -> Research/OSS + Innovation + relevant domain specialist.

No fixed swarm. One strong agent is preferred when coordination cost exceeds expected value.

## Agent interaction
Agents communicate through CouncilBus structured messages:
- observation;
- evidence;
- hypothesis;
- proposal;
- objection;
- risk;
- question-to-peer;
- handoff;
- recommendation;
- dissent.

The user-facing UI may show role, status, concise contribution and final synthesis, but never exposes private chain-of-thought.

## Council lifecycle
1. classify turn;
2. retrieve Project Brain context;
3. choose specialists;
4. parallel research/analysis only where dependencies allow;
5. deterministic evidence/tool checks;
6. specialist findings;
7. disagreement detection;
8. adjudication or operator escalation;
9. response synthesis;
10. optional artifact proposal;
11. promotion gate if operator/policy authorizes.

## Dissent
Material specialist disagreement is first-class. `DissentLedger` records the disputed claim, evidence on both sides, risk and resolution. High-impact unresolved disagreement blocks automatic artifact freeze.

## Research
Eligible agents can invoke ResearchRadar for web/GitHub research under provenance and untrusted-content rules. Findings carry source, timestamp, license/security notes when technology adoption is proposed, and an ADOPT/TRIAL/WATCH/REJECT recommendation where applicable.

## Artifact promotion
Conversation output can propose, but not silently canonize:
- Decision/ADR;
- requirement change;
- architecture change;
- Work Order;
- checkpoint delta;
- failure/success pattern;
- Skill candidate;
- Feature Impact Graph update.

Promotion pipeline:
`conversation claim -> proposed artifact -> authority/conflict check -> specialist review -> deterministic validation -> operator/policy authorization -> GitHub commit/PR -> canonical`

## Voice interaction with council
Voice and typed input use the same `ConversationTurn` contract. Spoken commands such as "chame o especialista de segurança", "pesquise no GitHub", "transforme isso em ADR" or "não congele ainda" become intent candidates, but authority-sensitive actions still follow confirmation/promotion policy.

## User experience
The chat can display a compact Agent Council rail:
- active agents;
- waiting/tool/research state;
- concise findings count;
- disagreement indicator;
- evidence/source count;
- current proposed artifact.

The UI should feel alive without exposing raw internal reasoning or flooding the user with inter-agent chatter.

## Cost control
Cheap/deterministic routing handles classification, retrieval and low-risk extraction. Strong models are reserved for complex synthesis, architecture/security and disagreement. The council records expected vs actual Verified Outcome Cost.

## STOP CONDITION
Do not freeze until team selection, council message contract, disagreement gate, research authority, artifact promotion path, voice parity and cost controls are explicit and testable.