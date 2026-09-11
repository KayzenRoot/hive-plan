# Data Model — Planning Baseline

The exact physical schema is not frozen. This document defines domain entities so future persistence choices do not leak into product logic.

## Core entities
- Project
- RepositoryConnection
- CanonicalSource
- SourceFingerprint
- Decision / ADR
- Requirement
- ScopeItem
- Checkpoint
- Conversation / PlanningSession
- AgentRole / AgentRun
- WorkOrder
- CorrectionDelta
- ExecutionManifest
- EvidenceItem / EvidenceBundle
- PullRequestSnapshot
- CIObservation
- ReviewRun
- Finding
- AuditRun / ReviewReceipt
- ContextPackage
- RetrievalRecord
- LLMCall
- CostRecord
- WorkflowEvent
- IntegrationHealth

## Identity rules
- Project, Work Order, Review, Audit, and Checkpoint IDs are stable and globally unique within Hive Plan.
- Git SHAs are external immutable identifiers and must not be replaced by mutable branch names in evidence.
- Review receipts bind a verdict to exact source fingerprints, policy version, and Git head SHA.

## Temporal/audit rules
Material state transitions retain timestamps and provenance. Canonical history is append-oriented where practical; corrections/supersessions should be explicit rather than silent overwrites.

## Isolation
All retrieval/memory/cost/evidence records are project-scoped. Cross-project retrieval requires explicit policy and is disabled by default.

## Persistence decision gate
PostgreSQL is the initial default candidate. Vector capabilities, Redis, and specialized vector stores require benchmark evidence before becoming mandatory dependencies.
