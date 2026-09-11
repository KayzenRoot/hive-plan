# HP-PLAN-010 — Visual Bible: Concrete Design Token Candidates

Status: PROPOSED / BENCHMARK-BOUND

## Product ambition
Hive Plan is internal-first but public-ready by architecture. The visual system must support a premium commercial product without forcing a future redesign of core UI primitives.

## Color candidates
Values are implementation candidates subject to contrast/display validation.
- color.bg.void: #05070B
- color.bg.obsidian.1: #080B12
- color.bg.obsidian.2: #0C111B
- color.bg.obsidian.3: #111827
- color.surface.solid: #111722
- color.surface.elevated: #151D2A
- color.glass.tint: rgba(18, 28, 43, .62)
- color.border.subtle: rgba(150, 190, 230, .14)
- color.signal.cyan: #39E7FF
- color.signal.blue: #4D8DFF
- color.signal.violet: #9B6CFF
- color.success: #36D99A
- color.warning: #FFB84D
- color.danger: #FF5D73
- color.text.primary: #F3F7FC
- color.text.secondary: #AAB8CB
- color.text.muted: #738298

Operational colors require non-color icon/text encoding.

## Spacing
Base unit 4px. Candidate scale: 0, 4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80.

## Radius
- r.xs 4
- r.sm 7
- r.md 10
- r.lg 14
- r.xl 20
- r.orb/full 999
Dense technical surfaces favor xs-sm; ambient/floating surfaces favor md-xl.

## Blur
- none 0
- subtle 8
- utility 14
- floating 20
- cinematic 28 maximum candidate
Blur is graphics-profile aware and cannot be required for information separation.

## Elevation
D0..D5 combines luminance, border and bounded shadow. Avoid multiple stacked shadows. Focus/critical state primarily changes border/signal rather than giant glow.

## Typography candidate scale
- display 32/38
- h1 26/32
- h2 22/28
- h3 18/24
- body 15/22
- bodyDense 14/20
- label 13/18
- caption 12/16
- metric 20/24 tabular
- code 13/20
Font families remain benchmark/licensing choices; prefer self-hostable variable sans + legible monospace.

## Layout tokens
- header target: 68px
- nav collapsed target: 80px
- right rail: clamp(300px, 25vw, 420px)
- content max prose: ~760px
- technical wide: up to viewport-safe width
- telemetry strip target: 32-40px
All targets adapt through density/responsive rules.

## Animation candidate bands
- micro 90-140ms
- fast 140-220ms
- standard 220-360ms
- focus 350-650ms
- causal event: data-bound, capped
Reduced motion collapses to minimal/near-instant state transition.

## Token governance
No feature screen hard-codes visual values when a semantic token exists. Token changes require visual regression and accessibility evidence.