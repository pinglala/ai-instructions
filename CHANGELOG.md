# Changelog

Notable lessons and changes go here, newest first. Keep entries short — the git log has the
full diff, this file is for the *why it mattered*.

## Unreleased

- Made the repo public and turned on branch protection for `main` (PR required,
  no direct pushes) so it could actually be enforced — GitHub's branch-protection
  API isn't available on free-tier private repos. Added `.github/CODEOWNERS`
  (`@pinglala`) and documented the rule in the README. Approvals aren't required
  to merge, since GitHub won't let the sole code owner approve their own PRs.
- Bumped both `backend` and `frontend` to Node 24.21.0 (latest LTS); Volta itself
  was already at its latest release (2.0.2), so nothing to do there. Left pnpm at
  10.32.1 rather than its own newer 12.4.2, since only Node/Volta were asked for.
- Scaffolded `~/work/sandbox/frontend` (Nuxt/Vue, TypeScript, ESLint, Prettier,
  Husky + lint-staged) per `projects/frontend/CLAUDE.md`. Had to make Node 24 the
  Volta default and rebind pnpm to it — Volta's global pnpm binary runs on
  whatever Node was default when it was installed, not the project's own pin.
- Added `projects/frontend/`: instructions for a Vue.js/Nuxt frontend (Node.js,
  Volta, pnpm, Vite, TypeScript, ESLint, Prettier, Husky, lint-staged), sibling of
  `backend` at `~/work/sandbox/frontend`.
- Added `projects/api-platform/`: instructions for a Turborepo monorepo (Node.js,
  Volta, pnpm, Express.js API + cloud functions, GitHub Actions CI), scaffolded at
  `~/work/sandbox/backend`.
- Repo created: structure for projects/skills/prompts.
