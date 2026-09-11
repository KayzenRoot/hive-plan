# HP-PLAN-010 — Rich Response Renderer + Visual Artifacts

Status: PROPOSED

## Mission
Make Engineering Chat responses readable, visual, inspectable and operationally useful instead of rendering every answer as flat Markdown.

## Response composition
The assistant response is compiled into a `ResponseDocument` with semantic blocks. Candidate block families:
- prose / headings / callouts;
- code / diff / terminal receipt;
- table / metric grid;
- timeline / checkpoint history;
- finding / risk / blocker card;
- source / citation / provenance card;
- agent activity / council summary;
- ADR / Work Order / checkpoint proposal;
- diagram;
- interactive graph;
- chart;
- image / visual reference;
- file/artifact card;
- expandable evidence bundle.

Unknown block types fail closed to readable text/JSON instead of breaking the conversation.

## Diagram pipeline
Use two tiers:
1. `MermaidRenderer` for deterministic text-generated diagrams that are easy to version in GitHub and render in chat.
2. `InteractiveGraphRenderer` behind adapter, with React Flow as leading candidate for architecture graphs, Feature Impact Graph, AgentTaskGraph, ProofGraph and dependency exploration.

Mermaid source remains exportable/copyable. Interactive graphs require a semantic text/DOM mirror for accessibility and evidence.

## Chart pipeline
Create provider-neutral `ChartSpec` rather than letting model-produced arbitrary JavaScript execute. Candidate renderer: Apache ECharts behind adapter, with simpler SVG/HTML renderers for small charts.

Allowed initial chart families:
- line / area;
- bar;
- stacked bar;
- scatter;
- heatmap;
- donut only where composition is truly useful;
- gauge only for bounded health/budget semantics;
- timeline / Gantt-like project views.

Charts must include units, source, freshness, accessible table alternative and no fabricated values.

## Image pipeline
Images may come from:
- user-provided attachments;
- repository artifacts/screenshots;
- approved web research;
- generated visual concepts when explicitly useful;
- UGAS integration in later authorized increments.

Every image block carries provenance and status. Generated concept art can never be presented as runtime evidence.

## Artifact actions
Rich blocks may expose governed actions such as:
- open source;
- inspect evidence;
- expand diagram;
- export Mermaid;
- pin to Project Brain;
- propose ADR;
- propose Work Order;
- compare versions;
- open Feature Impact Graph;
- send to review.

Actions never bypass normal authority/promotion gates.

## Streaming
Response blocks support progressive streaming:
- text can stream immediately;
- skeleton placeholders can reserve rich block space;
- diagram/chart spec renders only after structural validation;
- invalid partial specs remain hidden until complete;
- heavy graph/image rendering is deferred below the fold when appropriate.

## Visual quality
- Obsidian Glass surfaces around narrative and metadata;
- solid high-contrast panels for code/diffs/findings;
- contextual glow only for real state;
- smooth shared-element transitions for expanding artifact cards;
- no gratuitous animation on long technical content;
- visual hierarchy tuned for scanning rather than decorative density.

## Security
- no arbitrary HTML/JS from model or retrieved content;
- Markdown sanitized;
- Mermaid rendered under hardened config;
- links and images have source policy;
- diagram/chart specs validated against schemas;
- untrusted SVG handled by policy/sanitization;
- external research never gains action authority through a rich block.

## Performance
Virtualize long conversations; lazy-render heavy blocks; cache content-addressed diagram/chart output; avoid re-rendering completed blocks on unrelated chat updates; degrade to static SVG/DOM when ResourcePeacekeeper demands it.

## Evals
Golden response corpus must test code-heavy, architecture, review, data/chart, diagram, image-rich, long conversation, malformed spec, malicious Markdown/SVG, accessibility and low-resource profiles.