# Test & Benchmark Plan

## Risk posture
Baseline V1: STANDARD, elevated to ELEVATED/HIGH_ASSURANCE for secrets, privileged GitHub actions, security-sensitive flows, irreversible operations, migrations, or recovery.

## Test layers
- Unit: policies, state machines, parsers, context budgeting, routing, redaction, Work Order compiler.
- Integration: GitHub adapter, LLM providers, Hive MemoryProvider, local RAG, persistence, event/outbox.
- Contract: provider/adapters and machine-readable completion/evidence schemas.
- End-to-end: discuss → plan → Work Order → simulated executor completion → GitHub/CI observation → review → audit → checkpoint/correction.
- Fault injection: API outage, rate limit, stale PR head, partial CI failure, corrupted manifest, restart mid-review, duplicate event.
- Security: secret leakage, prompt injection, malicious repository content, privilege boundary tests.
- Recovery: backup/restore, event replay, restart/resume, database migration recovery.

## Review quality evals
Maintain a benchmark corpus of representative software-planning/review cases with seeded defects and expected outcomes. Measure:
- defect recall by severity;
- false approval rate;
- false positive rate;
- architecture/requirement violation detection;
- correction quality;
- context/token usage;
- model escalation frequency;
- latency and total cost.

## LLM router evaluation
Compare candidate profiles on the same corpus. Promote cheaper profiles only when quality remains within approved thresholds. Stronger model escalation is mandatory when assurance policy requires it, independent of cost.

## UI/performance
Measure first interactive load, chat streaming responsiveness, large project/event-list behavior, animation/GPU impact, memory consumption, and reduced-motion behavior.

## Acceptance budgets
Exact numeric budgets are intentionally OPEN until baseline measurements are collected during preflight planning.
