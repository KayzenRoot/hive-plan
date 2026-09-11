# ADR-028 — HIVE / UGAS / UADS Principal Ecosystem Specialists

Status: ACCEPTED  
Date: 2026-09-11  
Increment: HP-PLAN-008

## Context
Hive Plan must operate three adjacent systems correctly: HIVE for context/memory/intelligence, UGAS for multimodal production, and UADS for engineering orchestration. Generic software agents do not contain enough system-specific gate, durability, evidence and operational knowledge to use these systems safely and efficiently.

## Decision
Add three canonical principal specialists authored in Hive Plan:
- A-031 Principal HIVE Systems Specialist;
- A-032 Principal UGAS Production Systems Specialist;
- A-033 Principal UADS Orchestration Specialist.

Their charters are grounded in live repository research across HIVE/HIVE V2, UGAS/UGAS V2 and UADS/UADS V2. They refresh repository/checkpoint fingerprints before consequential advice and cooperate through the Tri-System Harmony Protocol.

Responsibility boundary:
- HIVE owns project/context/memory/intelligence substrate concerns;
- UADS owns engineering orchestration/execution coordination concerns;
- UGAS owns multimodal production/artifact pipeline concerns;
- Hive Plan remains planning/governance/cockpit/review authority.

Cross-system plans use versioned adapters/contracts and must not silently transfer authority between systems.

## Consequences
Positive:
- safer integrations;
- faster diagnosis and operation;
- less repeated repository rediscovery;
- better skills tailored to real systems;
- clearer subsystem ownership in the cockpit;
- stronger stale-context detection.

Costs:
- three more governed agent profiles;
- need to refresh system knowledge as repositories evolve;
- cross-system skills require multi-specialist review.

## Guardrails
- repository source hierarchy outranks agent memory;
- external research is untrusted evidence;
- exact gates/SHAs/evidence boundaries remain binding;
- specialists cannot self-grant new authority through skills;
- cross-system mutations require explicit ownership/contracts;
- derived caches/indexes never gain authority over canonical data.
