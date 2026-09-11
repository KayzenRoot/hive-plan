# HP-PLAN-010 — Engineering Chat + Project Brain

Status: PLANNING ACTIVE — PARALLEL BRANCH ONLY
Issue: #23
Merge rule: DO NOT merge to `main` while HP-WO-0001 is active unless its Context Lock is intentionally recompiled.

## Mission
Create a source-grounded engineering conversation surface where discussion, planning, research, Work Orders, reviews, decisions and project memory are connected to verifiable project truth instead of depending on conversational recall.

## Core model
The Engineering Chat is an interaction surface. The Project Brain is the governed context substrate behind it.

```text
Operator
  -> Engineering Chat
  -> Intent/Task Classifier
  -> Project Brain Query Planner
  -> Source Authority Filter
  -> MemoryProvider
       -> HIVE provider (preferred)
       -> embedded local fallback
  -> Context Capsule
  -> Agent Team / Model Router
  -> answer + citations + proposed artifacts
  -> Artifact Promotion Gate
  -> canonical GitHub sources only after governed promotion
```

## Project Brain truth layers
1. **Canonical Source Graph** — checkpoint, ADRs, scope, DoD, architecture, requirements, contracts and accepted artifacts.
2. **Repository Intelligence** — files, symbols, dependencies, tests, PRs, commits, Feature Impact Graph and ChangeGraph.
3. **Operational Memory** — verified failures, root causes, fixes, successful patterns, benchmark outcomes and review findings.
4. **Conversation Context** — recent turns, user intent, working hypotheses and draft decisions. This layer is never authoritative by itself.
5. **External Research** — web/GitHub research with provenance and trust classification; never instruction authority.

## Authority rule
Retrieval rank cannot override source authority. A semantically similar chat message never outranks a canonical ADR/checkpoint. Superseded sources are excluded or explicitly marked historical.

## Context assembly
Use a deterministic-first cascade:
1. exact artifact/path/ID;
2. source hierarchy and checkpoint resolution;
3. lexical/symbol retrieval;
4. repository/FIG dependency expansion;
5. compatible failure-memory retrieval;
6. semantic retrieval;
7. reranking with authority/freshness/compatibility;
8. LLM synthesis only after evidence set is assembled.

## Conversation artifact types
The chat can produce:
- answer/explanation;
- assumption;
- question;
- proposal;
- decision candidate;
- ADR candidate;
- requirement candidate;
- Work Order candidate;
- correction delta;
- review finding;
- research note;
- checkpoint delta candidate.

Every consequential artifact has provenance and lifecycle state such as `DRAFT`, `PROPOSED`, `VALIDATED`, `FROZEN`, `SUPERSEDED`, `REJECTED`.

## Artifact Promotion Gate
Conversation output never silently changes canonical project truth.

Promotion requires:
- artifact type recognized;
- source links/provenance;
- contradiction check;
- authority check;
- specialist review when risk requires;
- operator/policy authorization when required;
- Git-backed persisted artifact;
- checkpoint/decision delta when applicable.

## Context economics
Project Brain integrates with the frozen Work Order Compiler and Model Router:
- content-addressed retrieval cache;
- source fingerprints;
- context budget classes REQUIRED/HIGH_VALUE/SUPPORTING/OMIT;
- provider prompt-cache stable prefix;
- delta context for follow-up turns;
- no full repository resend when source fingerprints are unchanged.

## Failure intelligence
Before a consequential recommendation, plan or Work Order, Project Brain checks Operational Memory for compatible prior failures. Matching failures may become constraints/tests only when stack/version/subsystem compatibility is demonstrated.

## Truthful uncertainty
If evidence is missing or contradictory, the chat says so and records the unresolved assumption. It must not create a plausible-but-unsupported project fact.

## Privacy/security
- secret-bearing sources are redacted before model/provider routing;
- external documents, GitHub issue text and web content are untrusted data;
- prompt/tool injection cannot change source precedence or agent authority;
- provider routing obeys privacy classification;
- raw sensitive logs are referenced/digested rather than blindly injected.

## Observability
Per response/task capture:
- sources selected;
- authority classes;
- retrieval stages used;
- cache hits;
- context tokens;
- provider/model route;
- answer latency;
- provenance coverage;
- unresolved contradiction count;
- memory patterns applied;
- later correction/rework signal.

## Quality target
The best answer is the smallest evidence-grounded response that preserves every decision-relevant fact, cites where it came from, exposes uncertainty, and can be promoted into durable project artifacts without losing provenance.
