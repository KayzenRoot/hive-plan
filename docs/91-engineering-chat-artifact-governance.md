# HP-PLAN-010 — Engineering Chat Artifact Governance

Status: PROPOSED

## Principle
The Engineering Chat is where ideas are explored. Git-backed governed artifacts are where durable truth lives.

## Conversation state classes
- `EPHEMERAL` — ordinary discussion, never canonical.
- `WORKING` — active hypothesis/draft with provenance.
- `PROPOSED` — candidate artifact ready for validation.
- `VALIDATED` — evidence/specialist checks passed but not yet canonical.
- `FROZEN` — promoted through governance and persisted in canonical source.
- `SUPERSEDED` — historically valid but replaced.
- `REJECTED` — explicitly declined; retained only where useful for rationale/history.

## Promotion pipeline
```text
conversation
  -> structured candidate
  -> source/provenance attachment
  -> contradiction scan
  -> specialist activation by risk
  -> evidence/decision pressure test
  -> authority gate
  -> Git artifact
  -> PR/audit where required
  -> checkpoint/decision update
  -> FROZEN
```

## Promotion never happens from wording alone
Statements like “approved”, “decided”, “use this” or model confidence are not sufficient evidence of canonical promotion. The system checks operator/policy authority plus the required artifact lifecycle.

## Structured conversational artifacts
A chat turn may attach typed cards:
- `AssumptionCard`
- `DecisionCandidateCard`
- `ADRCard`
- `RequirementCard`
- `ArchitectureCard`
- `ResearchFindingCard`
- `FailurePatternCard`
- `WorkOrderCandidateCard`
- `ReviewFindingCard`
- `CheckpointDeltaCard`

Each card includes source refs, confidence/evidence status, owner/agent, lifecycle state and actions allowed by policy.

## Senior-agent collaboration
TeamComposer activates only the needed roles. Important artifacts may use a mini council:
1. primary specialist proposes;
2. relevant peer critiques;
3. dissent is captured rather than averaged away;
4. Engineering Director/Architect synthesizes within authority;
5. Independent Auditor enters only when risk/assurance requires.

Internal private chain-of-thought is never exposed. The UI shows conclusions, evidence, findings, dissent summaries and decisions.

## Research governance
Research Agent may search web/GitHub and propose technologies/patterns. Research results are `ADVISORY` until validated against official sources, repository reality, licensing, security, maintenance, compatibility and project architecture.

## Chat citations
Consequential claims should expose source chips/cards in the UI. Source state includes current/stale/superseded/unverified. Clicking a source should resolve to the exact project artifact, file/commit, evidence item or external reference when permitted.

## Conflict behavior
If two canonical sources conflict:
- do not silently choose the semantically closest;
- apply source hierarchy;
- if hierarchy does not resolve it, create contradiction record;
- block promotion of affected consequential artifact;
- ask/route to authorized resolution only when necessary.

## Decision continuity
When a decision becomes FROZEN, future conversations retrieve the decision and its rationale/provenance. A later contradictory proposal must acknowledge the frozen decision and either conform or initiate a governed supersession process.

## Learning loop
After implementation/review:
- verified success may become reusable engineering pattern;
- verified failure becomes failure pattern with root cause/correction;
- false positive review findings are marked to improve future review routing;
- escaped defects increase Review/FailureShield sensitivity for compatible future work;
- no single model observation self-modifies canonical policy.

## UX requirement
The user should be able to distinguish visually between:
- discussion;
- draft proposal;
- evidence-backed proposal;
- frozen decision;
- implementation work;
- review finding;
- blocker;
- superseded information.

The chat should feel conversational while maintaining an auditable engineering trail underneath.
