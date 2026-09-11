# HP-PLAN-010 — Engineering Chat Detailed Layout

Status: PROPOSED

## Mission
Create a voice-first, visually rich engineering conversation surface that remains excellent for hours of technical use.

## Desktop zones
- conversation canvas: dominant central column;
- Context/Agent rail: collapsible right rail;
- global nav: left rail;
- composer dock: persistent bottom zone;
- optional mini Project Pulse/Hive Core: compact, non-distracting.

## Conversation canvas
Messages are not identical bubbles. Assistant output is a semantic document with restrained glass narrative containers and specialized solid surfaces for code, diff, findings and evidence.

Width adapts by content:
- prose remains readable, not full-screen line length;
- tables/diffs/graphs can expand wider;
- full-screen artifact mode available;
- response outline appears for long answers.

## Voice composer
Composer contains:
- large microphone control / VoiceOrb;
- live partial transcript;
- send/cancel;
- mode selector: PUSH_TO_TALK / DICTATION / CONTINUOUS;
- attachment/context chips;
- text fallback;
- current project/focus indicator;
- privacy/provider indicator;
- optional `speak response` toggle.

Hands-free listening has an unmistakable screen state and hardware/privacy indicator.

## VoiceOrb motion
Orb deformation and waveform respond to measured microphone/assistant audio envelope and state, not random animation. State color/icon/text remain redundant. In reduced motion it becomes a mostly static state indicator.

## Rich response layout
Block families can occupy distinct visual grammar:
- narrative;
- decision/risk callout;
- diagram;
- chart;
- interactive graph;
- image/evidence screenshot;
- code/diff;
- findings;
- sources;
- agent council;
- ADR/WO/checkpoint proposal.

## Context Lens
A compact top/right indicator shows current project, canonical sources, memories, files, web research and agents influencing the response. Expand reveals exact provenance and freshness.

## Agent presence
Show specialists only when actually activated. Each chip exposes role, current bounded task, status and output/evidence. Avoid fake `thinking` animations disconnected from runtime events.

## Long-session ergonomics
- virtualized timeline;
- sticky current topic/objective;
- searchable conversation;
- TopicGraph breadcrumb;
- jump to decisions/artifacts/findings;
- collapse old rich blocks;
- branch subtopic action;
- resume capsule on return.

## Spoken response
Screen text is canonical response presentation. TTS uses a concise spoken projection. The operator can interrupt, request detail, navigate blocks or switch to silent mode.

## Interaction examples
`faça um diagrama disso` -> append validated diagram block.
`mostre as fontes` -> expand provenance.
`chame o especialista de segurança` -> policy/team evaluation then specialist if justified.
`transforme essa decisão em ADR` -> governed proposal.
`pare` -> immediate voice-output interruption lane.

## Performance
Heavy blocks lazy-render. Streaming prose is independent from chart/graph rendering. Voice visualization is first to degrade under resource pressure, never transcript/composer functionality.

## Acceptance direction
A 60-minute technical session must remain readable, responsive and navigable, including voice, long answers, diagrams, code and context inspection.