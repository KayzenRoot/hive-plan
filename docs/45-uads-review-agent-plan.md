# UADS Multi-Agent Review Plan

Status: PROPOSED FOR FREEZE — HP-PLAN-006

## Mission
Use UADS agent parallelism to make reviews faster and deeper without duplicating work or flooding the context. Agents are spawned from the frozen ReviewScope, with explicit non-overlapping responsibilities and bounded evidence packages.

## Core rule
Do not create an agent because one exists. Create it because the change surface/risk gives it a distinct review question.

## Agent plan compiler
Before semantic review, Hive Plan compiles an `AgentReviewPlan` from:
- Work Order and acceptance criteria;
- immutable diff/head SHA;
- Feature Impact Graph neighborhood;
- risk/security/data/runtime boundaries;
- deterministic findings;
- required proof channels.

Each assignment contains:
- agent role;
- exact scope/files/symbols/contracts;
- questions to answer;
- evidence already available;
- findings it must not duplicate;
- output schema;
- stop condition;
- time/token budget;
- escalation rule.

## Core review roles

### Senior Review Lead
Always owns final semantic synthesis. Responsibilities:
- validate ReviewScope completeness;
- identify missing specialist coverage;
- adjudicate conflicting findings;
- deduplicate root causes;
- apply severity/policy;
- verify acceptance criteria coverage;
- prepare verdict candidate for independent audit when required.

### Change Impact Reviewer
Activated for non-trivial changes. Checks:
- changed behavior vs impacted consumers;
- contract/API compatibility;
- missing Feature Impact Graph edges;
- unexpected change-surface expansion;
- architecture boundary violations.

### Test & Regression Reviewer
Checks:
- acceptance criterion → proof mapping;
- TestLens plan adequacy;
- missing negative/edge tests;
- prior-regression recurrence;
- suspicious skips/flaky evidence;
- tests that pass without proving the changed behavior.

### Security Reviewer
Mandatory for auth/session/permissions/secrets/crypto/signing/untrusted input/security-boundary changes; optional by risk elsewhere. Focuses only on realistic exploit/failure paths and frozen security policy.

### Data & Migration Reviewer
Activated for schema, persistence, migrations, queues, consistency or data lifecycle changes. Checks compatibility, rollback/recovery, idempotency and integrity.

### API / Integration Reviewer
Activated for public/internal contracts, external providers, events, webhooks and cross-service changes. Checks compatibility, error semantics, retries/timeouts/idempotency and versioning.

### Frontend / UX Runtime Reviewer
Activated for UI/state/navigation/accessibility/error-state or client/server contract changes. It reviews behavior and regression, not subjective aesthetics unless design tokens/spec require it.

### Reliability / Concurrency Reviewer
Activated for async jobs, locks, retries, state machines, race-prone paths, caching, distributed effects or recovery logic.

### Performance Reviewer
Activated only when the change can materially affect latency, memory, IO, query count, rendering, build/runtime throughput or explicit performance SLOs.

### Infrastructure / Deployment Reviewer
Activated for CI/CD, container, environment, network, permissions, runtime config and deployment changes.

## Example agent plan: login change
```text
Senior Review Lead
  receives: full focused evidence summary

Security Reviewer
  receives: auth/session/cookie/guard slice
  checks: auth bypass, fixation, CSRF, cookie flags, privilege boundaries, rate/abuse paths

API/Integration Reviewer
  receives: login endpoint/contracts/error mapping
  checks: request/response compatibility and downstream consumers

Frontend Reviewer
  receives: login form/state/navigation slice
  checks: state races, error handling, protected-route transition

Test Reviewer
  receives: changed behavior + auth test neighborhood
  checks: positive/negative/session-expiry/protected-route proof

Change Impact Reviewer
  receives: FIG neighborhood + actual diff
  checks: missing impacted consumers and graph drift
```

No Data Reviewer is spawned if persistence/schema is demonstrably unaffected.

## Prompt contract for agents
Prompts must be incisive and scope-locked. Every specialist receives instructions equivalent to:

1. Review only the assigned semantic slice and explicitly linked impact edges.
2. Do not propose unrelated refactors/features.
3. Use deterministic evidence first; do not invent missing code or test results.
4. Report only actionable defects or explicit proof gaps.
5. For every finding provide severity, file/symbol/contract, concrete failure condition, evidence, impact and correction criterion.
6. Distinguish pre-existing issue from regression introduced by this head SHA.
7. If no material defect is found, return PASS with reviewed coverage, not filler comments.
8. Stop when assigned questions and proof obligations are resolved.

## Parallelism policy
Safe parallelism:
- independent specialist slices run concurrently after ReviewScope/SnapshotGuard freeze;
- deterministic checks run concurrently where resource limits permit;
- agents share immutable evidence references, not mutable state.

Serialize:
- Senior Review Lead synthesis after specialist completion;
- independent audit after verdict candidate;
- checkpoint/merge effects after final receipt.

## Finding exchange
All agent outputs normalize to one finding schema. Senior Review Lead groups findings by root cause and affected requirement.

An agent cannot directly APPROVE a PR. Specialists provide dispositions/findings; governance authority remains with Review Lead + required Auditor/policy.

## Correction prompt compilation
For CORRECTION_REQUIRED, Hive Plan compiles a bounded executor plan from findings:
- objective: fix only confirmed findings;
- frozen head/review reference;
- exact files/symbols likely affected;
- per-finding required correction;
- required tests/evidence;
- explicit out-of-scope list;
- agent assignments where UADS parallel implementation is safe;
- no unrelated cleanup/refactor;
- STOP CONDITION: all findings resolved and evidence produced.

### UADS implementation-agent splitting
Where corrections/implementation are genuinely independent, the executor prompt may assign:
- Agent A: backend/auth fix;
- Agent B: frontend state fix;
- Agent C: targeted tests;
- Agent D: docs/contract update;
with dependency/merge ordering defined.

Do not split two agents onto the same mutable symbols/files unless the executor has an explicit conflict-resolution workflow.

## Agent efficiency controls
- agent count is proportional to distinct risk domains, not PR size alone;
- each agent gets a ContextCapsule slice;
- duplicate context is referenced by digest where possible;
- deterministic findings suppress redundant LLM analysis;
- low-value specialists are skipped based on ReviewScope;
- agent outputs are cached only for exact immutable snapshot/tool/prompt profiles;
- correction rounds reuse unaffected specialist dispositions when fingerprints remain valid.

## Senior-quality requirement
The Senior Review Lead profile has a minimum STRONG QualityFloor for consequential final review and T4/HIGH_ASSURANCE behavior when policy requires. It is evaluated on defect recall, false positives, false approvals, source grounding and correction effectiveness, not verbosity.

## Freeze boundary
Freeze UADS agent-plan compilation, conditional specialist activation, non-overlapping scope contracts, normalized findings, Senior Review Lead authority, parallelism rules and bounded correction prompt compilation. Exact UADS CLI/API invocation and model-per-agent assignment remain integration/runtime decisions.