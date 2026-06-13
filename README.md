# Finviz Signal Refresh Scheduler

Public scheduler for the private `avobati/finviz-lead-indicator` application.

The repository contains no database credentials or private application source.
GitHub Actions checks out the private application at runtime using encrypted
repository secrets, runs its tests, refreshes Neon, verifies freshness, and
records a heartbeat commit.

Required GitHub Actions secrets:

- `PRIVATE_REPO_TOKEN`: read access to `avobati/finviz-lead-indicator`
- `DATABASE_URL`: Neon Postgres connection string

Schedules:

- Primary: 23:30 UTC, Monday-Friday
- Watchdog: 04:30 UTC, Tuesday-Saturday

The watchdog checks the production refresh-status endpoint and skips when the
primary run already produced current data.
