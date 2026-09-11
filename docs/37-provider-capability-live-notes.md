# Provider Capability Live Notes

Status: LIVING / NON-CANONICAL CONFIG INPUT  
Observed: 2026-09-11

## Purpose
Track current provider features that may improve Hive Plan routing/caching. These notes are operational research, not frozen architecture. Provider behavior, model names, pricing and limits can change and must be refreshed before implementation/runtime configuration changes.

## OpenAI
Current Responses API documentation indicates GPT-5.6+ prompt caching supports `prompt_cache_key`, `prompt_cache_options`, implicit caching and up to four explicit breakpoints written per request. Current documented TTL for the new cache options is 30 minutes.

Architecture implication:
- stable system/project prefixes can be segmented for provider caching;
- cache diagnostics/usage should feed CacheFabric telemetry;
- provider cache semantics remain inside the OpenAI adapter.

Source:
- https://developers.openai.com/api/reference/cli/resources/responses/methods/create

## Google Gemini
Current Gemini documentation states implicit context caching is enabled by default for Gemini 2.5 and newer models, with model-specific minimum token thresholds. Explicit `CachedContent` is also available through generateContent flows, while the newer Interactions API currently supports implicit caching only.

Architecture implication:
- CacheFabric should distinguish implicit-hit optimization from explicitly managed cache objects;
- provider capability detection should choose the appropriate API path rather than assuming one universal cache mechanism;
- stable large prefixes/corpora are candidates for explicit caching only when expected reuse justifies storage/write cost.

Sources:
- https://ai.google.dev/gemini-api/docs/caching
- https://ai.google.dev/api/caching

## Anthropic Claude
Current Claude Platform documentation supports automatic prompt caching and explicit cache breakpoints with `cache_control`. The documented default cache lifetime is 5 minutes, with a 1-hour option at additional write cost. The provider supports up to four cache breakpoint slots in relevant flows.

Architecture implication:
- CacheValuePredictor should consider write multiplier/TTL/reuse probability rather than automatically creating long-lived cache entries;
- automatic vs explicit caching belongs in the Anthropic adapter;
- stable-prefix design remains portable across providers even though APIs differ.

Source:
- https://platform.claude.com/docs/en/build-with-claude/prompt-caching

## Provider lifecycle monitoring
Model IDs and availability are not architecture. ModelMesh should periodically or manually refresh:
- active/deprecated/retired state;
- capabilities;
- context limits;
- structured output/tool support;
- cache semantics;
- price;
- latency/health observations;
- data/privacy constraints.

A provider/model retirement must not require application architecture changes. It should invalidate/update configuration/eval profiles and trigger RouteLab validation of replacements.

## Rule
Never promote a provider capability from these live notes into a frozen architectural dependency without an ADR/Decision and benchmark/eval evidence.