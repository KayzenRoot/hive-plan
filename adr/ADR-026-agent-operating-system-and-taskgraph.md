# ADR-026 — Governed Agent Operating System and AgentTaskGraph

Status: ACCEPTED  
Date: 2026-09-11  
Increment: HP-PLAN-007

## Context
Hive Plan must use professional specialist agents for planning, execution coordination and review while avoiding uncontrolled swarms, overlapping writes, ad-hoc personas and executor-specific lock-in.

## Decision
Adopt the governed Agent Operating System defined by:
- TeamComposer;
- Capability Ledger;
- ExpertiseGraph;
- CouncilBus;
- Dissent Ledger;
- AgentGovernor;
- 30 canonical V1 agent charters A-001..A-030;
- machine-readable `agents/registry.yaml`;
- executor-neutral AgentTaskGraph with explicit dependencies, WRITE_SET/READ_SET/WATCH_SET, ContextCapsules, proof obligations and STOP CONDITION;
- dynamic ConcurrencyGovernor;
- single-agent fallback when multi-agent benefit is not proven.

Canonical Work Orders remain executor-neutral. UADS/Hades/Codex adapters render execution plans but do not invent canonical agent roles or alter project semantics.

## Consequences
Positive:
- consistent senior behavior;
- auditable agent responsibilities;
- safe parallelism;
- lower duplicate context/work;
- replaceable executors/models;
- measurable agent/team performance.

Costs/risks:
- orchestration complexity;
- need for capability discovery and task ownership;
- coordination overhead if team composition is poor.

Mitigation: benchmark multi-agent patterns against single-agent Verified Outcome Cost and demote patterns that do not improve results.

## Rejected alternatives
- free-form ad-hoc agents created by executor;
- always-on large swarms;
- fixed agent count/concurrency;
- overlapping concurrent writes to one workspace without proven conflict safety.
