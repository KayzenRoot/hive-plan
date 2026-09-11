# Integration Contracts

## Hive V1
Role: preferred MemoryProvider/RAG backend.

Required conceptual operations:
- ingest/upsert canonical sources with fingerprints;
- semantic/hybrid retrieval;
- project-scoped memory isolation;
- retrieve decisions/checkpoints/context by authority/freshness;
- support delta/freshness-aware context where available;
- expose health/capability metadata.

Hive Plan must remain functional with an embedded local-RAG fallback if Hive V1 is unavailable.

## UADS / Hades V1
Role: optional engineering/review/runtime integration where it materially improves current workflows.

Status: exact product/repository/version/API contract is OPEN and must be reconciled against the currently deployed V1 before implementation. Hive Plan must not invent capabilities that are not verified in that source.

## UGAS V1
Role: optional visual/asset generation support, especially for UI concept assets or future cockpit enhancements. It is not a hard dependency of the V1 planning/review core.

## Codex
Role: external implementation executor.

Hive Plan emits versioned Work Orders/correction deltas; Codex returns code through Git/GitHub plus a completion/block signal and evidence references. Executor statements are never canonical proof.

## GitHub
Role: canonical versioned project truth and execution/review coordination surface.

Authentication in V1: locally stored token/PAT with configurable privileges and strict redaction.

## LLM providers
All model providers are accessed through a normalized LLM Gateway. Domain workflows request capability profiles rather than hard-coded model names.
