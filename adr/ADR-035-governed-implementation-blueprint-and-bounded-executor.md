# ADR-035 — Governed Implementation Blueprint and Bounded Executor

Status: ACCEPTED  
Date: 2026-09-11  
Increment: HP-PLAN-010

## Context
Low-cost executors can waste tokens and introduce defects when they must rediscover architecture, scope and implementation strategy from a short prompt.

## Decision
Adopt a governed `Implementation Blueprint` compiled from the authorized Work Order, Context Lock, repository reality, ChangeGraph, FailureShield and TestLens. The blueprint moves high-value engineering reasoning upstream and renders a compact executor prompt.

Guidance depth is G0 CONTRACT_ONLY, G1 STRUCTURAL, G2 ALGORITHMIC or G3 NEAR_EXECUTABLE according to risk, ambiguity, novelty, executor capability and expected rework cost.

Every blueprint carries scope, change surface, file/symbol plan, contracts, tests, evidence, STOP condition and a decision budget of FROZEN, BOUNDED, OPEN_LOCAL or ESCALATE. Executor freedom is bounded. Material repository mismatch emits a `blueprint_deviation` artifact with evidence and impact. Scope expansion, contract change, invalidated tests or stale Context Lock cannot be accepted as a silent local correction.

Review binds to the exact Work Order, Context Lock, Blueprint and execution head used.

## Consequences
- cheaper models can execute precise plans rather than redesign architecture;
- prompt/token savings are measured by total Verified Outcome Cost, not single-call cost;
- deviations become auditable instead of hidden improvisation;
- G3 is used selectively rather than everywhere.

## Rejected alternatives
- generic one-line implementation prompts for complex work;
- executor silently redesigning frozen architecture;
- assuming detailed prompts are always cheaper;
- accepting executor completion claims without exact-head evidence.