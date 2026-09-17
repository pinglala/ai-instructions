# Notes: api-platform

Running log of prompting experiments and outcomes for this project. Newest first.

## 2026-09-17 — Bumped to Node 24.21.0
- **Tried:** Asked Claude to update Node/Volta to latest and align `backend` with
  `frontend` (which had already moved to Node 24 for Nuxt's sake).
- **Result:** Pinned to Node 24.21.0 (latest LTS), reinstalled, and reran
  `lint`/`build`/`test` — all passed unchanged.
- **Takeaway:** Keep. Both projects now share one Node line, so there's no
  cross-project drift to track.

## 2026-09-17 — Nested under backend/
- **Tried:** Asked Claude to add a `backend` directory inside `~/work/sandbox` and
  move all existing monorepo contents into it, so `sandbox` can hold sibling dirs
  (e.g. a future `frontend`) alongside `backend` later.
- **Result:** Everything (including `.git`, `node_modules`, `.turbo`) moved into
  `~/work/sandbox/backend`. Cleared the turbo cache and reran `pnpm build`/`lint`/
  `test` from the new path — all passed.
- **Takeaway:** Keep. Project root is now `~/work/sandbox/backend`, not
  `~/work/sandbox`.

## 2026-09-17 — Initial scaffold
- **Tried:** Asked Claude to scaffold a Turborepo monorepo (Node.js/Volta/pnpm,
  Express.js API + cloud functions, GitHub Actions CI) at `~/work/sandbox`, and to
  document the stack here in `ai-instructions`.
- **Result:** Scaffold created and verified locally: `pnpm install`, `pnpm lint`,
  `pnpm build`, and `pnpm test` all pass; the Express API responds on `/health`.
- **Takeaway:** Keep — this is the baseline stack for new API/cloud-function projects
  going forward.
