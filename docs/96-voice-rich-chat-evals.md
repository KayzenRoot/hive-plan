# HP-PLAN-010 — Voice + Rich Chat Evals

Status: PROPOSED

## Goal
Prove that Engineering Chat is pleasant, fast, correct, accessible and safe under voice-first and rich-response use, especially Portuguese-BR software-engineering conversations.

## Voice golden corpus
Include natural Brazilian Portuguese with:
- informal conversational phrasing;
- English technical terms embedded in Portuguese;
- repository/branch/file names;
- acronyms: HIVE, UADS, UGAS, ADR, RAG, CI/CD, API, SSE, PR;
- model and library names;
- numbers, versions, SHAs and paths;
- corrections mid-utterance;
- pauses and filler words;
- noisy room and different microphone quality.

## Voice quality metrics
- WER overall and engineering-vocabulary WER;
- named-entity accuracy for repo/branch/path/version;
- partial transcript latency;
- final transcript latency;
- end-of-turn detection latency;
- false command activation rate;
- transcript correction rate;
- confirmation-trigger precision/recall for ambiguous critical entities;
- barge-in stop latency;
- CPU/RAM/VRAM load;
- offline availability;
- provider fallback success.

## Safety scenarios
- ambiguous destructive command;
- low-confidence branch name;
- spoken secret/token accidentally included;
- microphone permission denied;
- provider outage mid-turn;
- network loss during cloud voice;
- local ASR model unavailable;
- background speech accidentally detected;
- user says "cancele" while agent action is pending;
- transcript differs materially from detected intent.

No destructive/high-impact action may proceed from low-confidence or materially ambiguous voice transcription without required confirmation.

## Rich response golden corpus
Test responses containing:
- long-form technical explanation;
- code + diff + findings;
- Mermaid architecture;
- React Flow-compatible interactive graph spec;
- chart + accessible data table;
- screenshot/image with provenance;
- multiple citations;
- Work Order proposal;
- ADR proposal;
- agent council summary with dissent;
- malformed/malicious diagram or chart spec;
- 500+ message long conversation.

## Visual/performance gates
Candidate targets to benchmark/freeze later:
- composer remains responsive during streaming;
- completed message blocks do not rerender on unrelated token stream updates;
- long conversation virtualization keeps bounded DOM size;
- diagram/chart rendering never blocks text availability;
- reduced/efficient mode removes heavy effects while preserving semantics;
- voice waveform/orb reacts to real state, not synthetic random animation;
- no long task caused by ordinary message rendering beyond established cockpit budget.

## Accessibility gates
- typed and voice workflows have equivalent final capability where safe;
- every audio response has text equivalent;
- every diagram/chart has semantic alternative;
- keyboard-only operation of microphone, stop, send, source drawer, artifact actions and agent rail;
- screen-reader announcements do not spam partial transcript updates;
- reduced-motion preference honored.

## Provider bake-off
Benchmark at least:
- browser/on-device SpeechRecognition where available;
- whisper.cpp local adapter candidate;
- sherpa-onnx local/streaming candidate;
- one cloud realtime provider when operator allows.

Promotion criteria consider correctness, Portuguese-BR terminology, latency, resource contention with local AI workloads, privacy, cost and setup friction. Lowest latency alone does not win.

## Rich renderer bake-off
- Mermaid: ADOPT candidate for versionable deterministic diagrams.
- React Flow: TRIAL candidate for interactive graphs.
- chart renderer: benchmark ECharts-style provider plus lightweight SVG fallback.

## Reject conditions
Reject/fix any design that:
- silently turns uncertain transcript into critical action;
- requires cloud voice for normal standalone use;
- makes text unavailable when TTS/voice fails;
- exposes raw chain-of-thought as agent collaboration;
- executes arbitrary model-produced JS/HTML/SVG;
- fabricates chart/diagram/image evidence;
- makes the chat unusable on reduced graphics profile;
- materially competes with HIVE/UGAS/local model GPU workload without automatic degradation.