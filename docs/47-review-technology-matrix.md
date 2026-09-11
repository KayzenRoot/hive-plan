# Review Technology Adoption Matrix

Status: PROPOSED FOR FREEZE — HP-PLAN-006

## Rule
Technology is adopted only when it increases material-defect detection, impact completeness or review speed without unacceptable noise/resource cost. Every tool remains behind a normalized evidence/finding adapter when practical.

## Candidates

| Technology / approach | Role | Initial status | Notes / adoption gate |
|---|---|---|---|
| Git diff/SHA/merge-base | exact changed surface | ADOPT | authoritative base evidence |
| RepoPulse + Tree-sitter/ast-grep | changed symbols/structural impact | ADOPT ARCHITECTURE / backend benchmark | verify language coverage/latency |
| language compiler/typechecker | semantic correctness | ADOPT WHEN AVAILABLE | deterministic, high value |
| project linter/formatter | style/static policy | ADOPT | keep style noise out of LLM review |
| SARIF 2.1 compatible normalization | scanner finding interchange | ADOPT AS INTERFACE | enables tool/vendor-neutral static findings |
| GitHub CodeQL | security/error/data-flow analysis | TRIAL → ADOPT by repo/language/policy | strongest value for supported high-risk paths; availability/license/resource constraints apply |
| Semgrep | fast pattern/security rules | TRIAL | measure incremental findings/noise; advanced interfile capability may require commercial engine |
| reviewdog-style diff filtering | surface static findings only when relevant to patch | TRIAL | useful output/annotation pattern, not core authority |
| changed-line / impacted-test coverage | test adequacy | TRIAL → ADOPT candidate | guard against tests that never exercise changed behavior |
| mutation testing on small critical slices | test strength | TRIAL for HIGH_ASSURANCE | expensive; only bounded changed/impact slices |
| property-based/fuzz testing | edge-case discovery | TRIAL by domain | compile from contracts/invariants where payoff is measurable |
| dependency/SBOM vulnerability scan | dependency changes | ADOPT WHEN RELEVANT | activate on lockfile/package/image changes |
| secret scanning | public-repo/push safety | ADOPT | deterministic gate before publication |
| OpenTelemetry-style spans/metrics | review pipeline observability | ADOPT AS INTERFACE | measure per-stage latency/cost/yield |

## SARIF policy
Normalize compatible static-analysis outputs to one internal Finding/Evidence adapter. SARIF is an interchange surface, not final severity authority. Hive Plan still applies scope, baseline, policy, duplication and evidence normalization.

## CodeQL policy
Use CodeQL when supported and justified by language/risk/resources. Strong use cases include auth/security boundaries, taint/data flow, dangerous source→sink paths and relevant code scanning. Keep query packs/version fingerprints in evidence. For unsupported/unavailable private-repo configurations, use other local/static adapters rather than weakening review quality silently.

## Semgrep policy
Semgrep can provide high-speed rule/pattern coverage across many stacks. Evaluate community/local rules independently from advanced cross-file offerings. Promote only rule packs with acceptable confirmed-finding precision on Hive Plan fixtures/projects.

## Diff filtering policy
Static tools may report pre-existing repository issues. ReviewScope/FindingGate distinguishes:
- NEW_REGRESSION;
- WORSENED_EXISTING;
- IMPACT_RELEVANT_EXISTING;
- UNRELATED_EXISTING.

Only the first three enter active review according to policy. Unrelated legacy noise is recorded separately if useful but does not block the increment.

## Test-strength innovations

### Changed Behavior Coverage
Prefer proof that changed semantic paths executed, not raw global coverage percentage.

### Targeted Mutation Gate
For HIGH_ASSURANCE or historically fragile logic, mutate only critical changed/impact-closure symbols. If required tests fail to kill plausible mutations, flag a proof gap. Do not mutation-test entire repositories by default.

### Contract Fuzz Seed
Generate bounded fuzz/property cases from JSON Schema/API/data invariants for changed contracts. Keep generated cases reproducible via seed and artifact digest.

## Tool portfolio optimization
Track each tool's:
- runtime/cpu/ram;
- findings generated;
- confirmed actionable findings;
- unique findings not detected elsewhere;
- false positive/noise rate;
- effect on escaped defects;
- effect on review wall-clock.

Remove or demote tools whose unique defect yield does not justify cost/complexity.

## Freeze boundary
Freeze adapter-based scanner architecture, SARIF-compatible normalization, diff/baseline filtering and benchmark-gated tool portfolio. Exact CodeQL/Semgrep/query-pack/test-strength tool configuration remains environment/project/risk dependent.