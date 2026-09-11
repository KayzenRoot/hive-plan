# Hive Plan

**Hive Plan** is the local-first software planning, governance, review, and engineering control cockpit of the Hive Project ecosystem.

> Status: **V1 PLANNING / FROZEN FOUNDATION**  
> Product type: local-first, single-user, Docker-based engineering system  
> Canonical source of truth: this GitHub repository

## Mission

Replace the current manual planning/review loop across chat, Codex, and GitHub with a specialized engineering system that plans professionally, preserves project truth, produces verifiable Work Orders, observes execution, reviews evidence automatically, audits changes independently, and maintains checkpoints.

## V1 product loop

```text
DISCUSS / INTERVIEW
      ↓
PLAN / ARCHITECT
      ↓
CANONICALIZE IN GITHUB
      ↓
WORK ORDER COMPILER
      ↓
CODEX (external executor)
      ↓
GITHUB + CI + EVIDENCE
      ↓
AUTO REVIEW
      ↓
INDEPENDENT AUDIT
      ↓
APPROVED | CORRECTION REQUIRED | BLOCKED
      ↓
CHECKPOINT / NEXT NECESSARY INCREMENT
```

## Frozen V1 foundations

- Local-first Docker application; no public SaaS requirement for V1.
- GitHub is the project source of truth.
- Hive V1 is the preferred memory/RAG provider, with an internal local-RAG fallback behind a provider contract.
- UADS/Hades V1 and UGAS V1 may be integrated when they materially improve planning, review, execution, observability, or asset workflows.
- Cheap LLM by default; stronger models are escalated only for complexity/risk.
- Aggressive provider prompt caching, local context cache, RAG, deduplication, context budgeting, and delta context.
- Codex remains the external implementation executor in V1.
- Completion claims are never accepted as proof; evidence is independently verified.
- Planning is a first-class product capability and is governed by specialized professional agents.
- The UI is a dark, high-technology command cockpit with project, GitHub, agent, token/cost, review, evidence, health, and progress telemetry.

## Canonical documentation

Start with [`docs/00-source-hierarchy.md`](docs/00-source-hierarchy.md). It defines which source wins when information conflicts.

## Current state

No implementation increment is authorized yet. The project is intentionally in structured planning until the V1 planning freeze is reached.
