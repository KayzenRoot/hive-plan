# HP-PLAN-010 — Screen State + Transition Matrix

Status: PROPOSED

## Purpose
Prevent polished mockups from hiding missing product states. Every major screen must be designed for operational reality.

## Mandatory state families
Every applicable screen defines:
- LOADING_INITIAL;
- CURRENT;
- EMPTY_VALID;
- NOT_CONNECTED;
- DEGRADED;
- STALE;
- RECONCILING;
- BLOCKED;
- PERMISSION_REQUIRED;
- PARTIAL_DATA;
- ERROR_RECOVERABLE;
- ERROR_BLOCKING;
- OFFLINE_LOCAL;
- HISTORICAL;
- REDUCED_GRAPHICS;
- ACCESSIBLE_2D.

## Transition rules
State transitions are driven by projection/event truth. Animation can visualize a transition but cannot invent or delay the underlying state.

Critical transitions that must never be coalesced away:
- approval/rejection;
- blocker created/resolved;
- Work Order lifecycle;
- review verdict;
- CI terminal transition;
- connection loss/recovery;
- security/recovery incident;
- checkpoint/merge;
- historical mode enter/exit.

## Navigation continuity
Cross-screen navigation preserves project, selected entity, relevant time boundary and focus where valid. Example: clicking a HIGH finding in Cockpit opens Review Command Center already pinned to the exact Review Receipt/head SHA.

## Motion continuity
Shared-element transitions are permitted for cards/nodes that represent the same entity across screens. Identity must remain explicit; motion never substitutes for breadcrumb/title.

## Error UX
Errors state what failed, affected capability, whether truth may be stale, last successful watermark, safe retry/recovery and whether operator action is needed. `Something went wrong` alone is unacceptable.

## Empty UX
Empty is not error. Examples: no active review, no blockers, no UADS tasks. Empty states show truthful meaning and next safe action where relevant.

## Visual regression matrix
Golden screenshots/render tests cover representative combinations across:
- desktop sizes;
- graphics profiles;
- reduced motion;
- 100/125/150% scaling;
- WebGPU and WebGL2 fallback;
- semantic 2D mode;
- voice active/inactive;
- light resource pressure / heavy resource pressure;
- key operational states.

## STOP CONDITION
No visual surface passes readiness from a happy-path screenshot alone. Required states and transitions must have acceptance evidence.