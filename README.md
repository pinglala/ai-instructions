# AI Instructions

A version-controlled home for the instructions, prompts, and Claude Code skills I use across
development work. The point of tracking this in git is twofold:

1. **History** — every tweak to an instruction file or prompt is a commit, so I can see what
   changed, when, and why (and revert if a "better" phrasing turns out worse).
2. **Practice** — this doubles as a training ground for writing good instructions/skills. Drafts
   live in `prompts/drafts/` until they're proven, then graduate into `prompts/templates/`,
   `projects/*/CLAUDE.md`, or `skills/*/SKILL.md`.

## Layout

```
ai-instructions/
├── projects/           # per-project instruction sets (CLAUDE.md + notes per project)
│   └── _template/
├── skills/              # Claude Code skills being drafted/iterated on
│   └── _template/
├── prompts/
│   ├── templates/       # reusable, "graduated" prompt snippets
│   └── drafts/          # work-in-progress prompts, experiments, failed attempts kept for learning
└── CHANGELOG.md         # human-readable summary of notable changes (commit log has the detail)
```

## Workflow

- Start new instructions/prompts in `prompts/drafts/`. Commit early and often — small commits
  make the diff history actually useful for reviewing how a prompt evolved.
- When a project needs its own persistent instructions, copy `projects/_template/` to
  `projects/<name>/` and fill in `CLAUDE.md`.
- When drafting a reusable Claude Code skill, copy `skills/_template/` to `skills/<name>/` and
  iterate on `SKILL.md`.
- Note anything worth remembering (a phrasing that worked well, a pattern that backfired) in
  `CHANGELOG.md` so lessons aren't only buried in commit messages.
