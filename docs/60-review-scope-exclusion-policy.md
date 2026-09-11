# Review Scope Exclusion Policy

Status: FROZEN — HP-PLAN-006

ReviewScope explicitly records excluded areas so reviewers do not wander.

An area may be excluded when:
- it is outside actual diff and verified impact closure;
- no contract/dependency/security/data/test edge connects it to the change;
- the Work Order explicitly marks it out of scope;
- no required proof obligation reaches it.

Exclusion is revoked immediately when evidence reveals a dependency/impact edge. HIGH_ASSURANCE paths may require broader validation even for unchanged components.