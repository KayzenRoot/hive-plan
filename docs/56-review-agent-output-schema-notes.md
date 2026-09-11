# Review Agent Output Schema Notes

Status: PROPOSED CONTRACT INPUT — HP-PLAN-006

Every specialist reviewer should return a structured disposition containing:
- agent_role;
- reviewed_snapshot_fingerprint;
- reviewed_scope_fingerprint;
- coverage/disposition by assigned question;
- findings[];
- proof gaps[];
- unresolved assumptions[];
- escalation_required;
- PASS / FINDINGS / BLOCKED;
- artifact digest.

Each finding should include:
- finding_id;
- severity;
- classification (NEW_REGRESSION / WORSENED_EXISTING / IMPACT_RELEVANT_EXISTING);
- requirement/criterion references;
- file/symbol/contract location;
- concrete failure condition;
- evidence references;
- impact;
- correction criterion;
- specialist role.

Free-form prose may accompany the structure but cannot substitute for it.