# HP-PLAN-010 — GitHub / Delivery Detailed Layout

Status: PROPOSED

## Mission
Make repository delivery state understandable without leaving Hive Plan while preserving GitHub as canonical source.

## Primary zones
- Delivery header: repository, branch, active increment, Work Order, release/version;
- Delivery River: issue -> branch -> commits -> PR -> checks -> review -> checkpoint -> merge -> release;
- PR/CI workbench;
- source freshness/fingerprint panel;
- release readiness rail;
- recent delivery timeline.

## Delivery River
A horizontally/vertically adaptive graph uses real GitHub entities. Nodes expose exact IDs/SHA/state. Animated flow occurs only on observed transitions. Blocked/stale/failed states interrupt the path visibly.

## PR/CI workbench
Shows changed surface, required checks, terminal states, failing jobs, artifacts and exact head SHA. Opening a failure can route to Review/Diagnostics while retaining WO identity.

## Source integrity
Display Context Lock freshness, canonical-source fingerprint changes, unexpected branch drift, missing evidence and checkpoint lag.

## Release readiness
Readiness is multidimensional: functional, tests, docs, deployment/recovery evidence, unresolved findings, security gates and release notes. No single decorative percentage can override blockers.

## Voice
`qual check falhou?`, `abra o PR ativo`, `o Context Lock está válido?`, `o que falta para merge?`, `compare a branch com main`.

## Degraded state
GitHub unavailable shows last verified watermark/time and disables mutation. Cached state is visibly STALE rather than current.