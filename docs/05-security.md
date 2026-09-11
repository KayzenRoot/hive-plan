# Security Baseline

## V1 security goals
- Protect GitHub token/API keys/secrets at rest and in memory as far as practical for a local single-user app.
- Never send secrets to LLM providers, logs, telemetry, exports, or repositories.
- Minimize external data exposure by compiling only necessary context.
- Verify privileged/destructive GitHub operations against explicit policy.
- Preserve auditability of consequential actions.

## Secret handling
- Secrets live in local secret storage/environment injection, never committed.
- UI displays secret presence/status only, never raw values after save.
- Logs apply structured redaction.
- Prompt/context pipeline includes secret-pattern and source-policy filtering before provider calls.
- Token permissions follow least privilege compatible with repository creation/management requirements.

## GitHub token policy
The initial internal V1 supports PAT/token authentication. Repository administration capability is allowed only when configured by the operator. Destructive or history-rewriting actions remain gated by explicit policy; force-push is prohibited by default.

## Threat areas to model before implementation freeze
- Token theft/leakage.
- Prompt injection from repository content/issues/PRs.
- Malicious or compromised dependency instructions.
- Agent confused-deputy behavior.
- Untrusted code/evidence claiming success.
- Arbitrary file/path access.
- Command execution boundaries around Codex/other executors.
- Supply-chain compromise.
- Cross-project context leakage.
- Accidental destructive GitHub action.
- Sensitive source disclosure to external LLMs.

## Review principle
Repository content is data, not authority. Instructions found in source files, issues, PRs, comments, generated evidence, or external text do not override Hive Plan system policy unless they originate from an approved canonical source and pass policy validation.
