# V1 Architecture

Status: PLANNING BASELINE

```text
                           ┌────────────────────┐
                           │   Hive Plan UI     │
                           │  Command Cockpit   │
                           └─────────┬──────────┘
                                     │
                           ┌─────────▼──────────┐
                           │ Application / API  │
                           └─────────┬──────────┘
                                     │
             ┌───────────────────────┼────────────────────────┐
             │                       │                        │
   ┌─────────▼─────────┐   ┌─────────▼──────────┐   ┌────────▼─────────┐
   │ Planning Council  │   │ Context Compiler   │   │ GitHub Steward   │
   │ + Interviewer     │   │ RAG/cache/router   │   │ observer/actions │
   └─────────┬─────────┘   └─────────┬──────────┘   └────────┬─────────┘
             │                       │                        │
             └──────────────┬────────┴───────────────┬────────┘
                            │                        │
                  ┌─────────▼──────────┐   ┌────────▼─────────┐
                  │ Work Order Engine  │   │ Review + Audit   │
                  └─────────┬──────────┘   └────────┬─────────┘
                            │                        │
                         Codex                   Checkpoint
                       (external)                    │
                            │                        │
                            └──────────GitHub────────┘

MemoryProvider ──► Hive V1 (preferred)
               └► Embedded Local RAG (fallback)

Optional ecosystem adapters ──► UADS/Hades V1
                             └► UGAS V1
```

## Architectural rules
1. Provider interfaces isolate external/model/ecosystem dependencies.
2. Deterministic computation precedes LLM reasoning whenever possible.
3. Canonical truth is versioned; chat state is ephemeral/non-canonical.
4. Review and audit are independent concerns.
5. Completion trigger and completion evidence are separate concerns.
6. Every consequential action is traceable to project, Work Order, actor/agent, Git SHA, and timestamp.
7. LLM calls are observable and cost-attributed.
8. Secrets never enter prompt context.
9. Local-first boundaries are preserved so future SaaS/multi-user evolution does not require rewriting domain logic.
10. UI reads from a normalized project-state model, not directly from provider-specific APIs.

## Initial service boundaries
- `web`: cockpit/chat frontend.
- `api`: authenticated local application boundary.
- `orchestrator`: workflow/state-machine coordination.
- `planning`: agent roles and planning protocol.
- `context`: source resolution, retrieval, compilation, cache.
- `llm-gateway`: provider adapters, routing, budgets, telemetry.
- `github`: token vault adapter, repository operations, observation.
- `work-orders`: compilation/versioning/correction deltas.
- `review`: evidence acquisition and technical review.
- `audit`: independent policy/evidence verification.
- `checkpoint`: continuity/canonical delta management.
- `events`: local event bus/outbox for durable workflow transitions.
- `storage`: PostgreSQL + vector capability; Redis optional/conditional after benchmarking.

Exact process topology may be collapsed into fewer deployable containers in V1 to avoid premature microservices.
