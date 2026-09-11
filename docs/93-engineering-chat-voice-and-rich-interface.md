# HP-PLAN-010 — Engineering Chat Voice + Rich Interface

Status: PROPOSED

## Mission
Make Engineering Chat a primary, voice-first engineering workspace that can be comfortably operated by speaking instead of typing while preserving provenance, authority, accessibility, performance, and exact artifact governance.

## Product principle
Voice is an input/output modality, not a weaker side channel. Any action available from typed chat that is safe to perform conversationally SHOULD be reachable by voice with the same authority gates and audit trail.

## Conversation surface
The chat is a full-width engineering workspace with:
- persistent conversation timeline;
- large multimodal composer;
- microphone / push-to-talk / hands-free modes;
- optional spoken assistant responses;
- live transcription preview;
- source/provenance drawer;
- agent participation strip;
- artifact cards for ADRs, Work Orders, checkpoints, findings, diagrams, graphs and images;
- expandable evidence and decision panels;
- Project Brain context indicator;
- model/cost/cache metadata collapsed by default;
- focus mode for long technical conversations.

## Voice architecture
Create a provider-neutral `VoiceProvider` contract. V1 routing priority:
1. LOCAL_ON_DEVICE when browser/host capability and quality are sufficient;
2. LOCAL_NATIVE provider such as whisper.cpp / sherpa-onnx behind adapter;
3. CLOUD_REALTIME provider when enabled by operator policy;
4. browser Web Speech fallback where supported;
5. typed input always remains available.

No single browser speech API is an architectural dependency.

### Voice modes
- PUSH_TO_TALK: safest default for engineering commands.
- CONTINUOUS_CONVERSATION: optional hands-free session with clear listening state.
- DICTATION: transcribe only, operator edits/sends.
- COMMAND_MODE: bounded recognized commands such as "abra o projeto", "mostre o review", "gere o diagrama", "pare", "cancele".
- READ_ALOUD: TTS of selected assistant content.

### Voice UX states
IDLE, REQUESTING_PERMISSION, LISTENING, SPEECH_DETECTED, TRANSCRIBING, REVIEW_TRANSCRIPT, SENDING, ASSISTANT_THINKING, SPEAKING, INTERRUPTED, DEGRADED, OFFLINE, ERROR.

Every state must be visible and screen-reader announced where relevant. There is no invisible microphone state.

## Voice safety
- destructive/irreversible/high-impact actions require explicit confirmation regardless of voice confidence;
- low ASR confidence must never silently mutate command semantics;
- critical entity names, branch names, repository names, amounts, versions and file paths receive transcript confirmation when ambiguity is detected;
- barge-in is allowed for stopping audio generation or cancelling a pending conversational action;
- raw audio retention defaults to OFF unless explicitly enabled;
- transcripts follow project privacy/retention policy;
- audio and transcript provenance identify provider and processing mode;
- voice transcript is conversational input, never canonical truth by itself.

## Local-first voice candidates
Evaluate behind adapters:
- browser on-device SpeechRecognition where available;
- whisper.cpp for local/offline ASR, especially Windows/NVIDIA and CPU fallback;
- sherpa-onnx for streaming/offline ASR, VAD, keyword spotting and WASM/native deployment;
- faster-whisper as optional local service candidate when Python/CTranslate2 integration is justified.

Provider promotion is benchmark-gated by Portuguese-BR WER, engineering-term accuracy, latency, CPU/RAM/VRAM pressure, streaming quality, privacy and installation friction.

## Cloud realtime candidate
A cloud realtime voice provider may be enabled behind `VoiceProvider` for low-latency speech-to-speech. It cannot become mandatory for standalone operation and must obey project privacy and budget policy.

## Visual language
Extend Obsidian Glass / Electric Signal into chat:
- restrained glass panels;
- depth layers and subtle parallax;
- voice waveform / orb tied to real microphone/assistant state;
- agent presence chips with meaningful activity states;
- soft motion on streamed content and artifact promotion;
- high-contrast code/diff surfaces remain mostly solid;
- reduced-motion and efficient graphics profiles preserve full functionality.

Glass and animation communicate state. They are not decoration that reduces legibility.

## Performance guard
Voice visualization and chat effects are subject to RenderBudget Governor and ResourcePeacekeeper. Heavy local inference, UGAS rendering or HIVE indexing can automatically reduce waveform/particles/blur/3D effects without affecting interaction.

## Accessibility
- full keyboard operation;
- visible focus;
- captions/transcript always available when voice is active;
- spoken response never replaces text response;
- reduced-motion support;
- screen-reader landmarks for messages, sources, artifacts, findings and agent activity;
- color never sole state indicator.

## Metrics
Track opt-in operational metrics such as:
- voice session latency;
- ASR partial/final latency;
- operator correction rate;
- command cancellation rate;
- provider fallback rate;
- TTS first-audio latency;
- CPU/RAM/VRAM use;
- Portuguese-BR engineering vocabulary error rate;
- transcript-to-intent disagreement.

## STOP CONDITION for this submodule
Do not freeze until voice provider abstraction, privacy model, command confirmation policy, fallback path, accessibility, performance budgets and Portuguese-BR eval plan are explicit and testable.