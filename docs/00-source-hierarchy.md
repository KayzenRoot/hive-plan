# Source Hierarchy

Status: FROZEN FOUNDATION

When sources conflict, Hive Plan MUST resolve truth in this order:

1. Current approved Checkpoint
2. Approved Decisions Ledger / ADRs
3. Approved Scope
4. Definition of Done
5. Architecture
6. Requirements
7. Security / Integration / Data contracts
8. Work Order and acceptance criteria for the active increment
9. Git state, CI results, tests, diffs, and evidence
10. Backlog and planning notes
11. Chat history and model memory

Git, executable code, tests, CI, and verified evidence override unsupported model claims. Chat memory is never canonical.

## Change control

A frozen decision is not overwritten silently. Material changes require an explicit decision record, impact analysis, and checkpoint delta. If a critical source changes during an active Work Order, the context is STALE until reconciled.
