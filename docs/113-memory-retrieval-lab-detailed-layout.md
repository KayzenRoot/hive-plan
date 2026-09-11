# HP-PLAN-010 — Memory / Retrieval Lab Detailed Layout

Status: PROPOSED

## Mission
Make RAG observable, debuggable and measurable instead of an invisible prompt trick.

## Primary zones
- query/input inspector;
- retrieval pipeline visualization;
- candidate result table;
- ContextCapsule composition;
- FailureShield matches;
- cache/index health;
- retrieval eval dashboard.

## Retrieval pipeline
Visual stages: query normalization -> exact/symbol -> lexical -> structural/graph -> vector -> fusion/RRF -> rerank -> authority/freshness/compatibility -> budget selection -> ContextCapsule.
Each stage reports duration, candidate count, cache status and failure/degraded reason.

## Candidate inspector
Rows/cards expose source, excerpt, path/entity, authority, freshness, compatibility, lexical/vector/fusion/rerank score, selected/omitted reason and provenance.

## ContextCapsule view
Shows REQUIRED/HIGH_VALUE/SUPPORTING/OMIT composition, token estimate, dedup savings and critical constraints. Operator can inspect but cannot silently downgrade mandatory canonical context.

## FailureShield
Displays matching verified prior failures, root causes, compatibility evidence, correction and prevention test. Semantic similarity alone is labeled insufficient.

## Eval dashboard
Track retrieval precision, canonical-source recall, stale-source rate, wrong-project contamination, failure-memory usefulness, token savings, cache hit rate and downstream correction attributable to missing/wrong context.

## Voice
`por que esse documento entrou?`, `qual memória foi descartada?`, `mostre falhas parecidas`, `quanto contexto economizamos?`.

## Safety
Secrets/redacted content never become visible merely because debug mode is open. Untrusted external text is labeled.