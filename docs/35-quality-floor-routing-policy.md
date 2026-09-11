# QualityFloor & Routing Policy

Status: PROPOSED FOR FREEZE — HP-PLAN-005

## Mission
Guarantee that Hive Plan never reduces engineering assurance merely to reduce model/API spend. Routing is an optimization problem only after hard quality, privacy, capability and governance constraints are satisfied.

## Core principle: optimize Verified Outcome Cost
The router MUST optimize the expected total cost of reaching a verified outcome, not the price of the next model call.

`VerifiedOutcomeCost = provider_cost + expected_rework_cost + expected_retry_cost + latency_penalty + defect_risk_penalty + human_intervention_penalty`

A cheaper model that historically causes more correction rounds may be economically worse than a stronger model used once.

## Capability tiers
These are provider-neutral capability/assurance classes, not permanent model names.

### T0 — DETERMINISTIC
Git, schema validation, AST, static analysis, cache, tests, CI, policy/state machine, exact retrieval. Use whenever the task is decidable without semantic model reasoning.

### T1 — FAST_CHEAP
Extraction, classification, query expansion, lightweight conversation, deterministic-result explanation, low-risk summarization and simple routing support.

### T2 — BALANCED
Normal discovery, requirements synthesis, bounded planning, Work Order drafting, moderate cross-file reasoning and standard review triage.

### T3 — STRONG
Architecture, difficult trade-offs, complex cross-domain planning, consequential review, non-trivial security reasoning, difficult root-cause analysis and high-blast-radius Work Order critique.

### T4 — HIGH_ASSURANCE
A governed assurance mode rather than merely a single expensive model. It may combine T3/stronger reasoning, independent critique/adjudication, deterministic evidence, stricter source recall, broader tests and explicit operator gates.

## Hard eligibility gate
Before scoring price/latency, a route must satisfy:
- minimum capability tier;
- task-required tool/structured-output features;
- minimum context capacity;
- privacy/data-routing policy;
- supported artifact/schema versions;
- provider/model health;
- project/vendor policy;
- required reasoning/vision/modalities where applicable;
- assurance independence requirements.

Ineligible routes are removed before economic optimization.

## Default minimum floors by task class
These are baseline floors and may be raised by risk/ambiguity/novelty.

| Task | Default floor |
|---|---|
| deterministic validation / exact facts | T0 |
| classification / extraction / navigation | T1 |
| ordinary engineering conversation | T1 |
| discovery questions | T1/T2 |
| requirements and bounded planning | T2 |
| Work Order synthesis | T2 |
| architecture decision | T3 |
| security-sensitive design | T3 |
| standard code/PR review triage | T2 |
| consequential final review/audit | T3 |
| HIGH_ASSURANCE approval path | T4 |

## Floor raisers
Raise one or more tiers when any of these increase materially:
- ambiguity;
- novelty / weak prior evidence;
- irreversible impact;
- data-loss potential;
- security boundary;
- migration risk;
- money/signing/privileged authorization;
- broad dependency reach;
- cross-domain complexity;
- weak source grounding;
- disagreement between evidence sources;
- repeated prior failures;
- low model/project historical success for this task class.

No floor-lowering signal can override a policy-mandated HIGH_ASSURANCE class.

## Acceptance is evidence-based, not self-confidence-based
Model-reported confidence is advisory only. A response may be accepted when required evidence and validators pass and the route meets its floor. Escalate when:
- required sources are missing;
- deterministic validators disagree with the model;
- acceptance criteria remain ambiguous;
- independent critic identifies a material issue;
- source-grounding score falls below policy;
- output schema/tool contract fails;
- answer changes materially under a small evidence-preserving perturbation;
- historical route reliability for the task is below threshold;
- a HIGH/CRITICAL finding remains unresolved.

## Draft → critic → adjudicator pattern
Consequential tasks should avoid paying T3/T4 for every token.

Possible governed flow:
```text
T1/T2 draft or extraction
        ↓
deterministic evidence checks
        ↓
T3 independent critique
        ↓
accept / correction / adjudicate
```

For HIGH_ASSURANCE, generation and final authorization SHOULD be independently routed where practical. Independence may mean another model profile, another model family/provider, or a deterministic/agent review path depending on the task. Provider diversity is a future enhancement, not a mandatory V1 dependency.

## Assurance packets
RouteGuard emits a machine-readable `AssurancePacket` containing at least:
- task class;
- risk class;
- ambiguity/novelty scores;
- blast radius;
- required capability tier;
- required tools/modalities;
- privacy class;
- required independent critique;
- proof obligations;
- maximum allowed degradation;
- route decision reason codes.

This makes routing auditable and prevents hidden model choice logic.

## Route decision: gate first, optimize second
After hard filtering, eligible routes are ranked by expected Verified Outcome Cost using:
- observed first-pass success;
- correction probability;
- false-approval/miss rate;
- source-grounding quality;
- p50/p95 latency;
- current provider health;
- real token/cache price;
- cache-hit probability;
- project/task-specific priors.

The exact scoring formula remains benchmarkable and replaceable.

## Rework Tax
Hive Plan maintains a `ReworkTax` estimate per route × task class × project/stack when sufficient evidence exists.

Examples of rework cost:
- additional Codex execution round;
- extra reviewer/auditor call;
- CI retries;
- human intervention;
- rollback/recovery;
- escaped defect remediation.

This prevents apparent API savings from hiding downstream engineering cost.

## Quality Debt Ledger
Temporary degraded routing is permitted only when policy explicitly allows it, for example during provider outage on LOW/STANDARD tasks.

Every degraded decision records:
- preferred route;
- actual route;
- reason;
- capability delta;
- affected artifact/decision;
- whether later revalidation is required;
- expiry/debt status.

HIGH_ASSURANCE work never silently incurs quality debt. If the required route is unavailable, BLOCK.

## Escalation budget
BudgetPilot may reserve a small portion of task budget for escalation rather than spending the entire budget on the first call. This enables cheap-first routing without trapping the workflow when evidence demands a stronger second pass.

## Stability and hysteresis
To avoid routing thrash:
- do not switch model/provider on tiny score changes;
- maintain minimum health/quality observation windows;
- use circuit-breaker states and cooldowns;
- require meaningful evidence before changing default route for a task class.

## Outcome learning
After verified completion, RouteLab records:
- selected route;
- actual cost/latency;
- cache hits;
- correction rounds;
- review findings;
- final verdict;
- human intervention;
- escaped defect if later discovered.

Project-local priors may adapt from repeated evidence, but canonical routing policy does not self-modify from one observation.

## Freeze boundary
Freeze the capability tiers, hard eligibility gate, Verified Outcome Cost principle, Rework Tax, evidence-based escalation, Quality Debt rules and HIGH_ASSURANCE no-silent-degradation rule. Exact model names, numeric thresholds and weighting coefficients remain runtime configuration validated by evals.