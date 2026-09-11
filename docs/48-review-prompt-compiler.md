# Review & Correction Prompt Compiler

Status: FROZEN — HP-PLAN-006

## Mission
Generate concise, scope-locked prompts for UADS/Codex that tell each agent exactly what to inspect or change, why, what evidence is required and when to stop.

## Prompt principle
Prompts are compiled from canonical structured artifacts. They are not handwritten narratives and do not become a second source of truth.

## Review prompt structure
Each review agent receives only:
1. ROLE and authority boundary;
2. immutable snapshot identity;
3. assigned semantic slice;
4. relevant requirements/contracts/ADRs;
5. deterministic evidence already available;
6. exact review questions/proof obligations;
7. known historical failures relevant to this slice;
8. prohibited/unrelated scope;
9. normalized finding output schema;
10. STOP CONDITION.

## Incisive rules
- Do not review unrelated repository areas.
- Do not repeat lint/formatter findings already deterministically resolved.
- Do not invent files, behavior or test results.
- Do not recommend refactors unless required to resolve a confirmed defect or frozen architecture violation.
- Distinguish introduced regression from pre-existing issue.
- Prefer root-cause finding over multiple symptom comments.
- Every blocking finding must include a concrete failure condition/evidence path.
- If assigned scope passes, return PASS with explicit coverage and stop.

## Correction prompt structure
Correction prompts are compiled from Correction Delta and contain:
- exact findings to resolve;
- severity/order;
- affected files/symbols/contracts;
- required fix behavior, not speculative implementation detail unless architecture dictates it;
- required tests/evidence per finding;
- known traps/failure history;
- explicit OUT OF SCOPE;
- UADS agent decomposition only for independent work;
- dependency/merge ordering between agents;
- Completion Manifest/Evidence Bundle obligations;
- STOP CONDITION.

## UADS task graph
When parallel work is safe, emit a dependency graph rather than a flat list:
```text
A backend/auth fix ─┐
                    ├─> D integration verification
B frontend state ───┤
C targeted tests ───┘
```

Agents with overlapping mutable symbols are serialized unless UADS supplies a proven conflict-safe workspace strategy.

## Prompt compression
Stable rules and schemas are referenced/cacheable. Dynamic prompt body contains only the current delta, impacted context and agent-specific slice. Repeated correction rounds use prior artifact digests and transmit changed findings/context only.

## Prompt quality gates
Before execution, CompileGuard verifies:
- every agent has one bounded objective;
- no conflicting file ownership without dependency policy;
- every blocking finding maps to a correction criterion;
- every criterion maps to proof/test evidence;
- no scope expansion was introduced by rendering;
- snapshot/context references are current;
- STOP CONDITION is executable;
- Completion/Evidence obligations are present.

## Freeze boundary
Freeze structured incisive prompt shape, per-agent context isolation, task dependency graph, no-unrelated-refactor rule, evidence obligations and delta-first correction rendering. Exact UADS invocation syntax/model assignment remains the next integration increment.