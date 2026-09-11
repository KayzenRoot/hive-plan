# Review Specialist Activation Policy

Status: FROZEN — HP-PLAN-006

Specialists are activated by affected risk domains:

- Security: auth, permissions, secrets, untrusted input, crypto/signing, security configuration.
- Data/Migration: schema, persistence, migrations, consistency, recovery, retention.
- API/Integration: contracts, external providers, events, webhooks, service boundaries.
- Frontend Runtime: state/navigation/accessibility/error states/client-server contracts.
- Reliability/Concurrency: async jobs, retries, locks, queues, caches, distributed/state-machine effects.
- Performance: explicit SLO/performance impact or relevant hot path.
- Infrastructure/Deployment: CI/CD, container, environment/network/permissions/runtime configuration.
- Test/Regression: activated for every non-trivial governed implementation change; depth is risk-adaptive.
- Change Impact: activated when change surface is non-trivial, shared, contract-affecting or graph confidence is insufficient.

Senior Review Lead always owns synthesis; independent Auditor is activated by existing assurance policy.

Do not activate a specialist whose domain is demonstrably outside ReviewScope.