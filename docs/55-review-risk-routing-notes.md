# Review Risk Routing Notes

Status: FROZEN — HP-PLAN-006

Review depth is raised by evidence, not PR size alone.

Signals that raise review depth include:
- authentication/authorization/security boundary;
- money/signing/privileged operations;
- data migration/integrity/recovery;
- concurrency/state-machine/distributed effects;
- public contract/schema/event compatibility;
- broad dependency centrality;
- historically fragile/hot module;
- repeated known failure pattern;
- weak test/proof coverage;
- unexpected change-surface expansion.

Signals that may keep the fast path include narrow low-risk change, complete deterministic evidence, stable impacted neighborhood, strong targeted tests and no material security/data/contract reach.

No low-risk signal can override a policy-mandated HIGH_ASSURANCE path.