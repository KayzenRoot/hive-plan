# Operational Security, Observability & Resilience Layer

Status: PROPOSED FOR FREEZE — HP-PLAN-008

## Mission
Make Hive Plan safe to operate continuously on a local workstation while remaining diagnosable, recoverable and resistant to silent corruption, stale authority, dependency outages and resource contention.

## 1. Security operating model

### Trust zones
1. **Operator UI** — local browser/cockpit.
2. **Hive Plan API** — command/validation boundary.
3. **Workers** — background execution with bounded capabilities.
4. **GitHub / model / external providers** — remote untrusted dependencies.
5. **HIVE / UADS / UGAS adapters** — privileged local integrations behind contracts.
6. **Artifact/data store** — durable local state.

### Default rules
- localhost-first binding;
- deny-by-default external network calls per capability;
- secrets never enter canonical project docs, logs, RAG chunks or prompts unless explicitly required and redacted/bounded;
- external text/repository content is untrusted data, not instruction authority;
- path traversal and symlink escape checks on any local project/data mount;
- public-repository pre-push secret/sensitive-data gate;
- least-privilege adapter scopes;
- mutating tool invocation requires agent/task authority + current Context Lock.

### SecretVault abstraction
V1 should expose a provider-neutral `SecretVault` API. Candidate Windows implementation paths are benchmarked/security-reviewed before freeze. Environment variables may bootstrap but are not the long-term secret-management abstraction.

Secret metadata stores identity/owner/provider/created/last-used/rotation policy, never plaintext in normal telemetry.

### Prompt/tool injection containment
Every external source receives an origin/trust label. AgentGovernor separates:
- SYSTEM/POLICY;
- CANONICAL_PROJECT;
- VERIFIED_EVIDENCE;
- EXTERNAL_UNTRUSTED;
- MODEL_PROPOSAL.

Untrusted source content cannot request tools, change agent authority or alter source priority.

## 2. Observability architecture

### One causal spine
Every significant operation carries:
- `trace_id`;
- `project_id`;
- `increment_id`;
- `work_order_id` where applicable;
- `execution_epoch`;
- `agent_id`/task_id;
- Git base/head SHA;
- provider/model route when relevant;
- event/effect IDs.

This allows one timeline from user command → planning → agent → provider/GitHub → evidence → review → checkpoint.

### OpenTelemetry boundary
Instrument API/workers/adapters using OpenTelemetry-compatible traces, metrics and logs. Backend/exporter remains replaceable; local V1 may retain a bounded internal projection instead of deploying a large observability cluster.

### Telemetry classes
- AUDIT: durable governance/security decisions;
- WORKFLOW: state transitions/events;
- DIAGNOSTIC: bounded logs/traces;
- PERFORMANCE: latency/resource samples;
- COST: tokens/provider/cost attribution;
- UX: local interaction/performance metrics with privacy limits.

### Truthful telemetry
Never convert timeout/missing sample into zero. Use states such as `UNKNOWN`, `STALE`, `UNAVAILABLE`, `LAST_KNOWN` with timestamp/freshness.

## 3. Cockpit health model

### Health is multidimensional
Each subsystem exposes:
- availability;
- freshness;
- authority state;
- dependency health;
- queue/backlog;
- error rate;
- latency;
- resource pressure;
- cost pressure;
- current blockers.

A single green dot cannot hide stale or degraded state.

### Dependency topology
Cockpit can render:
```text
Hive Plan
├─ PostgreSQL
├─ GitHub
├─ Model providers
├─ HIVE
├─ UADS
├─ UGAS
└─ local artifact store
```
with causal degradation propagation rather than generic `offline` status.

## 4. Resilience patterns

### Dependency isolation
Each remote/local adapter gets:
- timeout;
- bounded retry with jitter;
- circuit breaker;
- concurrency limit;
- health score;
- stale-data behavior;
- fallback/block policy.

### Retry taxonomy
Never retry blindly.
- TRANSIENT_NETWORK → bounded retry;
- RATE_LIMIT → Retry-After/backoff;
- AUTH/PERMISSION → block + operator action;
- VALIDATION → no retry until input changes;
- STALE_CONTEXT → cancel/recompile;
- CONFLICT → reconcile/rebase/replan;
- PROVIDER_CAPABILITY → reroute only if QualityFloor-compatible;
- DATA_INTEGRITY → fail closed and preserve evidence.

### Bulkheads
Separate concurrency pools for:
- interactive API/chat;
- GitHub observation;
- model calls;
- indexing/RAG;
- review;
- media/UGAS work;
- maintenance/backup.

Heavy indexing or media workloads cannot starve the UI/control plane.

### Resource arbitration
`ResourcePeacekeeper` receives CPU/RAM/GPU/load signals and can:
- lower cockpit graphics tier;
- reduce noncritical polling;
- delay background indexing;
- reduce worker concurrency;
- reserve interactive capacity;
- coordinate with UGAS/HIVE workloads.

It cannot silently reduce required review/security assurance.

## 5. Failure intelligence

### Incident Capsule
Any meaningful failure creates a structured capsule:
- failure class;
- first observed time;
- causal trace IDs;
- affected project/increment;
- source/adapter;
- relevant logs/evidence refs;
- last known good state;
- retry history;
- suspected root causes;
- recovery action;
- outcome;
- regression/prevention candidates.

Verified incidents feed FailureShield/HIVE defect memory and may produce SkillForge Failure Vaccine candidates.

### Loop detector
Repeated equivalent failure signatures trigger escalation instead of infinite retry/correction loops.

## 6. Data integrity and recovery

### Fail-closed cases
- artifact digest mismatch;
- review receipt does not match current SHA/context/evidence;
- checkpoint/source fingerprint conflict;
- migration version ambiguity;
- cross-system adapter contract major-version mismatch;
- secret/decryption integrity error.

### Restore hierarchy
1. application state restore;
2. PostgreSQL + artifact epoch validation;
3. rebuild derived indexes/cache;
4. reconcile GitHub external truth;
5. reconnect HIVE/UADS/UGAS adapters;
6. replay/revalidate active workflow state;
7. mark system READY only after RestoreProof passes.

## 7. SLO candidates for V1
SLOs are local operational targets, not public-cloud promises.

Candidate classes:
- interactive cockpit command latency;
- event detection latency;
- auto-review start latency after evidence readiness;
- review completion time by risk tier;
- stale-review false-approval target: zero;
- durable workflow recovery after process restart;
- verified backup/restore success;
- cache/RAG freshness correctness;
- escaped critical defect rate.

Numeric thresholds come from implementation benchmarks/evals.

## 8. Security / resilience drills
Before V1 release candidate, run controlled drills for:
- PostgreSQL restart during worker job;
- worker killed after external side effect;
- GitHub outage/rate-limit;
- model provider outage;
- stale PR head during review;
- corrupted artifact;
- Redis/cache loss;
- HIVE unavailable;
- UADS unavailable;
- UGAS busy/GPU pressure;
- backup + full restore;
- secret accidentally included in proposed public commit;
- malicious instructions inside fetched README/issue/web content.

## 9. Technology adoption rule
Do not add Prometheus, Grafana, Loki, Tempo, Kafka, Temporal, Vault or similar infrastructure merely because they are standard in larger deployments. Local V1 uses interfaces/contracts compatible with future adoption and adds infrastructure only when measured need exceeds operational cost.

## Freeze recommendation
Freeze trust-zone model, causal telemetry IDs, OpenTelemetry-compatible abstraction, truthful telemetry states, dependency adapters/circuit breakers, retry taxonomy, bulkheads, ResourcePeacekeeper, Incident Capsule, loop detection, RestoreProof and release fault drills. Keep exact telemetry backend, numeric SLOs, secret provider and infrastructure products benchmark-driven.
