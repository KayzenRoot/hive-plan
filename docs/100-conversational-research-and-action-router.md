# HP-PLAN-010 — Conversational Research + Governed Action Router

Status: PROPOSED

## Mission
Let the operator naturally ask the chat to research, inspect repositories, compare technologies, generate governed artifacts and initiate allowed workflows without memorizing tools or command syntax.

## Intent lanes
Every turn is classified into one or more lanes:
- ANSWER: grounded explanation only;
- PROJECT_QUERY: inspect canonical project sources;
- RESEARCH: current web/GitHub/primary-source research;
- ANALYZE: deterministic/tool-assisted analysis;
- PROPOSE_ARTIFACT: draft ADR/WO/checkpoint/decision;
- SAFE_ACTION: bounded reversible action under policy;
- HIGH_IMPACT_ACTION: requires explicit authority/confirmation;
- MEDIA: diagram/chart/image/UGAS-related request;
- VOICE_CONTROL: stop/read/repeat/navigate/listening controls.

## Research behavior
ResearchRadar deduplicates searches, prefers primary sources, records freshness and source quality, and separates external claims from canonical project truth. GitHub repository research uses Repository Intelligence Cards where adoption is being considered.

## Action planning
Natural language never maps directly to a privileged tool call. `ActionRouter` produces a typed ActionPlan containing intent, target, parameters, authority requirement, reversibility, expected effects, evidence plan and rollback/cancel behavior.

## Confirmation policy
No confirmation spam for harmless read-only operations. Explicit confirmation is required when policy says operator authority is necessary, including destructive/irreversible actions, privilege/security changes, secret exposure, scope expansion and contested high-impact decisions.

Voice and typed input use the same authority rules.

## Artifact commands
Natural requests such as `transforme isso em ADR`, `gere o próximo Work Order`, `registre no checkpoint`, `pesquise alternativas no GitHub`, `mostre em diagrama` or `faça o review` resolve into governed pipelines rather than one-shot free-form text.

## Failure behavior
If required connector/provider/tool is unavailable, show exact unavailable capability and safe alternatives. Never claim an action or research result occurred when it did not.

## Auditability
Every external action records request, resolved target, policy decision, executor/tool, effect receipt and resulting source fingerprint where applicable.

## STOP CONDITION
Freeze only when intent lanes, ActionPlan contract, authority mapping, failure semantics and audit trail are explicit and testable.