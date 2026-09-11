# Review Scope Schema Notes

Status: PROPOSED CONTRACT INPUT — HP-PLAN-006

A future machine-readable ReviewScope contract should carry:
- project_id / increment_id / work_order_id;
- repository / PR / base_sha / head_sha;
- context_root / evidence prerequisites;
- changed files and symbols;
- MUST_REVIEW / IMPACT_REVIEW / PROOF_ONLY / WATCH nodes;
- impact-edge reason/provenance/confidence;
- acceptance criteria and proof channels;
- required specialist roles;
- deterministic checks required;
- excluded/unrelated areas;
- risk/assurance class;
- scope fingerprint.

The contract should be canonicalized/fingerprinted under the existing artifact-contract rules. Review agent prompts are rendered views of this structured scope, not independent truth.