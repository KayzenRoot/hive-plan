# Hive Plan Skills

This directory is the governed registry for reusable agent capabilities.

A skill is reusable procedural knowledge, not authority. Skills inherit AgentGovernor restrictions and cannot grant themselves tools, filesystem scope, network rights, secrets, write access or approval authority.

Lifecycle: `CANDIDATE → TRIAL → APPROVED → DEPRECATED/REVOKED`.

Before creating a skill, agents must search the catalog and prefer reuse/composition over duplication. New or changed skills require validation appropriate to their risk class. See `docs/67-skill-fabric.md`.

Recommended package:
```text
skills/<skill-name>/
├── SKILL.md
├── skill.manifest.json
├── tests/
├── scripts/          # optional
├── references/       # optional
├── assets/           # optional
└── CHANGELOG.md
```

The initial template lives at `skills/_template/SKILL.md`.