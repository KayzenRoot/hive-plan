# Agent Authority and Escalation Matrix

Status: FROZEN — HP-PLAN-001

## Core rule
Agents may analyze and propose within their domain, but no agent may silently promote a material decision into canonical truth. Canonical changes pass governed approval and checkpoint reconciliation.

## Authority levels
- **A0 OBSERVE** — read sources, classify, retrieve, summarize.
- **A1 PROPOSE** — generate options, questions, recommendations, draft changes.
- **A2 REVIEW** — challenge/validate proposals and evidence independently.
- **A3 AUTHORIZE** — approve a governed transition when policy allows.
- **A4 OPERATOR** — human owner; final authority for scope expansion, high-impact irreversible decisions, privileged/destructive actions, and policy exceptions.

## Role matrix
| Role | Default authority | May freeze alone? | Mandatory escalation |
|---|---:|---|---|
| Interviewer / Discovery | A1 | No | unresolved critical ambiguity, scope conflict, HIGH risk |
| Product Planner | A1 | No | scope/version change, business-critical trade-off |
| Requirements Engineer | A1 | No | conflicting requirements, untestable acceptance criteria |
| Software Architect | A1 | No | high-impact architecture, irreversible coupling, platform boundary change |
| Innovation Scout | A1 | No | none by itself; proposals remain classified |
| Security Engineer | A2 in security domain | No | CRITICAL/HIGH finding, secret/data boundary change |
| Data / DBA | A2 in data domain | No | destructive migration, integrity/recovery risk |
| Migration / Recovery | A2 | No | rollback uncertainty, destructive/irreversible migration |
| Platform / Infrastructure | A1/A2 | No | privileged/destructive infra action, high operational blast radius |
| DevOps / Release | A1/A2 | No | release policy exception, branch/history destructive operation |
| QA / Test | A2 | No | missing proof obligation, failing critical acceptance test |
| Reliability | A2 | No | unmitigated high-severity failure mode |
| Performance | A2 | No | benchmark regression beyond configured budget |
| Observability | A1/A2 | No | critical system lacks evidence/diagnostic path |
| Frontend / UX | A1 | No | accessibility blocker or destructive UX workflow |
| API / Integration | A1/A2 | No | contract-breaking change, external trust boundary |
| GitHub Steward | A1 operationally | No | destructive/privileged GitHub operations |
| Work Order Compiler | A1 | No | stale context, ambiguous acceptance criteria |
| Reviewer | A2 | No | HIGH/CRITICAL defect, evidence gap |
| Independent Auditor | A2/A3 for eligible low/standard risk gates | No for high-assurance | policy violation, contradictory evidence, HIGH_ASSURANCE |
| Checkpoint / Continuity | A1 | No | canonical conflict/stale source |
| FinOps / LLM Cost | A1/A2 | No | cost budget breach or provider-risk concern |
| Documentation Engineer | A1 | No | documentation/code truth conflict |
| Operator | A4 | Yes where policy permits | none above operator, but policy may still prohibit unsafe actions |

## Risk classes
### LOW
Reversible, local, low blast radius. Targeted specialist checks are enough.

### STANDARD
Normal product engineering change. Requires relevant tests plus architecture/requirements consistency.

### ELEVATED
Meaningful persistence, migration, security, external integration, availability, performance, or recovery impact. Requires cross-specialist review and stronger evidence.

### HIGH_ASSURANCE
Money, privileged authentication/authorization, signing/Web3, security-critical controls, destructive or hard-to-reverse operations, severe data-integrity risk, or equivalent consequences. Requires independent proof obligations, strong testing, explicit rollback/roll-forward strategy, independent audit, and operator approval where material.

## Escalation triggers
Automatic escalation occurs when any of the following is detected:
- critical/high uncertainty affecting the next decision
- disagreement between canonical sources
- proposed scope expansion
- irreversible or expensive-to-reverse decision
- sensitive data / privilege / secret handling
- destructive migration or data integrity risk
- external provider lock-in with high switching cost
- breaking API/integration change
- material performance/cost budget breach
- insufficient testability or evidence
- stale Context Lock / changed critical source fingerprint
- Reviewer and Auditor disagree
- model confidence conflicts with deterministic evidence

## Independent critique rule
A consequential proposal cannot be reviewed by the same logical agent instance/process that authored its decisive recommendation when independent critique is required. Hive Plan should separate role context and, where practical, model call/state to reduce self-confirmation bias.

## Operator interruption points
Operator approval is required for:
- expanding the frozen V1 scope
- accepting an unmitigated HIGH/CRITICAL risk
- destructive/history-rewriting GitHub actions
- security-policy exceptions
- irreversible migration without proven recovery path
- materially increasing recurring cost/budget beyond configured threshold
- freezing a contested high-impact architecture decision when specialists disagree

## Stale-context rule
Any active analysis/decision packet is marked STALE if a critical canonical source, Git base/head, Work Order, scope, architecture decision, or required evidence changes after its Context Lock. Stale analysis cannot authorize progression until reconciled.

## Verdict semantics
- **APPROVED** — obligations satisfied; governed progression is allowed.
- **CORRECTION REQUIRED** — safe correction can remain within the same Work Order/PR; only a Correction Delta is generated.
- **BLOCKED** — external decision, unresolved risk, missing evidence, stale context, policy conflict, or unsafe condition prevents progression.

HIGH/CRITICAL known defects always prevent APPROVED.
