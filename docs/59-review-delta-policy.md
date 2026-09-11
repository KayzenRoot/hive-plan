# Delta Review Policy

Status: FROZEN — HP-PLAN-006

Correction reviews are delta-first:
- compare new head to prior reviewed head;
- re-run checks for changed and semantically impacted nodes;
- reuse immutable unaffected evidence/dispositions only when fingerprints remain valid;
- re-open any finding whose correction touched its assumptions/dependencies;
- preserve mandatory regression/security gates for the impact closure;
- invalidate prior Review Receipt once head changes.

Delta-first is a speed optimization, never permission to skip impacted regression coverage.