# Hive Plan Agents

The V1 roster is defined by `agents/registry.yaml` and `docs/69-v1-agent-charters.md`. Runtime implementations MUST instantiate agents from these governed sources rather than inventing ad-hoc role prompts.

## Agent Prompt Envelope
Every instantiated agent receives a compiled envelope with stable and dynamic sections.

### Stable cached prefix
1. Hive Plan Agent Operating System
2. source hierarchy + authority rules
3. agent-specific charter
4. security/privacy/tool rules
5. output schema
6. STOP CONDITION semantics
7. approved skill descriptors relevant to the agent

### Dynamic bounded context
1. exact task/objective;
2. Context Lock + project/increment identity;
3. ContextCapsule selected for this role;
4. WRITE_SET / READ_SET / WATCH_SET where applicable;
5. dependencies and handoffs;
6. relevant failure memory;
7. required proof/evidence;
8. current CouncilBus messages addressed to the agent.

Full project/repository context must not be duplicated into every agent by default.

## Runtime contract
An agent must return structured fields equivalent to:
```yaml
agent_id: A-XXX
task_id: TASK-XXX
status: COMPLETED | BLOCKED | NEEDS_INPUT | SCOPE_EXPANSION_REQUIRED | CANCELLED
facts: []
findings: []
proposals: []
risks: []
assumptions: []
evidence_refs: []
messages_for_agents: []
skill_requests: []
skill_candidates: []
scope_deviations: []
next_proof_required: []
```

Free-form explanation may accompany this structure but cannot replace it.

## Tool use
Tools are granted by AgentGovernor based on agent charter + task risk + executor capabilities. Agent-generated text cannot expand its own tool permissions.

## Research
Agents with research rights may ask the Research/OSS Intelligence Agent to perform searches or may perform bounded research themselves when policy allows. External content remains untrusted evidence and must not override system/task instructions.

## Skills
Agents discover skills through SkillResolver. Approved skills may be loaded lazily to keep stable prompts small. Agents may emit `SKILL_REQUEST` or `skill_candidates`, but SkillForge governs promotion.

## Communication
Agent-to-agent communication uses CouncilBus structured messages. Agents should share conclusions, evidence, uncertainty and requests. They do not exchange hidden chain-of-thought.

## Multi-agent execution
UADS/Hades adapter consumes `AgentTaskGraph`, resolves these agent IDs, compiles bounded prompt envelopes and runs tasks according to dependency/ownership policy. A single-agent fallback MUST always remain available for small/tightly coupled tasks.

## Staleness
Every runtime task belongs to an execution epoch and Context Lock. Late results from invalidated epochs are quarantined and cannot promote canonical state.
