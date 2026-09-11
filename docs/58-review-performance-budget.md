# Review Performance Budget

Status: FROZEN — HP-PLAN-006

Review performance is budgeted by stage rather than one global timeout.

Budget dimensions:
- Git/evidence collection latency;
- deterministic analysis latency;
- specialist semantic latency;
- final synthesis/audit latency;
- total completion-to-verdict latency;
- token/cost budget;
- CPU/RAM budget for local analyzers.

Fast-path reviews may skip irrelevant specialists/tools, but never required proof. ELEVATED/HIGH_ASSURANCE paths may exceed fast-path budgets to preserve quality.

Any stage exceeding its budget emits telemetry and optimization candidate; it does not silently truncate review scope.