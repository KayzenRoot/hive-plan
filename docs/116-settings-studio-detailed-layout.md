# HP-PLAN-010 — Settings / Studio Detailed Layout

Status: PROPOSED

## Mission
Centralize operator configuration while keeping preference, capability, authority and secret management clearly separated.

## Sections
1. General / project defaults;
2. Models & providers;
3. Voice & audio;
4. Visual / graphics studio;
5. Accessibility;
6. GitHub;
7. HIVE / UADS / UGAS integrations;
8. Memory/RAG policy;
9. Storage / backup / retention;
10. Security / privacy / secrets;
11. Agents / skills policy;
12. Notifications / automation;
13. Advanced diagnostics.

## Voice studio
- microphone/device test;
- provider selection/benchmark;
- language/pt-BR;
- push-to-talk/continuous/dictation defaults;
- VAD/noise settings;
- TTS voice/speed;
- privacy/local-only preference;
- interruption behavior.
A visual meter and test transcript provide immediate validation.

## Graphics studio
- CINEMATIC/QUALITY/BALANCED/EFFICIENT/ACCESSIBLE/SAFE_2D;
- automatic hardware profile;
- 3D enable;
- motion/reduced motion;
- particle/reflection/blur quality within safe bounded presets;
- UI density;
- live preview scene;
- ResourcePeacekeeper auto-degrade behavior.
Unsafe manual settings cannot disable semantic fallback.

## Provider/integration settings
Capability status, permissions, connection health and last verification are shown separately from secret values. Secrets use SecretVault abstraction and are never displayed in canonical artifacts/logs.

## Preference vs truth
Visual density, voice verbosity and layout are operator preferences. Review severity, evidence, source authority, QualityFloor policy and security gates cannot be cosmetically overridden.

## Change safety
Settings classify LIVE_SAFE / RESTART_REQUIRED / REINDEX_REQUIRED / HIGH_IMPACT. High-impact changes show affected capabilities and validation/rollback plan.

## Voice
`teste meu microfone`, `use modo gráfico balanceado`, `deixe a voz mais rápida`, `mostre integrações desconectadas`. Privileged/security changes still obey confirmation policy.