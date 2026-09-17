# Project: frontend

## What this project is
A Vue.js/Nuxt frontend, scaffolded at `~/work/sandbox/frontend` as the sibling of
the `backend` API/cloud-functions monorepo (see `projects/api-platform/CLAUDE.md`).

## Stack
- Node.js 24.21.0 (latest LTS as of 2026-09), version pinned via Volta (`volta`
  field in `package.json`) — same version as `backend`
- pnpm (`packageManager` field pins the exact version)
- Vue.js
- Nuxt (app framework, file-based routing, SSR/SSG)
- Vite (bundler/dev server, bundled with Nuxt — no separate config needed)
- TypeScript
- ESLint for code-quality rules
- Prettier for formatting — kept out of ESLint's job via `eslint-config-prettier` so
  the two never disagree on a rule
- Husky for git hooks
- lint-staged so hooks only touch staged files, not the whole repo

## Conventions
- Pre-commit hook (Husky) runs `lint-staged`, which runs `eslint --fix` and
  `prettier --write` on staged files only.
- ESLint owns correctness/quality rules; Prettier owns formatting. Don't add
  stylistic rules to the ESLint config that Prettier already handles.
- Use `<script setup lang="ts">` for Vue components; avoid the Options API in new
  code.
- Prefer Nuxt's built-in conventions (file-based routing in `pages/`, auto-imports)
  over manual wiring.

## Standing instructions for Claude
- Don't add Nuxt modules or plugins unless asked.
- Don't relax `lint-staged` to run across the whole repo — keep it scoped to staged
  files so commits stay fast.
- Don't hand-roll Vite config unless Nuxt's defaults genuinely can't do what's
  needed — Nuxt manages Vite under the hood.

## Gotchas
- Volta (as configured elsewhere in this environment) can't pin pnpm directly
  ("Only node and yarn can be pinned") — pin pnpm via the `packageManager` field
  instead; `pnpm/action-setup@v4` reads it automatically in CI if this project gets
  one.
- Husky v9+ dropped the old `husky install` postinstall script in favor of a
  `"prepare": "husky"` script plus a plain `.husky/<hook>` file committed to the
  repo — don't reach for the old v4-style setup.
- Nuxt 4.5 requires Node ^22.19 / ^24.11 / >=26.
- Volta's globally-installed `pnpm` binary always runs on whatever Node was the
  Volta *default* when `pnpm` was installed/reinstalled — it ignores a project's
  own `volta.node` pin. So when a project needs a newer Node than Volta's current
  default (as this one did), `volta pin node@<version>` in the project alone is
  not enough: also run `volta install node@<version>` (sets the new default) and
  then `volta install pnpm@<version>` (rebinds pnpm to it). Verify this hasn't
  silently changed behavior for other projects afterward.
- `typescript-eslint` 8.x caps its TypeScript peer dependency below 6.1.0; pnpm
  will happily install TypeScript 7.x anyway (a peer-dependency warning, not an
  error) — pin `typescript` to a `^5.x` version explicitly.
