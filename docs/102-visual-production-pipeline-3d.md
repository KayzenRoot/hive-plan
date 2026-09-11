# HP-PLAN-010 — Visual Production Pipeline / 3D

Status: PROPOSED

## Mission
Create a premium visual system for Hive Plan with realistic 3D, fluid motion, high-end materials and lighting, while keeping the runtime responsive, accessible and hardware-aware.

## Tooling policy
Asset creation may use Blender, Maya, Substance-style texturing tools, procedural generators, approved MCP adapters and other DCC tools when they improve quality. Tool choice is not part of the runtime contract. Runtime delivery remains browser-compatible and performance-budgeted.

## Authoring pipeline
Concept -> blockout -> high-poly where justified -> retopology -> UV -> PBR materials -> baked normals/AO where useful -> LODs -> animation/rig -> export validation -> glTF/GLB -> mesh/texture compression -> runtime integration -> visual/performance QA.

## Preferred interchange
Use glTF 2.0 / GLB as the primary interchange for realtime browser assets. Authoring files (.blend/.ma/.mb/etc.) remain source assets and are not runtime dependencies.

## Asset classes
- HERO: Hive Core and focal interactive objects;
- SYSTEM_NODE: agents, HIVE/UADS/UGAS, GitHub, review/evidence nodes;
- AMBIENT: decorative background geometry/particles;
- UI_3D: shallow-depth control-room elements and transitions;
- EFFECT: energy flows, particles, pulses and state indicators.

Each class gets triangle, texture, animation and draw-call budgets appropriate to its importance.

## Material direction
PBR-first materials with restrained realism:
- dark anodized metal / graphite;
- smoked/translucent glass;
- emissive electric cyan/violet state lighting;
- selective clearcoat / roughness variation;
- micro-surface detail only where visible;
- no expensive shader complexity without measurable visual benefit.

## Lighting
Prefer baked/environment lighting and a small number of purposeful dynamic lights. Real-time lighting is reserved for meaningful state changes and focal interaction. Lighting must degrade gracefully with graphics profile.

## Motion
Animation must feel physical and intentional:
- spring/inertial transitions;
- eased camera moves;
- subtle idle motion;
- state pulses tied to real events;
- no perpetual heavy animation for decoration;
- reduced-motion profile removes nonessential movement without losing information.

## DCC automation
Where useful, approved MCP/tool adapters may automate:
- Blender scene setup;
- export validation;
- naming conventions;
- LOD generation;
- texture packing;
- camera turntables;
- comparison renders;
- asset metadata extraction.

Automation cannot bypass artifact provenance, license checks or visual QA.

## Asset provenance
Every production asset records source, license/ownership, authoring tool, version, export settings, digest and runtime target. Generated/concept assets are labeled and cannot be treated as runtime evidence until integrated and validated.

## STOP CONDITION
Do not freeze until authoring pipeline, interchange format, asset classes, material/lighting rules, provenance and export validation are testable.