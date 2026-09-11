# HP-PLAN-010 — Work Order, Review + Agents Detailed Layout

Status: PROPOSED

## Work Order Studio
Visual objective: feel like a compiler/flight-plan surface, not a text editor.

Primary zones:
- identity/status header with WO, increment, risk and authorization;
- scope + acceptance center;
- Context Lock/source fingerprint rail;
- Change Surface map;
- AgentTaskGraph;
- FailureShield constraints;
- Test/Evidence obligations;
- CompileGuard panel;
- revision diff and STOP CONDITION.

Authorization state is unmistakable. Draft, stale, blocked and authorized must never share ambiguous styling.

## Review Command Center
Visual objective: enable senior review to locate material defects quickly.

Primary zones:
- snapshot bar: repo/PR/base/head/context/evidence roots;
- semantic changed-surface map;
- findings stack by severity/domain;
- code/diff workbench;
- CI/static/security/test evidence rail;
- ProofGraph/evidence coverage;
- specialist disagreement/blind spots;
- Review Receipt and verdict gate.

Selecting a finding synchronizes diff, impacted graph node, evidence and required proof. Findings without evidence are visibly distinguished from validated findings.

## Agents / Council
Visual objective: show coordinated engineering work without turning agents into cartoon characters.

Primary zones:
- TeamComposer roster;
- capability/authority badges;
- live AgentTaskGraph;
- task dependency lanes;
- write/read/watch ownership;
- UADS execution epoch;
- specialist outputs and dissent;
- cost/latency/resource pressure;
- integration barrier and completion state.

3D can represent team/task topology, but a deterministic DAG/list remains primary for execution truth.

## Cross-screen flow
WO -> Agents: inspect exact task assignment.
Agents -> Review: inspect resulting changed surface/evidence.
Review -> WO: trace finding to acceptance/proof obligation.
Review -> Brain: inspect architecture/failure memory.
Brain -> WO: propose bounded correction or future increment.

Shared entity identity enables smooth transition while retaining breadcrumb, SHA and Work Order identity.

## Voice examples
`qual agente está bloqueado?`
`mostre os arquivos que o backend pode escrever`
`abra o finding crítico`
`qual evidência falta para aprovar?`
`compare o diff com o MUST_TOUCH`
`gere a correção mínima`

## Acceptance direction
A reviewer should move from a finding to exact code, evidence, requirement and responsible task in a few interactions without manually hunting across unrelated screens.