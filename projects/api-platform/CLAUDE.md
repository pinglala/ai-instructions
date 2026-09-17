# Project: api-platform

## What this project is
A Turborepo monorepo, scaffolded at `~/work/sandbox/backend`, for hosting an HTTP API
and cloud functions from a single codebase. It lives under `sandbox/backend` (rather
than directly in `sandbox`) to leave room for sibling top-level dirs later (e.g. a
`frontend`).

## Stack
- Node.js, version pinned via Volta (see `volta` field in root `package.json`)
- pnpm workspaces (`packageManager` field pins the exact pnpm version)
- Turborepo for task orchestration (`turbo.json`)
- Express.js for the HTTP API (`apps/api`)
- Plain TypeScript function handlers for cloud functions (`apps/functions`), kept
  provider-agnostic (no AWS/GCP SDK wired in yet)
- ESLint (flat config, `typescript-eslint`) at the repo root, shared by all apps
- GitHub Actions for CI (`.github/workflows/ci.yml`): install → lint → build → test on
  push to `main` and on pull requests

## Conventions
- New apps go under `apps/<name>/`, each with its own `package.json`, `tsconfig.json`,
  and `src/`. Add the app to `pnpm-workspace.yaml` implicitly via the `apps/*` glob —
  no extra step needed.
- Every app exposes `build`, `dev` (if long-running), `lint`, and `test` scripts so
  `turbo run <task>` at the root fans out correctly.
- Keep CI simple: one job, one Node/pnpm version, no matrix builds, no deploy step yet.
  Add deploy steps only when there's a real target to deploy to.

## Standing instructions for Claude
- Don't add a cloud provider SDK (AWS/GCP/Azure) to `apps/functions` unless asked —
  it's intentionally provider-agnostic for now.
- Don't introduce a shared `packages/*` workspace until there's actual code to share
  between `apps/api` and `apps/functions`.
- Keep the CI workflow to build/lint/test only unless asked to add deployment.

## Gotchas
- This Volta version (2.0.2) can't pin pnpm directly ("Only node and yarn can be
  pinned") — pnpm's version is pinned via the `packageManager` field instead, and
  `pnpm/action-setup@v4` picks it up automatically in CI.
- ESLint flat config resolves per linted file by walking up from that file's
  directory, so one root-level `eslint.config.js` covers every app; no per-app
  config needed.
