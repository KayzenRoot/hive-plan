# GitHub Governance

## Purpose
Make each managed repository auditable, navigable, releaseable, and suitable as a canonical project source.

## Baseline repository expectations
- README and Source Hierarchy.
- Versioned canonical docs appropriate to project type.
- Branch-based changes and pull requests for governed increments.
- Stable Work Order IDs referenced by branch/PR/evidence/checkpoint.
- Issues for actionable work; planning notes alone do not masquerade as approved scope.
- PR template with objective, scope, evidence, tests, risks, checkpoint delta.
- Semantic versioning policy where the artifact is versioned/released.
- Tags/releases only after release gates.
- CI/checks appropriate to language/risk.
- No force-push/history rewrite by automation by default.

## Hive Plan GitHub Steward
The Steward may create and organize repositories when configured token permissions allow it. It can propose repository structure, documentation, issues, branches, PRs, tags/releases, and version governance, but must obey project scope, policy, and destructive-action controls.

## Repository creation protocol
Before creating a new repository, capture at minimum: project identity, visibility, purpose, ownership, source hierarchy, initial scope, security/secrets constraints, versioning strategy, and expected integrations. Then bootstrap the canonical Source Pack before implementation.

## Versioning
Default recommendation for versioned applications/libraries: Semantic Versioning (`MAJOR.MINOR.PATCH`) with pre-1.0 development allowed. Release policy is project-specific and may supersede this through an ADR.

## PR gates
A governed PR should not become APPROVED solely because CI is green. Approval considers Work Order acceptance criteria, architecture, requirements, security/risk obligations, evidence, unresolved review findings, and checkpoint correctness.

## Public-repository rule
Public repositories must be treated as globally readable. Hive Plan must perform secret/sensitive-data checks before publishing generated documentation or artifacts and must never assume low visibility equals confidentiality.
