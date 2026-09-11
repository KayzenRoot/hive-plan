# HP-PLAN-010 — Multimodal Composer + Context Capture

Status: PROPOSED

## Mission
Make the Engineering Chat composer the universal intake surface for spoken, typed, visual, file, repository and structured engineering context without forcing the operator to manually translate every input into prompts.

## Composer capabilities
The composer supports:
- typed text and multiline technical prompts;
- push-to-talk, dictation and continuous voice;
- drag-and-drop files;
- paste/upload screenshots and images;
- repository file/symbol mentions;
- issue/PR/commit/Work Order/checkpoint mentions;
- artifact references from Project Brain;
- diagram/chart/image requests;
- optional screen-region capture adapter in a later authorized implementation;
- command palette and slash/voice commands.

## Context chips
Every attached input becomes an inspectable chip with source, project, freshness, sensitivity, size/token estimate and authority class. The operator can remove or pin chips before send.

## Context Capture Pipeline
INPUT -> MIME/TYPE DETECTION -> SECURITY/SENSITIVITY SCREEN -> PROJECT BINDING -> PROVENANCE -> EXTRACTION/INDEXING -> AUTHORITY CLASSIFICATION -> DEDUP -> CONTEXT BUDGET -> ContextCapsule.

No attachment becomes canonical merely because it was uploaded.

## Smart capture
The system may propose relevant nearby context using RepoPulse, Feature Impact Graph and Project Brain, but automatic additions must be visible in a `Context used` drawer. Critical context cannot be silently omitted due to token budget.

## Large inputs
Large PDFs, logs, repositories and media use staged extraction/indexing rather than stuffing full content into a model prompt. Exact excerpts remain traceable to the original artifact.

## Voice + visual continuity
A voice turn can reference currently visible artifacts using bounded deictic commands such as `compare este gráfico`, `abra esse finding` or `transforme este diagrama em ADR`. The UI resolves the target from explicit focus/selection state, never by guessing among multiple candidates.

## Security
Untrusted attachments are data, never instructions. Executables/macros/scripts are not run during ingestion. Archive traversal, decompression bombs, malicious SVG/HTML, prompt injection and secret leakage receive deterministic gates.

## Performance
Uploads/extraction/indexing run off the interaction-critical path. The composer remains responsive while background context preparation reports truthful progress.

## STOP CONDITION
Do not freeze until multimodal input, provenance, security, large-input handling, context visibility, token budgeting and target resolution are explicit and testable.