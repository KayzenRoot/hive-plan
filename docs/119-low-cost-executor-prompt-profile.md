# HP-PLAN-010 — Low-Cost Executor Prompt Profile

Status: PROPOSED

## Mission
Produce concise, implementation-heavy executor prompts that reduce reasoning burden, token consumption and architecture drift when using cheaper coding models.

## Operating assumption
The executor is not the system architect. It is a bounded implementation worker operating from a validated Work Order + Implementation Blueprint + Context Lock.

## Prompt shape
A generated executor prompt SHOULD follow this order:

1. EXECUTION IDENTITY
   - Project / Work Order / branch / exact base SHA.

2. NON-NEGOTIABLE CONTRACT
   - objective;
   - acceptance criteria;
   - out-of-scope;
   - STOP CONDITION;
   - destructive-action prohibition;
   - source/context lock.

3. IMPLEMENTATION MAP
   - ordered steps;
   - exact files/symbols likely to touch;
   - responsibilities per file;
   - interfaces/types/signatures/schema sketches;
   - pseudocode/algorithm where needed.

4. EDGE CASES + FAILURE PREVENTION
   - known prior failures;
   - validation/error/transaction/retry/idempotency rules;
   - security/performance constraints.

5. TEST MAP
   - exact tests to create/change;
   - fixtures/scenarios;
   - negative/edge cases;
   - required build/lint/typecheck/security/e2e gates.

6. EVIDENCE MAP
   - commands/checks/artifacts to collect;
   - exact-head Git evidence;
   - Completion Manifest fields.

7. DEVIATION RULE
   - do not invent architecture;
   - if repo reality conflicts, choose safest minimal correction and document deviation;
   - stop/escalate only when a blocking ambiguity cannot be resolved from canonical sources.

8. OUTPUT CONTRACT
   - concise completion receipt;
   - files changed;
   - tests/evidence;
   - deviations;
   - unresolved blockers.

## Compression rules
- Reference stable canonical artifact IDs/digests instead of restating them.
- Do not include motivational prose.
- Do not repeat requirements in multiple sections.
- Prefer tables/structured lists for file/task/test maps.
- Include code/pseudocode only for nontrivial/high-risk behavior.
- Include exact excerpts only when the executor cannot safely retrieve them from the locked repository.

## Cheap-executor tuning
When executor capability is below preferred reasoning tier, increase blueprint depth rather than prompt verbosity indiscriminately. Favor G2/G3 precise instructions, deterministic checks and narrower task slices.

## Model-specific adaptation
ExecutorFit may adapt syntax/format for a provider/model, but semantic contract remains identical. No model receives permission to reinterpret scope or lower evidence requirements.

## Example implementation directive
Instead of: `Implement reconnect logic for SSE.`

Prefer:
`In packages/api-client/src/sse-client.ts add reconnect state machine with states CONNECTING, OPEN, BACKOFF, SNAPSHOT_REQUIRED, CLOSED. Preserve last accepted watermark. On disconnect use bounded exponential backoff with jitter. Send last watermark on reconnect. If server cannot prove gap completeness, discard queued deltas, fetch fresh snapshot, then resume stream. Never coalesce CRITICAL_STATE events. Add unit tests for clean reconnect, missed-gap snapshot recovery, duplicate watermark, stale delta rejection and backoff cap.`

The executor receives decisions, not a blank page.

## Success metrics
- first-pass acceptance rate;
- executor input/output tokens;
- implementation latency;
- correction rounds;
- architecture deviations;
- escaped defects;
- predicted-vs-actual change surface;
- verified outcome cost.

## STOP CONDITION
Freeze only when the prompt profile can be generated from canonical Work Order/Blueprint artifacts and evaluated against cheaper vs stronger executor cohorts.