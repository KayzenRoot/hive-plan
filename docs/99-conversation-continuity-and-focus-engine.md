# HP-PLAN-010 — Conversation Continuity + Focus Engine

Status: PROPOSED

## Mission
Support very long engineering conversations without token explosion, topic drift or loss of decisions.

## Conversation model
A conversation is an event stream plus derived views, not one endlessly growing prompt.

Derived layers:
- RecentTurnWindow: exact recent turns needed for local coherence;
- SessionState: active objective, selected project, focused artifacts and pending questions;
- DecisionTrail: proposed/accepted/rejected/superseded decisions with provenance;
- ArtifactTrail: diagrams, charts, files, ADR/WO/checkpoint proposals;
- TopicGraph: semantic topics and relationships;
- ConversationDigest: evidence-linked rolling summaries;
- ProjectBrainLinks: canonical references and verified memories.

## Focus Engine
`FocusEngine` computes what belongs in the next ContextCapsule using current intent, explicit focus, source authority, recency, dependency reach, unresolved questions, known failure patterns and token budget.

It must preserve critical constraints even when old turns are compressed.

## Topic branching
The operator may branch a subtopic without losing the parent thread. Branches share canonical Project Brain references but maintain separate local session state. Rejoining creates an explicit synthesis event rather than concatenating transcripts.

## Continuation across sessions
A new session can restore from checkpoint + canonical sources + SessionResumeCapsule. Raw old transcript is retrieved only when necessary.

## Drift detection
Detect:
- objective drift;
- contradiction with canonical source;
- unresolved question forgotten by the dialogue;
- assumption silently becoming fact;
- repeated discussion already decided;
- stale artifact/source;
- excessive context growth.

When material, surface a compact continuity warning or ask a targeted question.

## Compression safety
Summaries are derived memory with provenance, never higher authority than their sources. Critical exact values, paths, SHAs, acceptance criteria and operator decisions remain losslessly referenceable.

## Voice continuity
Voice sessions use the same SessionState. `continue de onde paramos`, `volte para o assunto do review` and similar commands resolve against TopicGraph/DecisionTrail and show the resolved target before high-impact action.

## Metrics
Context tokens/turn, retrieval precision, stale-context incidents, repeated-question rate, lost-constraint rate, correction caused by missing context, resume success and summary/source disagreement.

## STOP CONDITION
Do not freeze until long-session compaction, branching, resume, drift detection and critical-information preservation have explicit tests.