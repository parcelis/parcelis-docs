---
title: Contributor Setup
slug: /contributor-getting-started
---
Parcelis is a pnpm/Turbo monorepo. This guide gets the web app, API, and local services running on your machine.

Existing PostgreSQL 16 development databases must follow [Upgrade PostgreSQL 16 to 18](../Deployment/upgrade-postgresql.md) before running `pnpm dev` or refreshing services. New installations use PostgreSQL 18.

## Requirements

| Tool           | Required version       |
| -------------- | ---------------------- |
| Node.js        | 24.19.0                |
| pnpm           | 12                     |
| Docker Desktop | Current stable release |

Confirm your local runtime before continuing:

```bash
node --version
pnpm --version
```

## First-time setup

```bash
pnpm install
cp .env.example .env
docker compose -f docker-compose-dev.yml up -d
pnpm db:generate
pnpm db:migrate
```

Choose one setup path on a new local database.

- **Command line** — Set `SEED_ADMIN_EMAIL` to a new address. Set `SEED_ORGANIZATION_NAME` and a unique
  `SEED_ADMIN_PASSWORD` of at least 12 characters in `.env`. Run `pnpm db:seed` for a bootstrap-only
  workspace or `pnpm db:seed:demo` to include sample records. Start `pnpm dev` and sign in with the
  seeded administrator.
- **Registration UI** — Skip the seed commands and start `pnpm dev`. Select **Fresh install** for a
  bootstrap-only workspace or **Demo install** for starter records, then create your account.

Use an email other than `admin@parcelis.dev` for a new account. A historical migration already
creates that account, and seed reruns leave existing passwords in place.

`pnpm dev` runs the web app, API, and React Email previews with hot reload. Docker provides nginx,
PostgreSQL, pgAdmin, MinIO, and the one-time MinIO initialization job.

Documentation is maintained and deployed separately in [parcelis/parcelis-docs](https://github.com/parcelis/parcelis-docs). `pnpm dev` does not start a documentation server. Legacy application `/docs` links redirect to the hosted site.

## Local URLs

Use nginx as the usual entry point:

| Service              | URL                           |
| -------------------- | ----------------------------- |
| Web app              | `http://localhost`            |
| Documentation        | `https://docs.parcelis.dev/`      |
| API                  | `http://localhost/api/v1`     |
| React Email previews | `http://templates.localhost/` |

The apps and services are also available directly:

| Service              | Address                                                                 |
| -------------------- | ----------------------------------------------------------------------- |
| Web app              | `http://localhost:30000`                                                |
| API                  | `http://localhost:40010`                                                |
| React Email previews | `http://localhost:30001` by default; use the port printed by `pnpm dev` |
| PostgreSQL           | `localhost:54320`                                                       |
| pgAdmin              | `http://localhost:8000`                                                 |
| MinIO API            | `http://localhost:9001`                                                 |
| MinIO console        | `http://localhost:9010`                                                 |

pgAdmin uses `admin@parcelis.dev` / `parcelis`. The local Parcelis database is preconfigured; its password is `parcelis`.

## Database workflow

Prisma commands run through `pnpm db:*` load the root `.env`. If `DATABASE_URL` is unset, the API uses `postgresql://parcelis:parcelis@localhost:54320/parcelis?schema=public` only when `ENVIRONMENT` is `development` or `test` (falling back to `NODE_ENV` when `ENVIRONMENT` is unset). Other environments require an explicit PostgreSQL URL; empty or invalid values fail startup.

After pulling schema changes, run:

```bash
pnpm db:migrate
pnpm db:generate
```

Run `pnpm db:seed` for initial bootstrap or when an update explicitly requires a bootstrap
seed-data change. When targeting a real environment, export its `DATABASE_URL` and ensure
`SEED_DEMO_DATA` is unset or `false` in the shell and `.env`. The Prisma wrapper falls back to
local PostgreSQL when no URL is configured. Reruns can update the bootstrap organization and
administrator membership.

Use `pnpm db:seed:demo` only on local or dedicated demo databases because it can overwrite or
delete existing sample records. Setting `SEED_DEMO_DATA=true` also enables demo seeding.

To use `admin@parcelis.dev` on your local database, set `ENVIRONMENT=development` and
`SEED_ADMIN_EMAIL=admin@parcelis.dev` in `.env`, then run `pnpm db:seed`. The seed falls back to
`NODE_ENV` when `ENVIRONMENT` is unset.

## Useful commands

```bash
pnpm typecheck
pnpm lint
pnpm dev:services:refresh
```

`pnpm dev:services:refresh` recreates nginx, PostgreSQL, and MinIO while preserving their volumes, then reruns MinIO initialization. Stop an existing app watcher with `Ctrl+C` before starting another `pnpm dev` process.

For the complete contributor workflow, including commit conventions and production-style deployment, see the [contributing guide](https://github.com/parcelis/parcelis/blob/main/CONTRIBUTING.md).
