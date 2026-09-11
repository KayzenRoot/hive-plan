# Worked Example — Login Change Review

Status: EXAMPLE / NON-CANONICAL POLICY ILLUSTRATION — HP-PLAN-006

## Scenario
A Work Order changes login behavior, error handling and session creation.

## ReviewScope seed
Actual diff identifies changes in:
- login form/state;
- auth login endpoint;
- session creation helper.

## Feature Impact Graph expansion
The graph may add:
- request/response auth schema;
- route guard/protected-route transition;
- cookie/session configuration;
- CSRF/CORS/security policy if coupled;
- auth middleware consumers;
- login/session tests;
- prior authentication regressions.

Billing, search, media and unrelated admin modules remain excluded unless an explicit dependency edge proves impact.

## Deterministic preflight
- base/head SHA and Context Lock match;
- changed symbols extracted;
- typecheck/lint/build status collected;
- targeted auth tests and impacted integration/E2E tests identified;
- static security findings normalized;
- prior failure patterns retrieved.

## UADS AgentReviewPlan

### Security Reviewer
Scope: session/token/cookie/guard/security configuration only.  
Questions: bypass, privilege transition, fixation, CSRF, cookie flags, unsafe redirects, brute/abuse boundaries, secret leakage.

### API/Integration Reviewer
Scope: login handler/schema/error contract + known consumers.  
Questions: compatibility, status/error semantics, client expectations, retry/idempotency where relevant.

### Frontend Reviewer
Scope: login form/state/navigation/protected transition.  
Questions: stale state, race/double-submit, error visibility, incorrect navigation, client/server contract mismatch.

### Test Reviewer
Scope: acceptance criteria + auth test neighborhood.  
Questions: valid login, invalid credentials, disabled user if applicable, expiry/session behavior, protected route, negative/security cases.

### Change Impact Reviewer
Scope: actual diff + FIG neighborhood.  
Questions: missing affected consumer, hidden coupling, unexpected touched file, stale graph edge.

### Senior Review Lead
Receives normalized specialist outputs and deterministic evidence, deduplicates root causes, checks acceptance/proof coverage and produces verdict candidate.

## Example blocking finding format
```yaml
finding_id: AUTH-017
severity: HIGH
classification: NEW_REGRESSION
location: src/api/auth/login.ts::createSession
failure_condition: successful login creates a session cookie without the required HttpOnly flag
impact: session token becomes accessible to client-side script, increasing token theft risk
proof:
  - changed head SHA
  - cookie construction diff
  - frozen security policy reference
correction_criterion: create the session cookie with required policy flags and add/adjust a test that proves them
```

## Correction prompt behavior
The correction prompt contains AUTH-017 and any other confirmed findings only. It does not tell Codex to redesign the authentication system, refactor unrelated middleware or clean legacy code.

If the fix changes only session-cookie construction and tests, the next review reuses unaffected evidence and re-runs the impacted auth/security closure plus required regression tests.

## Purpose
This example demonstrates the target behavior: narrow start, complete semantic impact, specialist depth only where justified, actionable findings and delta-first correction.