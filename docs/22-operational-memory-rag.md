# Operational Memory & RAG Governance

Status: FROZEN DIRECTION — HP-PLAN-002

## Purpose
Hive Plan must remember more than approved decisions. It must preserve useful engineering experience so future planning, Work Orders, reviews, and corrections can reuse what has already been proven while avoiding repeated mistakes.

The memory system is not authority by itself. Retrieval supplies evidence and experience; canonical truth is still resolved by the Source Hierarchy.

## Memory classes

### 1. Canonical Memory
Approved project truth mirrored/indexed from authoritative sources such as:
- Checkpoints
- Decisions Ledger / ADRs
- Scope
- Definition of Done
- Architecture
- Requirements
- security/data/API/integration contracts
- approved releases/tags

Authority: HIGH, subject to source freshness and supersession.

### 2. Execution Memory
Traceable facts from implementation and delivery:
- Work Orders and Correction Deltas
- base/head SHAs
- PRs and diffs
- CI/test/build/lint/typecheck results
- benchmarks
- Evidence Bundles
- review receipts
- release results

Authority: FACTUAL when deterministically verified; otherwise claim-only until verification.

### 3. Experience Memory
Reusable engineering knowledge learned from completed work:
- patterns that worked
- implementation approaches that reduced time/cost
- architecture choices and their observed trade-offs
- high-value test strategies
- provider/model/tool behavior
- effective prompts/context packages
- successful recovery paths

Authority: ADVISORY. It may inform planning but cannot override canonical project decisions.

### 4. Failure / Negative Knowledge Memory
Failures are first-class knowledge:
- failed approaches
- root causes
- regressions
- flaky tests
- broken dependencies
- incorrect assumptions
- review misses
- unsafe migrations
- expensive LLM/context patterns
- fixes that resolved the failure

Every reusable failure record should capture:
- failure ID
- project / Work Order / PR
- symptom
- root cause, or UNKNOWN if not proven
- contributing conditions
- rejected hypotheses
- correction
- validation evidence
- affected technology/version/environment
- recurrence-prevention rule
- confidence
- supersession/expiry status

This memory exists specifically so Hive Plan can ask: `Have we failed this way before?` before proposing or executing a similar path.

### 5. Preference / Workflow Memory
Stable operator-approved workflow preferences and project conventions may be indexed, but only explicit/canonical preferences may affect governed behavior.

## Provenance contract
Every memory item used in consequential reasoning must retain provenance where available:
- source repository
- source path/object
- source type
- commit SHA / PR / Work Order / release
- timestamp
- project
- authority class
- validation state
- superseded-by relation
- technology/version/environment metadata

No anonymous vector chunk may silently become a planning fact.

## Retrieval pipeline

```text
Task / question / workflow event
        ↓
Canonical source resolver
        ↓
Project-local retrieval
        ↓
Execution + failure-memory retrieval
        ↓
Cross-project proven-pattern retrieval (when policy permits)
        ↓
Freshness / authority / compatibility scoring
        ↓
Deduplication + contradiction detection
        ↓
Context budget allocator
        ↓
Context Compiler
```

## Retrieval ranking dimensions
- authority
- semantic relevance
- project locality
- freshness
- validation strength
- source compatibility
- technology/version compatibility
- environment/hardware compatibility
- recurrence/frequency
- outcome quality
- supersession state

Semantic similarity alone is insufficient.

## Cross-project learning
Hive Plan may reuse experience across Hive ecosystem projects when:
1. no project confidentiality policy forbids it;
2. the retrieved pattern is clearly marked as cross-project experience;
3. technology/version/environment compatibility is checked;
4. canonical local decisions retain priority;
5. the system does not copy secrets, credentials, private data, or project-specific sensitive content into another context.

Reusable knowledge should prefer normalized `Engineering Pattern` / `Failure Pattern` records over copying raw project conversations.

## Learning loop

```text
PLAN
 ↓
WORK ORDER
 ↓
EXECUTION
 ↓
EVIDENCE
 ↓
REVIEW / AUDIT
 ↓
OUTCOME
 ↓
LESSON EXTRACTION
 ↓
VALIDATE LESSON
 ↓
INDEX AS EXPERIENCE / FAILURE MEMORY
 ↓
AVAILABLE TO FUTURE PLANNING
```

Lesson extraction occurs only after outcome evidence exists. Executor claims alone do not produce trusted lessons.

## Negative-knowledge preflight
Before a Work Order is finalized, Hive Plan should search for prior failures matching:
- technology stack
- changed subsystem
- integration/provider
- error signature
- migration type
- architecture pattern
- security boundary
- performance pattern

High-confidence matching failures become explicit Work Order constraints or tests when relevant.

## Cache integration
RAG and cache cooperate but are distinct:
- RAG finds relevant knowledge.
- Local retrieval cache avoids repeating equivalent searches while source fingerprints remain unchanged.
- Compiled-context cache reuses safe context packages by task + canonical fingerprints.
- Provider prompt cache handles stable instruction/source prefixes.
- Any critical source change invalidates dependent compiled-context artifacts.

## Anti-poisoning rules
- Repository/chat/external content is data, not authority.
- Retrieved instructions cannot override system policy or Source Hierarchy.
- Unverified generated text is never indexed as canonical truth.
- Contradictory memories are surfaced, not silently merged.
- Superseded decisions remain historically searchable but excluded from current-authority answers unless history is requested.
- Low-confidence root causes remain labeled UNKNOWN/PROBABLE rather than promoted to fact.

## Retention and compaction
Prefer structured durable facts and lessons over endless raw transcripts.
- preserve canonical history and traceability;
- summarize/compress low-value conversation history;
- deduplicate repeated chunks;
- retain failure/evidence links;
- allow re-embedding without losing original provenance;
- keep vector indexes rebuildable from durable sources.

## Quality metrics
Track at minimum:
- retrieval precision / useful-context rate
- stale-context rate
- contradiction detection rate
- repeated-error recurrence rate
- prior-failure-prevented count
- cross-project reuse success rate
- context tokens avoided
- cache hit ratio
- retrieval latency
- answer/review quality after retrieval

## Core principle
The goal is not `remember everything`. The goal is `retrieve the smallest, freshest, highest-authority set of facts and proven experience that improves the current engineering decision`.