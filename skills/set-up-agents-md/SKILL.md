---
name: set-up-agents-md
description: Make `AGENTS.md` the single source of truth for a repository's agent instructions and symlink every agent's own instruction file to it. Use when a repo has no agent instructions yet, when they live in `CLAUDE.md` as a real file, or when several instruction files have drifted apart.
---

# set-up-agents-md

One instruction file per repo, `AGENTS.md` at the root. Each agent's own file is a symlink to it, so an instruction is written once and every agent reads the same text.

Claude is the default and usually the only agent to wire. Add another one (`GEMINI.md`) only when the user names it, using the same symlink. Codex and opencode read `AGENTS.md` directly and need nothing.

## Target layout

```
AGENTS.md                real file
CLAUDE.md -> AGENTS.md   symlink
```

Both sit in the same directory, so the symlink is a bare filename and works in every clone.

## Steps

1. Find what exists: `ls -la AGENTS.md CLAUDE.md GEMINI.md 2>&1`. A file that is already a symlink to `AGENTS.md` is done, leave it.
2. Bring the content together into `AGENTS.md`, by case:

| Found | Action |
| --- | --- |
| `AGENTS.md` only | Nothing to move. |
| `CLAUDE.md` only | `git mv CLAUDE.md AGENTS.md`, or `mv` when untracked. |
| Both | Read both. Merge every instruction from the other files into `AGENTS.md`, dropping only what it already says. Where the two contradict each other, ask the user which one holds. |
| Neither | Write one, see below. |

3. Replace each agent's file with the symlink: `rm CLAUDE.md && ln -s AGENTS.md CLAUDE.md`. Only after its content lives in `AGENTS.md`.
4. Verify the merge survived: `cat CLAUDE.md` reads back the instructions, and nothing that was in the old files is missing.

Repos carrying nested instruction files (`packages/foo/CLAUDE.md`) get the same treatment per directory, each symlink pointing at the `AGENTS.md` beside it.

Finish by naming which files merged and which are now symlinks.

## Writing the file from scratch

Read the repo first, enough to say what a new agent needs to know: build and test commands, the layout, the conventions the code follows but does not state. `writing-for-agents` owns how to write it. Keep it to what nearly every task in this repo needs, and let focused topics become skills through `set-up-skills`.
