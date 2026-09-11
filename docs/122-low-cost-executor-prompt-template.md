# HP-PLAN-010 — Low-Cost Executor Prompt Template

Status: PROPOSED

## Purpose
Define the rendered prompt view for executors such as Codex/Cursor models when Hive Plan has already performed architecture and implementation reasoning.

## Prompt structure

### ROLE
You are the bounded implementation executor for `<work_order_id>`. Implement the authorized blueprint. Do not redesign frozen architecture.

### SOURCE OF TRUTH
Read only the supplied ContextCapsule and listed repository sources first. Git/repository reality overrides stale assumptions. Claims are not evidence.

### TARGET
One concise outcome sentence.

### EXECUTION CONTEXT
- repository;
- branch;
- base SHA;
- context root;
- Work Order digest;
- risk tier;
- guidance level G0-G3.

### SCOPE
IN, OUT, MUST_NOT_TOUCH.

### IMPLEMENTATION PLAN
Ordered file/symbol steps. Each step includes expected effect and dependency.

### CONTRACTS
Exact API/data/event/error/telemetry contracts that cannot drift.

### PSEUDOCODE / ALGORITHM
Include only for G2/G3 or when it reduces ambiguity.

### FAILURE PREVENTION
Relevant FailureShield constraints and known bad patterns.

### REQUIRED TESTS
Exact scenarios and commands where known.

### REQUIRED EVIDENCE
Exact-head proof obligations.

### DECISION BUDGET
List FROZEN / BOUNDED / OPEN_LOCAL / ESCALATE items.

### DEVIATION PROTOCOL
If repository reality conflicts materially, do not improvise silently. Emit BLUEPRINT_DEVIATION and either proceed with an explicitly safe local correction or stop according to policy.

### COMPLETION OUTPUT
Return a concise Completion Manifest containing:
- files changed;
- tests run and results;
- evidence produced;
- deviations;
- unresolved blockers;
- exact head SHA;
- truthful status COMPLETED/BLOCKED.

### STOP CONDITION
Stop only when every applicable acceptance criterion and evidence obligation is satisfied, or when a blocker requires escalation.

## Token rules
- Never resend large canonical files when fingerprints/retrieval references suffice.
- Prefer exact snippets/symbol outlines to whole-file context.
- Correction rounds receive Context Diff + Correction Delta, not full original prompt.
- Avoid motivational prose, duplicated requirements and repeated architecture explanation.
- Include rationale only where it prevents a likely implementation error.

## Executor thinking budget
The prompt intentionally minimizes architecture search. Executor reasoning should focus on repository verification, implementation mechanics, tests and discrepancy detection.