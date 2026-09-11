# V1 Requirements

Status: PLANNING BASELINE

## Product and planning
- REQ-P01: Provide a specialized engineering chat for discussing, interviewing, planning, reviewing, and governing software projects.
- REQ-P02: Use an Interviewer/Discovery agent to expose ambiguity, missing constraints, hidden requirements, and scope risk.
- REQ-P03: Use specialist agents for product, architecture, security, data, infrastructure, DevOps, QA, resilience, performance, observability, frontend/UX, GitHub/release, documentation, FinOps/LLM cost, innovation, review, and audit.
- REQ-P04: Important architectural decisions require independent critique before canonical approval.
- REQ-P05: New ideas are classified NECESSARY, IMPORTANT, FUTURE, or OUT OF SCOPE and never enter active scope merely because an agent suggested them.

## Source of truth and memory
- REQ-M01: GitHub is canonical for approved project truth.
- REQ-M02: Hive V1 is the preferred RAG/memory provider behind a provider interface; local embedded RAG is fallback.
- REQ-M03: Chat history/model memory is non-canonical.
- REQ-M04: Critical context must be compiled from authoritative sources with relevance, deduplication, and token budgets.

## GitHub
- REQ-G01: Support PAT/token-based GitHub integration for the internal single-user deployment.
- REQ-G02: Support repository creation and organization when token permissions allow it.
- REQ-G03: Support branches, commits/changes, issues, pull requests, reviews, labels, milestones where available, tags, releases, semantic versioning policy, CI evidence, and repository health.
- REQ-G04: Use least privilege compatible with requested capabilities and never expose token material to the UI, logs, prompts, or repository.

## Work Orders / Codex
- REQ-W01: Compile approved planning into stable Work Orders with OBJECTIVE, CONTEXT, SCOPE, OUT OF SCOPE, FILES/SOURCES TO READ, REQUIREMENTS, ARCHITECTURE RULES, CONSTRAINTS, ACCEPTANCE CRITERIA, TESTS, DELIVERABLES, REVIEW FORMAT, and STOP CONDITION.
- REQ-W02: Preserve Work Order identity across implementation, correction, review, evidence, PR, and checkpoint.
- REQ-W03: Codex remains an external executor in V1.

## Auto review
- REQ-R01: A machine-readable completion manifest MAY announce completion or blocked state but is only a trigger, never proof.
- REQ-R02: Hive Plan observes GitHub/CI and automatically starts review after an execution completion condition is satisfied.
- REQ-R03: Review must independently verify base/head SHA, diff, changed files, CI, tests, lint/typecheck/build where applicable, acceptance criteria, architecture, requirements, security obligations, and evidence.
- REQ-R04: Verdicts are APPROVED, CORRECTION REQUIRED, or BLOCKED.
- REQ-R05: Safe corrections generate a Correction Delta for the same Work Order/PR.
- REQ-R06: No automatic progression while HIGH/CRITICAL defects remain.

## LLM economics
- REQ-L01: Cheap models are default for low-risk work.
- REQ-L02: Risk/complexity routing escalates stronger models only when justified.
- REQ-L03: Use provider prompt caching, local context cache, RAG, delta context, deduplication, stable prefixes, and deterministic computation before LLM calls.
- REQ-L04: Expose token/cost telemetry by project, Work Order, agent, model, and time window.

## UI
- REQ-U01: Dark technological command cockpit.
- REQ-U02: Project navigation, engineering chat, active Work Order/PR/checkpoint, health, cost/tokens, agent activity, CI, risks, blockers, and progress are visible from the cockpit.
- REQ-U03: Support architecture/infra diagrams and visual planning artifacts; frontend planning may include mockups/images.
- REQ-U04: Real-time or near-real-time state updates for local execution and GitHub observation.

## Local operation
- REQ-O01: Run locally via Docker/Compose.
- REQ-O02: Persistent project state survives restarts.
- REQ-O03: External data sent to LLM providers is minimized to the necessary compiled context.
