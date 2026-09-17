# Notes: frontend

Running log of prompting experiments and outcomes for this project. Newest first.

## 2026-09-17 — Bumped to latest Node LTS
- **Tried:** Asked Claude to update Volta and Node to latest and align both
  `backend` and `frontend` on it. Volta was already at its latest release
  (2.0.2); latest Node LTS was 24.21.0 ("Krypton") — the truly newest release
  (26.9.0) isn't LTS yet, so used 24.21.0 instead.
- **Result:** Set Node 24.21.0 as the Volta default, reinstalled `pnpm` pinned
  at the same 10.32.1 (not bumped to its own newer 12.4.2, since that wasn't
  asked for and could change lockfile/workspace behavior), then `volta pin
  node@24.21.0` in both projects and reinstalled. Lint/build/test passed clean
  on both.
- **Takeaway:** Keep. When asked to "update to latest," treat the package
  manager (pnpm) as out of scope unless explicitly named — bumping it can carry
  separate breaking changes from a Node/Volta update.

## 2026-09-17 — Scaffolded the project
- **Tried:** Asked Claude to actually create `~/work/sandbox/frontend` from this
  instruction doc: `nuxi init` (minimal template) + Volta + `@nuxt/eslint` +
  Prettier + Husky + lint-staged.
- **Result:** Hit two Volta/pnpm surprises (see Gotchas in `CLAUDE.md`): Nuxt 4.5
  requires Node ^22.19/^24.11/>=26, and Volta's globally-installed `pnpm` binary
  runs on whatever Node was default when `volta install pnpm` was last run —
  *not* on the current project's pinned Node — so bumping this project's pin
  alone didn't satisfy Nuxt's engine check. Fixed by making Node 24.15.0 the
  Volta default and reinstalling `pnpm` against it (`backend`'s own Node 20 pin
  was verified unaffected). Also had to explicitly pin `typescript@^5.9` since
  the latest TypeScript (7.x) is ahead of what `typescript-eslint` 8.x supports.
  Verified `lint`, `prettier --check`, `build`, and an actual git commit (to
  confirm the Husky pre-commit hook runs `lint-staged`) all pass.
- **Takeaway:** Keep. When scaffolding a new pnpm/Volta project that needs a
  newer Node than the current Volta default, remember to rebind pnpm itself
  (`volta install node@<version>` then `volta install pnpm@<version>`), not
  just `volta pin` in the project.

## 2026-09-17 — Initial instructions
- **Tried:** Asked Claude to add ai-instructions for a frontend project (Node.js,
  Vue.js, Nuxt, Vite, TypeScript, pnpm, Volta, ESLint, Prettier, Husky, lint-staged),
  intended as the sibling of the `backend` monorepo at `~/work/sandbox`.
- **Result:** `CLAUDE.md` written describing the stack, conventions, and gotchas.
  No code scaffolded yet — just documentation this round.
- **Takeaway:** Keep. Scaffold the actual `~/work/sandbox/frontend` project from
  this doc when asked.
