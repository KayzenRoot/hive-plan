# HP-PLAN-006 Review Round Checklist

Status: FROZEN

Before auto-review can publish a verdict:
- immutable snapshot pinned;
- Work Order/Context Lock valid;
- CI/evidence prerequisites satisfied;
- ReviewScope compiled from diff + impact closure;
- Feature Impact Graph neighborhood checked;
- deterministic/static/test tools completed as required;
- UADS specialist plan compiled and required roles completed;
- findings normalized, evidence-grounded and deduplicated;
- all acceptance criteria/proof channels disposed;
- no unresolved HIGH/CRITICAL finding;
- Senior Review Lead synthesis complete;
- independent audit complete where policy requires;
- snapshot revalidated immediately before Review Receipt;
- correction/checkpoint side effects guarded by EffectLedger.

STOP CONDITION: publish exactly one current Review Receipt or a governed BLOCKED state for the exact reviewed snapshot.