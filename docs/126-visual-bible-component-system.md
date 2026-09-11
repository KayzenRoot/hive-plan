# HP-PLAN-010 — Visual Bible: Component System

Status: PROPOSED

## Component architecture
Components are grouped into primitives, operational components, rich-response components and spatial components.

## Primitives
Surface, Stack, Grid, Divider, Text, Icon, Button, IconButton, Input, Select, Tooltip, Popover, Dialog, Drawer, Tabs, Badge, Progress, Skeleton, ScrollArea.
All primitives consume semantic tokens rather than hard-coded visual values.

## Operational components
StatusBadge, HealthIndicator, FreshnessBadge, AuthorityBadge, RiskBadge, QualityFloorBadge, CostMetric, ResourceMeter, BlockerCard, IncidentCard, WorkOrderCard, ReviewCard, FindingCard, EvidenceCard, CheckpointCard, GitHubEntityCard, AgentChip, AgentTaskNode, SourceFingerprint, ContextLockStatus.

## Rich-response components
NarrativeBlock, CalloutBlock, CodeBlock, DiffBlock, TableBlock, MetricGrid, TimelineBlock, DiagramBlock, GraphBlock, ChartBlock, ImageBlock, SourceBlock, AgentCouncilBlock, ArtifactProposalBlock, EvidenceExpandable.
Unknown rich blocks fall back to readable structured content.

## Spatial components
HiveCoreScene, SystemNode3D, RelationshipEdge3D, EventFlow3D, VoiceOrb3D, KnowledgeConstellation, ArchitectureLensGraph, ProofGraphView, AgentTaskGraphView, VisualTruthMirror.

## State contract
Applicable components implement explicit states: DEFAULT, HOVER, FOCUS_VISIBLE, ACTIVE, SELECTED, DISABLED, LOADING, CURRENT, STALE, DEGRADED, BLOCKED, ERROR, SUCCESS, UNKNOWN.

## Component provenance
Operational cards show source/freshness when relevant. No component may visually present derived/model-proposed data as verified canonical data without authority labeling.

## Composition rules
- Glass utility around content, not behind dense code/diff.
- One dominant focal object per major view.
- Critical alerts cannot be visually drowned by ambient signal effects.
- Charts/graphs include textual/table alternatives.
- Large cards use progressive disclosure rather than walls of metadata.

## Interaction
Keyboard/focus behavior is defined at component level. Pointer hover is never the only discovery mechanism. Touch targets remain usable in comfortable/default modes.

## Testing
Each component receives story/golden states, accessibility checks, keyboard tests and visual regression. Operational components also receive truth-state tests.

## STOP CONDITION
Component system freezes after representative implementations demonstrate consistent tokens, state behavior, accessibility and graphics-profile degradation.