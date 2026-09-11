# HP-PLAN-010 — Adaptive Response Composer

Status: PROPOSED

## Mission
Choose the smallest and clearest combination of text, table, chart, diagram, graph, image and governed artifact cards for each engineering answer.

## Principle
The model does not receive arbitrary rendering authority. It proposes semantic content; `ResponsePlanner` chooses validated presentation blocks according to intent, evidence, data shape, accessibility, performance and user preference.

## Presentation policy
- explanation/recommendation -> structured prose + evidence;
- comparison with few dimensions -> table;
- quantitative trend/distribution -> chart + accessible table;
- architecture/process/dependency -> diagram;
- large navigable dependency/impact structure -> interactive graph + semantic mirror;
- visual/UI/artifact question -> image/screenshot where evidence exists;
- review -> finding cards + diff/evidence + optional impact graph;
- project status -> metric cards + timeline/progress chart + blockers;
- decision -> options/trade-offs + decision proposal card;
- implementation instruction -> Work Order proposal, never free-form executable authority.

Multiple representations are allowed when each adds distinct information. Decorative duplication is rejected.

## ResponsePlanner inputs
Intent, data_shape, evidence_types, authority, uncertainty, freshness, interaction mode, voice mode, viewport, accessibility profile, ResourcePeacekeeper state, user visual preference and response budget.

## Visual Integrity Gate
Before render:
- all numeric visuals map to supplied values;
- units and scales are explicit;
- no truncated axis may mislead without disclosure;
- freshness/source accompany operational metrics;
- generated concepts are labeled as generated;
- evidence screenshots identify exact source/snapshot;
- charts/graphs/diagrams have semantic fallback;
- unsupported rich blocks degrade to readable text.

## Voice-aware answers
When assistant speech is active, TTS reads a concise spoken layer while the screen may contain richer detail. Spoken summaries must not claim details absent from the visible/evidenced response. The operator can say `explique o gráfico`, `leia os findings` or `detalhe o segundo ponto` to traverse blocks.

## Personalization without hidden truth changes
The system may learn preferred density, chart/diagram frequency, voice verbosity and layout, but presentation preference cannot change canonical evidence, severity or verdict.

## Metrics
Measure scan time, expansion rate, block usefulness, visual correction rate, accessibility failures, rich-render latency, abandoned responses and operator preference overrides.

## STOP CONDITION
Freeze only when selection rules, integrity gates, fallback behavior, voice relationship and eval metrics are deterministic enough to test.