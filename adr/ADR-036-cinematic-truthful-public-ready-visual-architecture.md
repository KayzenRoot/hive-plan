# ADR-036 — Cinematic, Truthful and Public-Ready Visual Architecture

Status: ACCEPTED  
Date: 2026-09-11  
Increment: HP-PLAN-010

## Context
Hive Plan is internal-first but may later become a public commercial product. Its interface must be memorable and premium without sacrificing engineering truth, accessibility, performance or forcing SaaS scope into V1.

## Decision
Adopt `Obsidian Glass / Electric Signal` as the product visual language. Cinematic quality is achieved through coherent materials, lighting, motion, depth and spatial composition, not by hiding state behind decoration.

Hive Core and VoiceOrb are signature visual systems. Critical information always has a semantic DOM/text equivalent through VisualTruthMirror or equivalent accessible representation. 3D and heavy visual effects degrade through governed graphics profiles and ResourcePeacekeeper before interaction or engineering assurance is degraded.

Preserve future public-product seams such as theme/token independence, user/workspace/project UI boundaries, capability/entitlement-ready presentation seams, internationalization-ready strings, redistribution-safe asset provenance and privacy provenance. Do not add V1 billing, subscription enforcement, public auth, multi-tenancy or marketplace scope without separate authorization.

## Consequences
- the product can be visually distinctive from its first implementation;
- cinematic UI cannot fabricate health/activity or become the sole truth representation;
- future commercialization remains possible without prematurely building a SaaS platform;
- visual quality has accessibility/performance/evidence gates.

## Rejected alternatives
- generic dashboard styling with no product identity;
- glass/3D effects applied everywhere;
- fake activity for visual spectacle;
- public SaaS infrastructure pulled into V1 only as future-proofing.