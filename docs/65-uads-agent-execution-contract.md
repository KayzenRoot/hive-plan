# UADS/Hades Agent Execution Contract

Status: PROPOSED FOR FREEZE — HP-PLAN-007

## Mission
Translate one canonical Hive Plan Work Order or Correction Delta into a safe executor-specific multi-agent execution plan without changing objective, scope, acceptance criteria, architecture constraints or evidence obligations.

## Boundary
Canonical truth remains:
`Work Order / Correction Delta + Context Lock + project sources`.

`AgentTaskGraph` is an executor rendering/plan, not new project truth.

## Core artifacts

### Executor Capability Manifest
A versioned handshake describing what the connected executor can actually do:
- executor name/version;
- agent creation/parallelism support;
- maximum/constrained concurrency;
- isolated workspace/worktree support;
- file/symbol ownership/conflict controls;
- terminal/test/tool access;
- structured output support;
- cancellation/resume/retry capabilities;
- commit/push/PR capabilities;
- supported Hive Plan artifact contract versions;
- model/profile selection controls if exposed;
- evidence/telemetry channels.

Hive Plan must not assume a UADS capability that the manifest does not advertise.

### AgentTaskGraph
A DAG compiled from the canonical Work Order.

Each task contains:
- task_id;
- agent_role;
- objective;
- dependency task IDs;
- exact semantic scope;
- ContextCapsule refs;
- expected file/symbol ownership;
- allowed read neighborhood;
- out-of-scope boundaries;
- acceptance/proof obligations;
- required deterministic commands/tests;
- budget/timeout hints;
- completion output schema;
- STOP CONDITION.

### Agent Completion Result
Each agent reports structured claims:
- task_id/status;
- files/symbols changed or inspected;
- commands/checks claimed;
- produced artifacts;
- deviations from assigned scope;
- blockers;
- evidence pointers;
- handoff notes to dependent tasks.

Claims remain non-authoritative until Hive Plan/Git/CI independently verifies them.

## Parallelism compiler
Hive Plan classifies task relationships:
- PARALLEL_SAFE: disjoint mutable ownership and no ordering dependency;
- PARALLEL_READ_ONLY: concurrent analysis/review only;
- ORDERED: task B requires output/commit from task A;
- EXCLUSIVE: shared mutable state/symbols require serialization;
- INTEGRATION_BARRIER: multiple tasks must complete before one integration/test task.

Default to serialization when ownership/conflict safety cannot be proven.

## Ownership model
Prefer symbol/module ownership over crude file-count splitting.

An agent may receive:
- WRITE_SET: files/symbols it may mutate;
- READ_SET: bounded supporting context;
- WATCH_SET: dependencies it must not mutate without escalation.

If execution discovers a required mutation outside WRITE_SET, the agent reports `SCOPE_EXPANSION_REQUIRED`; the orchestrator recompiles/authorizes ownership rather than silently editing it.

## Example
```text
WO: Change login flow

A Backend/Auth
  WRITE: auth handler + session helper

B Frontend
  WRITE: login UI/state

C Tests
  READ: A/B contracts
  WRITE: targeted tests
  depends_on: A,B where test implementation needs final interfaces

D Integration Verify
  READ: all changed scope
  WRITE: none unless explicit correction task
  depends_on: A,B,C
```

A and B may run in parallel if contracts are frozen and ownership disjoint. C may partially prepare fixtures but final verification waits for A/B. D is an integration barrier.

## Workspace strategy
If the executor supports isolated worktrees/workspaces, independent agents SHOULD operate in isolated branches/worktrees with a governed integration step. If not, Hive Plan restricts concurrency to read-only agents or provably disjoint mutations supported safely by the executor.

Never assume concurrent writes to one working tree are safe.

## Context isolation
Each agent receives only its ContextCapsule slice plus shared stable references. Do not duplicate the full Work Order/repository context into every agent.

Shared canonical constraints remain referenced by digest and are immutable during the execution snapshot.

## Model/profile mapping
The AgentTaskGraph expresses capability/assurance hints, not hard-coded model names:
- FAST_CHEAP;
- BALANCED;
- STRONG;
- HIGH_ASSURANCE where applicable.

Executor-specific model mapping is handled by the UADS/Hades adapter and ModelMesh policy.

## Partial failure
If one task fails:
- independent completed tasks remain recorded but are not automatically trusted/merged;
- downstream dependent tasks pause/cancel;
- unrelated parallel tasks may continue only if policy says their output remains useful;
- retry is bounded and idempotent where possible;
- changed ownership/context invalidates dependent outputs when necessary;
- operator is involved only for governed blockers/authority decisions.

## Cancellation / stale context
A changed canonical source, Context Lock, base/head or operator cancellation invalidates affected tasks. Executor cancellation is requested where supported; any late result from the old execution epoch is quarantined and cannot update canonical state.

## Aggregate completion
The adapter aggregates per-agent Completion Results into one executor Completion Manifest associated with:
- one increment/Work Order;
- one final integrated head SHA;
- one Context Lock;
- all task/result artifact references.

Hive Plan then independently assembles the Evidence Bundle and runs Auto Review.

## Correction execution
Correction Delta may compile into a smaller AgentTaskGraph containing only unresolved findings and impacted tasks. Unaffected work is referenced rather than repeated.

## Efficiency rules
- use multiple agents only when expected wall-clock/rework benefit exceeds coordination cost;
- avoid duplicate repository exploration by supplying precompiled RepoPulse/FIG context;
- keep task prompts incisive and scope-locked;
- parallelize deterministic tests/checks where resource budget permits;
- measure coordination/merge overhead explicitly;
- fall back to one agent when the task is tightly coupled or small.

## Eval requirements
Compare multi-agent vs single-agent baseline on:
- first-pass correctness;
- wall-clock to verified head;
- merge/conflict count;
- duplicate work;
- scope violations;
- correction rounds;
- tokens/API cost;
- evidence completeness;
- human intervention;
- total Verified Outcome Cost.

Multi-agent is not promoted solely because it finishes generation faster.

## Freeze boundary
Freeze executor-neutral capability handshake, AgentTaskGraph semantics, explicit ownership/dependency classes, context isolation, structured Completion Results, safe partial-failure/stale handling, aggregate completion boundary and benchmark-gated parallelism. Exact UADS/Hades command/API syntax, concurrency limits and model names remain adapter/runtime configuration.