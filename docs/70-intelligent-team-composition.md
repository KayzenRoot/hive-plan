# Intelligent Team Composition & AgentTaskGraph Policy

Status: PROPOSED FOR FREEZE — HP-PLAN-007

## Mission
Choose the smallest team and execution graph that minimizes total time/cost to a verified correct outcome without sacrificing required expertise or assurance.

## No swarm-by-default
Hive Plan MUST NOT create multiple agents merely because UADS supports them. Multi-agent work introduces coordination, duplicated context, conflicting writes and correlated errors.

Default rule:
`single agent unless distinct expertise or provable parallelism creates positive verified value`.

## TeamComposer inputs
- task/increment objective;
- risk and QualityFloor;
- Feature Impact Graph;
- Work Order semantic scope;
- affected architecture/data/security/UI/infra domains;
- dependency DAG;
- predicted WRITE/READ/WATCH sets;
- prior similar-task outcomes;
- agent benchmark history;
- required skills/tools;
- model/provider health/budget;
- CPU/RAM/GPU/IO/network budget where local tools execute;
- expected serial duration and coordination overhead.

## Agent activation classes
### REQUIRED
Policy/risk/domain makes specialist participation mandatory.

### BENEFICIAL
Expected verified-outcome improvement exceeds activation/coordination cost.

### OPTIONAL
May be used for experiments/shadow evaluation but cannot delay main path.

### EXCLUDED
No material contribution to current semantic scope.

## Team Utility model
A candidate team is ranked by expected:
```text
Team Utility =
  Quality Gain
+ Wall-clock Saving
+ Risk Reduction
+ Rework Reduction
- Coordination Cost
- Context Duplication Cost
- Merge/Conflict Risk
- Tool/Model Cost
- Resource Contention
```

Exact numeric weights are benchmarked later. Hard QualityFloor/authority requirements are constraints, not tunable weights.

## Parallelism qualification
A pair of mutating tasks is parallel-safe only when:
- dependency ordering allows it;
- mutable ownership is disjoint or isolated workspaces make integration safe;
- shared contracts are frozen/stable for the execution epoch;
- changes do not rely on mutable global state without coordination;
- integration proof exists.

If uncertain, serialize.

## Concurrency governor
`ConcurrencyGovernor` sets the active-agent limit dynamically using:
- executor-advertised capability;
- local hardware/resource pressure;
- API/model rate limits;
- token/cost budget;
- task dependency width;
- worktree/workspace availability;
- historical conflict rate.

Concurrency is a resource allocation decision, not a fixed configuration value.

## AgentTaskGraph compiler
Compile canonical Work Order into DAG nodes containing:
- task_id;
- agent_id/required capability;
- objective;
- input artifact refs;
- dependency IDs;
- WRITE_SET;
- READ_SET;
- WATCH_SET;
- ContextCapsule;
- required skills;
- allowed tools;
- proof/test obligations;
- budget/time limits;
- output schema;
- STOP CONDITION;
- integration strategy.

## Execution patterns
### Pattern S — Single Senior Agent
Small/tightly coupled changes. Lowest coordination cost.

### Pattern P — Parallel Specialists
Distinct domains with disjoint ownership, e.g. backend auth + frontend login view under a frozen contract.

### Pattern W — Writer + Read-only Critics
One mutating agent, specialists inspect/advise in parallel. Useful when shared code makes multiple writers risky.

### Pattern B — Barrier Pipeline
Parallel preparation followed by one integration/test barrier.

### Pattern R — Research Cell
Research/OSS agent + domain specialist + Security/Architect critic where technology adoption is consequential.

### Pattern H — HIGH_ASSURANCE Council
Primary specialist + independent specialist/critic + Auditor. Mutation remains controlled/serialized unless safety is proven.

## Planning council composition
Planning work usually uses read-only parallelism more freely:
- Interviewer/Lead frames question;
- domain agents independently analyze assigned aspects;
- Research Agent supplies current external evidence;
- Innovation Scout proposes alternatives;
- Lead synthesizes;
- Auditor/red team challenges when required;
- operator resolves governed decisions.

## Skill-aware routing
Before activating a new specialist, TeamComposer checks whether the current agent can safely satisfy the need through an approved skill. Conversely, a skill cannot substitute for a specialist when policy requires independent domain authority.

## Research-aware routing
ResearchRadar prevents duplicate browsing. One Research Agent can gather primary evidence and distribute evidence refs to multiple specialists, reducing cost/context duplication.

## Agent Capability Cards
Each agent exposes a portable capability card derived from `agents/registry.yaml`:
- role/capabilities;
- supported task classes;
- tools/skills;
- assurance ceiling/floor;
- input/output contracts;
- availability/health;
- compatibility/version.

Design SHOULD remain compatible with the concepts of open agent-discovery/delegation standards such as A2A without making A2A a V1 runtime dependency.

## Tool interoperability
Agent tool/data access SHOULD be isolated behind a provider-neutral tool adapter and can adopt MCP-compatible adapters where useful. Canonical task semantics never depend on MCP-specific transport details.

## Conflict prevention
- ownership reservation before mutating tasks start;
- no overlapping WRITE_SET without explicit integration policy;
- file overlap is a warning, symbol/semantic overlap is stronger evidence;
- dependency/interface changes emit invalidation events to downstream tasks;
- late/stale task results are quarantined;
- integration agent never silently resolves semantic conflicts.

## Handoff protocol
A completed upstream agent publishes a structured Handoff containing:
- output artifact refs;
- contract/interface changes;
- assumptions confirmed/invalidated;
- evidence;
- new risks;
- downstream invalidations;
- required next checks.

Dependent agents receive delta context, not the upstream agent's entire transcript.

## Adaptive learning
Track per task class:
- single vs multi-agent success;
- wall-clock speedup;
- coordination time;
- conflicts;
- duplicate work;
- token/tool cost;
- correction rounds;
- escaped defects;
- specialist unique-finding yield.

TeamComposer policies are promoted only when they improve Verified Outcome Cost and do not regress quality.

## Shadow team experiments
New agent/team patterns may run in read-only shadow mode against historical/current artifacts to evaluate finding quality or recommendation utility without affecting canonical state.

## STOP CONDITION
Team composition is complete when:
- all mandatory expertise/assurance roles are covered;
- every task has a qualified owner;
- dependencies and ownership are conflict-safe;
- context/tool/skill needs are satisfied;
- coordination cost is justified by expected verified benefit;
- fallback path exists for executor capability loss.

## Freeze boundary
Freeze minimal-sufficient team selection, activation classes, Team Utility concept, dynamic ConcurrencyGovernor, AgentTaskGraph semantics, standard execution patterns, capability cards, skill/research-aware routing, ownership reservation, structured handoffs, shadow evaluation and benchmark-driven team learning. Exact scoring weights/concurrency limits remain eval-derived configuration.