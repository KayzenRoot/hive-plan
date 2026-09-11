# HP-PLAN-005 Routing Invariants

1. Deterministic/local resolution wins over LLM reasoning when the task is decidable locally.
2. QualityFloor is evaluated before price/latency ranking.
3. A cache hit must match all critical fingerprints and may not gain authority.
4. Provider/model fallback must satisfy required capability, privacy and assurance.
5. HIGH_ASSURANCE never silently degrades.
6. Exact provider/model names and prices are runtime configuration, not architecture.
7. Routing improvements are promoted only by eval evidence.
8. Optimize total verified outcome cost, not isolated call price.
9. Model self-confidence does not elevate assurance.
10. Unavailable required assurance results in BLOCK, not guesswork.