# Reviewer Anti-Drift Policy

Status: FROZEN — HP-PLAN-006

Every review agent is constrained by snapshot, ReviewScope, assigned questions, canonical sources and output schema. Agents must not expand product scope, rewrite architecture, introduce optional features or transform review into general refactoring advice.

Any newly discovered material dependency is returned as a scope-expansion evidence edge to ReviewScope Compiler, which decides whether to expand review under policy.