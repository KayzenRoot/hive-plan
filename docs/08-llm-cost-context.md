# LLM Cost & Context Engine

## Objective
Maximize planning/review quality per unit of cost while preserving escalation for high-risk reasoning.

## Core strategy
1. Deterministic tools first.
2. Retrieve only authoritative relevant context.
3. Deduplicate and delta-compress context.
4. Keep stable prompt prefixes cache-friendly.
5. Route low-risk work to cheaper models.
6. Escalate when complexity, uncertainty, blast radius, or assurance requirements justify it.
7. Measure real quality/cost with evals instead of assuming model hierarchy.

## Context Compiler
```text
User intent / workflow event
        ↓
Canonical source resolver
        ↓
RAG retrieval + dependency expansion
        ↓
Git/tool facts
        ↓
Dedup / freshness / authority scoring
        ↓
Token budget allocator
        ↓
Stable cached prefix + dynamic context package
        ↓
Model router
```

## Routing dimensions
- task type;
- risk class;
- architecture/security/data impact;
- reversibility;
- context size;
- uncertainty/confidence;
- previous failed attempts;
- expected value of stronger reasoning;
- current provider/model price and availability.

## Model policy
No model name is permanently hard-coded as the only tier. Profiles such as `FAST_CHEAP`, `BALANCED`, `STRONG`, and `HIGH_ASSURANCE` map to currently approved provider models and may change without rewriting domain workflows.

## Caching layers
- Provider prompt cache for stable instruction/source prefixes.
- Local semantic/retrieval cache.
- Tool-result cache with freshness/ETag/SHA semantics.
- Compiled-context cache keyed by source fingerprints and task class.
- Response reuse only for safe deterministic/equivalent requests.

## Telemetry
Attribute at minimum: input/output/cached tokens, estimated/actual cost, provider/model/profile, latency, retries, cache-hit ratio, retrieved-context size, project, Work Order, agent role, and verdict/outcome quality signal.

## Quality guardrail
Cost optimization MUST NOT suppress required HIGH_ASSURANCE review, security reasoning, independent audit, or proof obligations.
