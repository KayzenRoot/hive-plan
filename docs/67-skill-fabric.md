# Skill Fabric / SkillForge

Status: PROPOSED FOR FREEZE — HP-PLAN-007

## Mission
Give Hive Plan agents reusable procedural capabilities without bloating every agent prompt or recreating expertise repeatedly.

Hive Plan SHOULD use an Agent Skills-compatible packaging model where practical: a skill is a directory with a required `SKILL.md` plus optional scripts, references and assets. The Hive Plan governance layer adds provenance, testing, risk, versioning and promotion metadata.

## Skill lifecycle
```text
NEED DETECTED
   ↓
SkillCatalog search
   ↓
REUSE / COMPOSE / CANDIDATE NEW SKILL
   ↓
SkillForge sandbox
   ↓
Schema + security + deterministic tests
   ↓
Specialist review
   ↓
Skill benchmark / examples
   ↓
APPROVED / TRIAL / REJECTED
   ↓
Versioned Skill Registry
   ↓
Agent assignment + telemetry
```

## Skill classes
- ANALYSIS: repeatable inspection/reasoning procedure.
- TOOLING: wraps deterministic commands/APIs.
- RESEARCH: current-source discovery/evaluation.
- REVIEW: defect/risk detection procedure.
- DELIVERY: Git/GitHub/CI/release workflow.
- DOMAIN: specialized business/technical knowledge.
- TRANSFORMATION: structured artifact conversion/generation.
- RECOVERY: diagnosis/repair/rollback procedure.

## Skill package
Recommended structure:
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

## skill.manifest.json additions
- skill_id;
- version;
- status: CANDIDATE | TRIAL | APPROVED | DEPRECATED | REVOKED;
- owner_agent_role;
- allowed_agent_roles;
- task_classes;
- required tools/capabilities;
- network requirement;
- data sensitivity ceiling;
- write/side-effect capabilities;
- assurance ceiling;
- deterministic test refs;
- benchmark refs;
- source/provenance;
- dependency/license metadata;
- fingerprint;
- reviewed_by;
- supersedes/superseded_by.

## Skill creation authority
Any qualified agent MAY create a candidate skill when:
- the same procedure is likely to recur;
- a complex procedure would otherwise be repeatedly re-derived;
- standardization materially improves correctness or speed;
- another agent needs the capability;
- a verified failure suggests a reusable prevention/diagnostic procedure.

Before creating, the agent MUST search SkillCatalog to avoid duplication.

## Promotion rules
LOW-risk read-only skills may reach TRIAL after automated validation + specialist review.
Skills that write code, mutate Git, access secrets, deploy, modify infrastructure, execute external code, affect auth/security/data or perform irreversible actions require stronger review/authorization.

A skill is never trusted simply because its creator is a strong model.

## Skill validation
Validation can include:
- frontmatter/manifest schema;
- instructions completeness;
- tool permission checks;
- malicious/prompt-injection content scan;
- secret scan;
- license/dependency checks;
- deterministic unit/golden tests;
- sandbox execution where code exists;
- failure/edge-case examples;
- before/after benchmark;
- reproducibility;
- rollback/removal behavior.

## Skill selection
`SkillResolver` ranks candidate skills by:
- exact task-class match;
- risk compatibility;
- environment compatibility;
- recency/version support;
- verified success rate;
- token/context cost;
- latency;
- prior project success;
- dependency health.

Semantic similarity alone cannot auto-activate a mutating/high-risk skill.

## Skill composition
Skills MAY compose other approved skills through explicit dependencies. Composition must prevent:
- circular invocation;
- permission escalation;
- hidden network/write privileges;
- duplicated side effects;
- incompatible assumptions.

## Skill portability
Hive Plan's core skill instructions should remain executor/model neutral. UADS/Hades/Codex-specific rendering belongs in adapters or compatibility metadata.

## Skill learning
After each use, record:
- success/failure;
- task class;
- runtime/cost;
- warnings;
- false assumptions;
- human intervention;
- downstream review findings;
- escaped defects attributable to the skill;
- compatibility changes.

`SkillFitness` is measured by verified outcomes, not usage count.

## Failure Vaccine integration
A recurring verified failure can create a `SKILL_CANDIDATE` containing:
- detection method;
- prevention rule;
- correction procedure;
- regression test guidance;
- applicability boundaries.

This converts mistakes into reusable organizational capability.

## Skill sharing between agents
An agent can publish a `SKILL_REQUEST` on CouncilBus specifying:
- need/problem;
- required capability;
- risk;
- input/output contract;
- needed tools;
- urgency;
- reuse likelihood.

Skill Engineer/qualified specialist may satisfy it with an existing skill, composition or candidate creation.

## Security boundary
Skill instructions, references and imported third-party material are untrusted until validated. Skills cannot grant themselves tools, secrets, filesystem scope or authority beyond AgentGovernor policy.

## Freeze boundary
Freeze SkillCatalog, SkillForge, lifecycle/statuses, reusable package structure, validation/promotion rules, SkillResolver, SkillFitness, skill requests/sharing, Failure Vaccine integration and portable executor-neutral semantics. Exact storage/runtime loader implementation remains a later ADR.