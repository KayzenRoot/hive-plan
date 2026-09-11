# HP-PLAN-007 Audit Checklist

- [x] Agent roles are authored canonically in Hive Plan rather than delegated to Codex/UADS design.
- [x] All 30 V1 roles have mission, activation, responsibilities, outputs and STOP semantics.
- [x] Machine-readable registry exists.
- [x] Agent prompt/runtime envelope is bounded and cache-friendly.
- [x] Multi-agent use is conditional, benchmarked and conflict-aware.
- [x] AgentTaskGraph remains executor-specific rendering, not canonical project truth.
- [x] WRITE_SET/READ_SET/WATCH_SET and dependency barriers are explicit.
- [x] Single-agent fallback remains supported.
- [x] Skill creation/reuse is governed, versioned and permission-bounded.
- [x] Research/web/GitHub content is treated as untrusted evidence.
- [x] Technology adoption includes license/security/maintenance/lock-in checks.
- [x] Structured agent communication and Dissent Ledger prevent hidden consensus.
- [x] Reviewer/Auditor independence is preserved.
- [x] Open-standard compatibility does not create mandatory MCP/A2A/runtime lock-in.
- [x] No production implementation is authorized by this increment.

Audit target: PR diff + Source Hierarchy + HP-CP-0017 + ADR-026/027.