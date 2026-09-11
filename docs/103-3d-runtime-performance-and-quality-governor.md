# HP-PLAN-010 — 3D Runtime Performance + Quality Governor

Status: PROPOSED

## Mission
Deliver premium 3D without allowing visuals to compromise interaction, local AI workloads, battery/thermals or accessibility.

## Runtime principles
- 60 FPS is the preferred interactive target on capable desktop hardware;
- interaction latency and semantic correctness outrank visual fidelity;
- no critical state exists only in canvas;
- graphics quality adapts continuously within bounded profiles;
- local AI/UGAS/HIVE workloads can temporarily reclaim GPU/CPU resources.

## Graphics profiles
CINEMATIC: maximum approved quality for idle/demo/high-headroom use.
QUALITY: premium daily mode.
BALANCED: default adaptive mode.
EFFICIENT: reduced GPU/CPU and blur/particle load.
ACCESSIBLE: minimal nonessential motion and guaranteed semantic DOM mirror.
SAFE_2D: canvas disabled or unsupported; full product remains usable.

## FrameBudget Governor
Observe rolling frame time, long tasks, GPU pressure signals where available, tab visibility and interaction demand. Adjust only within policy:
- DPR/render scale;
- shadow quality;
- post-processing;
- particle density;
- reflection/refraction quality;
- animation update rate;
- LOD threshold;
- texture mip/quality tier;
- optional effects.

Do not dynamically hide or change semantic system status.

## ResourcePeacekeeper
Coordinate graphics with local compute demand. When local inference, HIVE indexing, UGAS generation or other heavy work is detected, reduce visual resource consumption before degrading engineering functionality.

## Asset optimization
- glTF/GLB optimized for runtime;
- mesh compression evaluated with Meshopt/Draco as appropriate;
- KTX2/Basis-class texture compression;
- mipmaps and texture-size caps;
- LODs for meaningful geometry;
- instancing for repeated objects;
- merge/batch where it reduces draw calls without harming interaction;
- dispose GPU resources deterministically.

## Effects budget
Bloom, depth effects, reflections, glass/refraction and particles are allowed only behind measurable cost budgets. Expensive full-screen effects must prove visual value. Cinematic effects may be disabled during heavy interaction.

## Performance acceptance direction
Benchmarks must record at minimum frame-time distribution, long tasks, CPU/RAM/VRAM where measurable, draw calls, triangles, texture memory estimate, loading time and interaction responsiveness across graphics profiles.

## Degradation ladder
WebGPU -> WebGL2 -> reduced 3D -> static visual -> semantic 2D/DOM.

Fallback is a normal supported path, not an error screen.

## STOP CONDITION
Do not freeze until profile transitions, performance metrics, degradation paths, local-compute coexistence and semantic parity have deterministic evidence plans.