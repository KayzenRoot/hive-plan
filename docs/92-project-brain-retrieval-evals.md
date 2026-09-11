# HP-PLAN-010 — Project Brain Retrieval & Memory Evals

Status: PROPOSED

## Objective
Prove that Project Brain retrieves the right current evidence with bounded context and does not convert stale, irrelevant or semantically similar material into project truth.

## Golden scenario classes
1. exact current checkpoint lookup;
2. current ADR versus superseded ADR;
3. conflicting requirement sources resolved by hierarchy;
4. symbol/file impact lookup;
5. prior compatible failure retrieved and converted into constraint/test;
6. incompatible prior failure rejected;
7. recent chat statement conflicting with frozen decision;
8. HIVE unavailable with embedded fallback allowed;
9. HIVE unavailable where fallback is insufficient and task must block/degrade;
10. cross-project memory isolation;
11. secret-bearing source redaction;
12. malicious prompt/instruction embedded in retrieved content;
13. external GitHub/web research with advisory authority only;
14. source fingerprint change invalidating cached context;
15. provider restart/Redis loss with durable truth recovery.

## Retrieval metrics
- Canonical Recall@K
- Critical Evidence Miss Rate
- Superseded Source Leakage Rate
- Cross-Project Leakage Rate
- Failure Pattern Compatibility Precision
- Provenance Coverage
- Context Token Efficiency
- Cache Correctness / Stale Hit Rate
- Contradiction Detection Rate
- Unsupported Claim Rate
- Time to Evidence-Complete Context

## Zero-tolerance defects
- wrong-project memory returned as authoritative;
- superseded critical source presented as current without warning;
- secret material routed contrary to privacy policy;
- retrieved prompt injection altering agent/tool authority;
- canonical source omitted while lower-authority contradictory memory is used;
- stale cached ContextCapsule accepted after critical fingerprint change.

## Ablations
Compare:
- exact/lexical only;
- lexical + semantic;
- lexical + semantic + authority filter;
- lexical + semantic + authority + FIG/graph;
- full cascade + failure memory + reranker.

The full system must demonstrate measurable quality gain without unacceptable context/token/latency cost.

## Provider parity
Run the same golden corpus through HIVE_PROVIDER and EMBEDDED_LOCAL_PROVIDER. The embedded fallback may be less capable, but it must preserve authority, isolation, provenance and safety invariants. Capability loss must be exposed, never hidden.

## Answer-level evaluation
For selected engineering prompts, grade:
- whether the answer cites the correct current sources;
- whether every consequential recommendation is grounded;
- whether uncertainty is exposed;
- whether frozen decisions are respected;
- whether known prior failures are incorporated when compatible;
- whether unnecessary context is omitted.

## Promotion rule
No MemoryProvider/retrieval profile becomes default merely because semantic relevance scores improve. Promotion requires improved verified engineering outcomes with no regression in zero-tolerance safety/correctness gates.
