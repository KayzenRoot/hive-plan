# Definition of Done — Hive Plan V1

V1 is complete only when all NECESSARY scope items are objectively satisfied and evidenced.

## Product
- Engineering chat supports discussion, discovery, planning, Work Order generation, review/audit results, and continuity.
- Specialized planning roles operate under documented authority rules.
- GitHub is used as canonical project truth.
- Hive V1 memory/RAG integration works, with tested local-RAG fallback.
- Codex Work Orders are generated with stable IDs and required sections.
- Execution completion automatically triggers eligible review without manual operator prompting.
- Review/audit produces APPROVED, CORRECTION REQUIRED, or BLOCKED with evidence.
- Safe correction deltas are generated automatically.
- Checkpoints preserve continuation across restarts/chats.

## GitHub
- Token integration works without exposing token material.
- Required supported operations for repo governance are validated against a test repository.
- Repository organization/versioning policy is documented and exercised.

## Quality
- Unit, integration, and end-to-end tests for critical workflows pass.
- Lint/typecheck/build pass.
- Auto-review idempotency, stale-head cancellation, retry, dead-letter, and recovery are tested.
- Security threat model and secret/prompt-injection controls are tested.
- Data persistence/recovery is validated.
- Performance and LLM-cost benchmarks meet approved budgets.

## UI
- Early cockpit vertical slice is evolved into the final V1 cockpit.
- Core project, Work Order, GitHub, review, health, token/cost, agent, and checkpoint state is visible.
- Reduced-motion/accessibility and failure states are covered.

## Deployment
- Local Docker/Compose bootstrap is repeatable from a clean machine with documented prerequisites.
- Persistence and backup/restore procedures are validated.
- Upgrade/rollback or roll-forward strategy is documented and tested where applicable.

## Evidence
Final release requires an evidence bundle containing release SHA/tag, tested environment, test/lint/typecheck/build results, security evidence, benchmark/cost evidence, known risks, recovery evidence, and final checkpoint.

No HIGH/CRITICAL known defect may remain open at V1 completion.
