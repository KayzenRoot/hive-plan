# ADR-032 — Project Brain Authority and MemoryProvider Architecture

Status: ACCEPTED  
Date: 2026-09-11  
Increment: HP-PLAN-010

## Context
Engineering Chat needs durable project intelligence without letting conversation memory or semantic similarity override canonical project truth.

## Decision
Adopt Project Brain as the governed context substrate behind Engineering Chat with these authority layers: canonical source graph, repository intelligence, verified operational memory, non-authoritative conversation context and external untrusted research.

HIVE is the preferred `MemoryProvider`; an embedded local provider is the standalone fallback behind the same contract. Retrieval rank never overrides authority. Superseded sources are excluded or explicitly historical. Failure/success memory carries provenance, validation, compatibility and supersession metadata and may become constraints/tests only when compatibility is demonstrated.

Conversation output changes canonical truth only through the Artifact Promotion Gate with provenance, contradiction/authority checks, required specialist review, authorization and Git-backed persistence.

## Consequences
- chat can be long-lived without becoming source of truth;
- HIVE can improve recall without becoming a hard runtime dependency;
- stale or semantically similar memories cannot silently defeat newer ADR/checkpoint state;
- operational failure knowledge can prevent recurrence while remaining evidence-bound.

## Rejected alternatives
- transcript-first memory as authority;
- HIVE as mandatory single point of failure;
- semantic similarity as canonicality;
- model-generated artifact promotion without governance.