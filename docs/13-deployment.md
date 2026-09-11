# Deployment

## V1 target
Local single-user deployment via Docker Compose.

## Deployment principles
- One-command/one-script bootstrap after documented prerequisites.
- Persistent volumes for database/vector state and local application state.
- Secrets injected locally and excluded from images/repos.
- Health checks for critical containers.
- Clear dependency startup order without relying on fragile sleeps.
- Versioned migrations.
- Backup and restore procedure before destructive migrations.
- Reproducible builds with pinned dependencies/lockfiles.

## Initial topology
Prefer a small number of deployable containers even if the code has strong internal module boundaries. Avoid premature microservice sprawl.

Expected initial components:
- web/app
- PostgreSQL (+ vector extension if benchmark-selected)
- optional Redis only if benchmarks justify it
- optional embedded/local retrieval service if not provided by Hive V1

Hive V1/UADS-Hades/UGAS integrations remain external adapters unless a later approved architecture decision changes this.

## Clean-machine validation
Before V1 release, bootstrap must be validated from a clean supported Windows/Docker environment, including secrets configuration, GitHub connection, provider connectivity, persistence, restart, backup, and restore.
