# GitHub Governance & Lifecycle

Status: FROZEN — HP-PLAN-002

## Objective
Use GitHub as the canonical, auditable operating backbone for planning, implementation, review, release, recovery, and organizational memory while minimizing manual operator work.

## Principles
1. Every material change has a stable increment identity.
2. `main` contains only reconciled canonical truth and approved implementation.
3. Planning and implementation are both reviewable through branches/PRs.
4. GitHub metadata is structured enough for deterministic automation.
5. Release/version semantics distinguish product maturity from individual commits.
6. Destructive actions remain gated; automation favors reversible operations.
7. Public repositories receive automatic secret/sensitive-data screening before publication.
8. Repository state and Hive Plan state must reconcile by SHA, not by model memory.

## Project bootstrap
For a new project Hive Plan should create or adopt the repository and establish:
- README / Source Hierarchy
- Project Manifest
- canonical Source Pack
- `.github/` templates and governance files
- branch/review policy
- issue taxonomy
- milestone/version strategy
- CI baseline appropriate to the stack
- security/secret scanning policy
- checkpoint and Decisions Ledger
- RAG/index registration

No implementation Work Order is released until mandatory bootstrap sources and lifecycle gates exist.

## Project Manifest
A machine-readable manifest provides deterministic project identity and lifecycle state.

Reference fields:
- project ID / name / type
- canonical repository and default branch
- lifecycle stage
- current release line
- current checkpoint ID
- active planning/implementation increment
- planning freeze state
- implementation authorization state
- risk profile
- memory provider
- executor profile
- CI/review policy profile
- source-pack schema version

## Lifecycle states
Recommended baseline:

`IDEA → DISCOVERY → PLANNING → PLANNING_FROZEN → IMPLEMENTATION → VALIDATION → RELEASE_CANDIDATE → RELEASED → MAINTENANCE`

Transitions are governed and recorded. Invalid jumps are blocked unless an explicit policy exception is approved and recorded.

## Issue taxonomy
Issues are operational objects, not generic notes.

Recommended types:
- `epic` — large outcome/version objective
- `plan` — planning increment
- `feature` — implementation increment
- `bug` — defect
- `security` — security issue
- `infra` — platform/infrastructure
- `debt` — verified technical debt
- `research` — benchmark/spike/evaluation
- `release` — release coordination
- `incident` — production/operational failure when applicable

Recommended state labels are generated from structured workflow state rather than manually curated where possible.

## Milestones
A milestone represents a release/version objective, not a random collection of tasks.

Each milestone should expose:
- target version
- release objective
- Definition of Done linkage
- required planning decisions
- included increments
- blockers
- release risk
- completion evidence

## Branch taxonomy
Default:
- `plan/<id>-<slug>`
- `feat/<id>-<slug>`
- `fix/<id>-<slug>`
- `sec/<id>-<slug>`
- `infra/<id>-<slug>`
- `docs/<id>-<slug>`
- `release/<version>` only when release preparation requires a controlled branch

Avoid long-lived parallel branches unless there is evidence they are necessary.

## Pull requests
One PR should normally map to one governed increment and one primary objective.

Mandatory metadata:
- stable increment/Work Order ID
- linked issue
- base/head SHA
- objective
- scope / out of scope
- risk class
- acceptance criteria
- tests/evidence
- architecture/security/data impact
- known deviations/risks
- checkpoint delta proposal

PR size is controlled by reviewability, not arbitrary line-count limits. Oversized multi-concern PRs are decomposed unless atomicity requires otherwise.

## Planning PRs
Planning decisions affecting canonical truth use planning branches/PRs just like code changes. This preserves an auditable history of why Scope, Architecture, Requirements, ADRs, DoD, or Checkpoints changed.

## Freeze semantics
`FROZEN` means approved canonical baseline, not immutable forever.

A frozen item can only change through:
1. explicit change proposal;
2. impact analysis;
3. affected-source identification;
4. independent critique when required;
5. operator approval when policy requires;
6. superseding ADR/decision entry;
7. checkpoint reconciliation.

Silent replacement is forbidden.

## Versioning policy
Use SemVer where the product/API semantics make it meaningful, with a planning/release policy that distinguishes:
- `MAJOR`: intentional incompatible/breaking product or contract change;
- `MINOR`: backward-compatible functionality;
- `PATCH`: backward-compatible fix/correction.

For pre-1.0 development, version semantics remain explicit; `0.x` does not mean governance-free.

Planning documents may carry schema/version identifiers independently of product SemVer where needed.

## Tags and releases
A release tag is created only after the release gate passes.

Each release record should include:
- version/tag
- exact commit SHA
- release notes generated from governed increments
- included PRs/issues
- migration/rollback notes when applicable
- known limitations
- test/security/benchmark evidence summary
- checkpoint/release receipt

Release tags are never moved silently.

## Patch/hotfix policy
A patch/hotfix follows the same evidence principles but uses the smallest safe path.

For urgent fixes:
- create a dedicated stable increment;
- classify severity/risk;
- reproduce or prove the defect when feasible;
- implement minimal correction;
- run targeted + regression checks proportional to risk;
- review/audit;
- update affected release line and memory records;
- capture root cause and recurrence prevention.

Urgency does not remove evidence requirements.

## Canonical promotion
Material planning/code changes become canonical only after the relevant gate passes and the approved PR is merged into the canonical branch.

After merge Hive Plan:
- records merge SHA;
- verifies canonical files/state;
- promotes approved checkpoint delta;
- refreshes RAG/indexes;
- invalidates stale cached contexts;
- extracts lessons/failures;
- advances the workflow to the next eligible increment.

## Repository health model
Hive Plan should compute repository health from deterministic signals such as:
- branch/PR drift
- stale checkpoints/context locks
- CI health
- unresolved HIGH/CRITICAL findings
- dependency/security alerts when available
- documentation/code mismatch
- test/build status
- pending migrations/recovery obligations
- unreviewed canonical changes
- release/version inconsistency

The cockpit exposes health with causes, not just a green/red badge.

## Automation boundaries
GitHub Steward may automatically perform reversible low-risk actions allowed by policy, such as:
- create branches/issues/PRs
- update planning metadata
- apply labels
- link evidence
- create release drafts
- refresh checkpoints/index state after approval

Operator approval remains mandatory for configured destructive or exceptional actions such as:
- force-push/history rewrite
- destructive branch/repository operations
- security-policy exceptions
- contested release despite blocking evidence
- irreversible migrations or equivalent high-impact transitions

## Public repository safeguard
Before any content is committed/pushed to a public repository, perform deterministic and heuristic checks for:
- tokens/API keys/passwords/private keys
- `.env`/secret files
- sensitive personal/business information
- local paths or dumps that should remain private
- generated artifacts containing secrets
- credentials embedded in logs/test fixtures

A failed secret/sensitive-data gate blocks publication.

## Planning-history traceability
Given any released behavior, Hive Plan should be able to traverse:
`release → commit → PR → Work Order → issue → decision/requirement → checkpoint → evidence → review/audit → lessons/failures`.

The reverse path should also be available when practical.

## Quality/speed principle
GitHub governance must reduce coordination cost, not create ceremony. Fields, checks, and artifacts exist only when they improve traceability, correctness, automation, reuse, or measurable delivery speed.
