# Feature Impact Graph (FIG)

Status: PROPOSED FOR FREEZE — HP-PLAN-006

## Mission
Maintain a continuously improving map of which files, symbols, contracts, tests, data objects and runtime paths implement or depend on each product capability. The map accelerates Work Order compilation, impact analysis and focused review.

## Principle
The map is evidence-derived, not manually trusted forever. It evolves from planning predictions plus verified implementation outcomes.

## Graph entities
At minimum:
- FEATURE / CAPABILITY;
- REQUIREMENT / ACCEPTANCE CRITERION;
- ADR / ARCHITECTURE RULE;
- MODULE / PACKAGE;
- FILE;
- SYMBOL;
- API / ROUTE / EVENT / SCHEMA;
- DATABASE TABLE / MIGRATION / QUERY;
- CONFIG / SECRET BOUNDARY;
- TEST / PROOF CHANNEL;
- PR / WORK ORDER;
- FAILURE / REGRESSION;
- DEPLOYMENT / RUNTIME COMPONENT.

## Edge examples
- IMPLEMENTED_BY;
- CALLS / IMPORTS / EXPORTS;
- DEPENDS_ON;
- GUARDED_BY;
- PERSISTS_TO;
- CONTRACTS_WITH;
- TESTED_BY;
- CHANGED_BY;
- BROKE_IN;
- FIXED_BY;
- OBSERVES;
- DEPLOYED_IN;
- SUPERSEDES.

Every edge carries provenance, confidence, first_seen, last_verified, relevant Git SHA/version and source authority.

## Update lifecycle
```text
PLANNING
  ↓ predicted feature/change map
WORK ORDER
  ↓ predicted MUST/LIKELY impact
EXECUTION
  ↓ actual changed symbols/files
REVIEW
  ↓ validated semantic impact
MERGE
  ↓ verified graph delta
POST-MERGE / INCIDENT
  ↓ correction/regression feedback
FIG UPDATED
```

## Predicted vs verified edges
- PREDICTED: generated before execution, useful for guidance.
- OBSERVED: derived from actual Git/AST/runtime/test facts.
- VERIFIED: confirmed by review/evidence.
- STALE: source changed or confidence decayed.
- SUPERSEDED: replaced by newer architecture/implementation.

Review never treats a predicted edge as proof.

## Feature manifests
Each capability may expose a compact machine-readable manifest generated from the graph, for example:
```yaml
feature: authentication.login
entrypoints:
  - src/ui/login/*
  - src/api/auth/login.ts
contracts:
  - contracts/auth/login.schema.json
security_boundaries:
  - session_cookie
  - rate_limit
impacted_runtime:
  - web
  - api
required_tests:
  - auth-login-unit
  - auth-login-integration
  - auth-protected-route-e2e
```

These are derived views, not separate canonical truth.

## Review use
For a changed feature, ReviewScope starts from actual diff nodes and asks FIG for:
- direct implementers;
- downstream consumers;
- public contracts;
- persistence/security boundaries;
- required tests/proofs;
- past regressions;
- high-centrality dependency hubs.

Only relevant graph neighborhoods are expanded into review context.

## Work Order use
The Work Order Compiler uses FIG to propose:
- likely files/symbols;
- do-not-touch boundaries;
- related contracts;
- mandatory tests;
- prior failure constraints;
- specialist agents likely required.

## Drift detection
After each verified merge compare predicted graph delta vs actual verified delta. Unexpected touched nodes trigger:
- graph correction;
- change-surface model feedback;
- possible architecture/documentation drift finding;
- review-policy update candidate if a blind spot is repeated.

## Centrality/risk signals
Nodes accumulate operational metadata such as:
- change frequency;
- defect frequency;
- review finding density;
- fan-in/fan-out;
- security/data sensitivity;
- incident history;
- test coverage confidence.

This feeds Repository Temperature Map and review depth, but cannot lower mandated assurance.

## Performance
The graph must be incremental and content-addressed. Recompute only affected nodes/edges where practical. Store compact IDs/fingerprints and retrieve bounded neighborhoods rather than loading the entire graph into LLM context.

## Source of truth boundary
GitHub canonical docs/contracts/ADRs remain authoritative for policy and approved design. FIG is a derived engineering intelligence layer with provenance back to canonical sources and verified code/evidence.

## Freeze boundary
Freeze persistent feature→code→contract→test→failure graph semantics, provenance/status model, predicted-vs-verified lifecycle and automatic update after verified merge. Exact graph database/storage implementation remains an architecture benchmark decision.