# ADR-033 — Voice-First Governed Engineering Chat

Status: ACCEPTED  
Date: 2026-09-11  
Increment: HP-PLAN-010

## Context
Hive Plan needs a primary engineering conversation surface that is comfortable by voice, rich in technical artifacts and capable of research/actions without weakening authority, accessibility or auditability.

## Decision
Adopt Engineering Chat as a voice-first, multimodal, source-grounded workspace. Voice uses a provider-neutral `VoiceProvider`, with local-first routing and typed fallback. Raw transcripts are conversational input only and never canonical truth.

Every natural-language action is resolved through a typed ActionPlan/ActionRouter with explicit target, parameters, authority, reversibility, expected effects, evidence and rollback/cancel semantics. Destructive, irreversible, privileged, scope-expanding or otherwise high-impact actions require policy/operator confirmation regardless of voice confidence.

Rich responses use validated semantic blocks rather than arbitrary model HTML/JS/SVG. Agent collaboration exposes evidence-backed conclusions, disagreement and uncertainty, not hidden chain-of-thought. Artifact promotion into canonical GitHub state remains governed.

## Consequences
- voice can become the preferred operating mode without becoming a privileged bypass;
- multimodal responses can include code, diffs, diagrams, charts, evidence and governed artifact proposals;
- local/cloud voice providers remain replaceable;
- accessibility and text equivalents remain mandatory.

## Rejected alternatives
- raw transcript directly invoking privileged tools;
- cloud voice as a mandatory dependency;
- arbitrary model-rendered executable UI;
- voice-only workflows with no text/accessibility equivalent.