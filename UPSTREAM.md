# Upstream baseline

Both roles were rebased on hifis.toolkit 7.0.1 (2026-10-28).
Source: https://github.com/hifis-net/ansible-collection-toolkit/releases/tag/v7.0.1

The gitlab_runner role matches upstream. The gitlab role retains these local extensions:

- Registry listen address, token realm and nginx enable switch.
- Registry cleanup policy script and cron (tasks/registry-cleanup.yml).
- Cleanup of legacy APT repository declarations.
- Read-only upgrade preflight: pinned version, no downgrade, configured upgrade stops,
  schema migrations, all unfinished batched migrations, PostgreSQL 17 gate for GitLab 19.
- Configurable post-deployment migration skipping; set
  gitlab_skip_post_deployment_migrations: false for standalone upgrades.

The migration checks use local gitlab-psql and target a primary Linux-package
installation with local PostgreSQL. They stop on pending schema migrations instead
of silently running database repairs. Read-only checks also run in check mode;
upstream dependency tasks can still update package indexes or create temporary files.

Set gitlab_upgrade_stops to verified patch versions for your upgrade route.
Application versions are pinned in inventory, not in role defaults.
Collection version 1.1.0 is local and has not been published.
