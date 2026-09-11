# Review Technology Live Notes

Status: LIVING / NON-CANONICAL CONFIGURATION INPUT

Current research notes that inform implementation benchmarks but do not freeze vendor choices:

- GitHub CodeQL treats code as queryable data and supports vulnerability/error detection plus data-flow/path analysis for supported languages.
- GitHub code scanning can ingest third-party SARIF results; SARIF 2.1-compatible normalization is therefore a useful tool-neutral evidence surface.
- Semgrep offers broad pattern/rule scanning; advanced interfile/cross-function analysis should be evaluated separately for cost, language coverage and unique finding yield.
- Diff-filtering/reporting patterns such as reviewdog can reduce static-analysis noise by surfacing findings relevant to the patch, but Hive Plan retains its own ReviewScope/FindingGate authority.

These capabilities, license/availability constraints and versions must be refreshed before implementation/tool adoption.