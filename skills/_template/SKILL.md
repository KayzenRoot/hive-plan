---
name: replace-me
description: Describe exactly what this skill does and when an agent should activate it.
license: Proprietary unless otherwise specified
compatibility: Hive Plan governed agent runtime; declare external requirements explicitly.
metadata:
  hive-plan-status: CANDIDATE
  hive-plan-version: "0.1.0"
  owner-agent: A-008
  risk-class: STANDARD
allowed-tools: ""
---

# Purpose
State the reusable capability and exact applicability boundary.

# Preconditions
- Required inputs/context.
- Environment/tool prerequisites.
- Conditions where this skill MUST NOT be used.

# Procedure
1. Use deterministic checks first where possible.
2. Perform the bounded procedure.
3. Validate outputs against the declared contract.
4. Record evidence and deviations.

# Output Contract
Define machine/human-readable outputs, evidence pointers and failure states.

# Failure / Edge Cases
List known failure modes, recovery/escalation behavior and STOP conditions.

# Security & Scope
Declare network/write/secret/data permissions required. A skill cannot self-grant permissions beyond AgentGovernor policy.

# Tests
Reference deterministic/golden/sandbox tests required before promotion.

# Examples
Provide concise valid examples and at least one negative/misuse example.

# Provenance
Record creator, source inspirations/references, reviewed-by, fingerprints and supersession information in `skill.manifest.json`.