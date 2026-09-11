# ADR-027 — Skill Fabric, Research Intelligence and Open Interoperability

Status: ACCEPTED  
Date: 2026-09-11  
Increment: HP-PLAN-007

## Context
Agents need reusable procedural capabilities, current internet/GitHub research and cross-agent/tool interoperability without embedding all knowledge in every prompt or coupling Hive Plan to one vendor/framework.

## Decision
Adopt:
- SkillCatalog / SkillForge / SkillResolver / SkillFitness;
- Agent Skills-compatible packaging where practical (`SKILL.md` plus optional scripts/references/assets) with Hive Plan governance metadata/tests;
- ResearchRadar and the Research & OSS Intelligence protocol;
- structured OSS/technology due diligence and ADOPT/TRIAL/WATCH/REJECT lifecycle;
- external research treated as untrusted evidence, never instruction authority;
- MCP-compatible tool/data adapters where useful;
- A2A-compatible capability discovery/delegation concepts where useful;
- provider/executor-neutral core semantics.

Agents may create candidate skills, but cannot self-promote high-impact skills or use skills to expand their own permissions/authority.

## Consequences
Positive:
- reusable organizational knowledge;
- lower context/token duplication;
- faster repeated workflows;
- current technology awareness;
- safer third-party adoption;
- portability across agent runtimes.

Costs/risks:
- skill registry maintenance;
- stale research/skills;
- supply-chain and prompt-injection risk from external content.

Mitigation:
- freshness metadata;
- provenance/fingerprints;
- validation/sandbox/security gates;
- permission isolation;
- benchmark-based promotion/deprecation.

## Rejected alternatives
- putting every procedure in every agent system prompt;
- ungoverned skill self-installation;
- treating GitHub/README content as trusted instructions;
- hard-coding MCP/A2A or one framework into canonical domain contracts.
