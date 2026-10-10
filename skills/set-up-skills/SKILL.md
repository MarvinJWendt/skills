---
name: set-up-skills
description: Wire a repository's skills so `.agents/skills/` is the single source of truth and every agent reads it through a symlink. Use when a repo has no skill setup yet, when skills sit in `.claude/skills/` as real files, or when a second agent should read the same skills.
---

# set-up-skills

One skill store per repo, at `.agents/skills/`. Each agent's own skill directory is a symlink to it, so a skill is written once and no copy can drift.

Claude is the default and usually the only agent to wire. Add another one (`.codex/skills`, `.gemini/skills`, `.opencode/skills`) only when the user names it, using the same symlink.

## Target layout

```
.agents/skills/<skill-name>/SKILL.md    real files
.claude/skills -> ../.agents/skills     symlink
```

The symlink is relative, so it survives every clone and every machine. Git stores it as a symlink, so the wiring travels with the repo.

## Steps

1. See what exists: `ls -la .agents/skills .claude/skills .codex/skills 2>&1`. A directory that is already a symlink to `../.agents/skills` is done, leave it.
2. Create `.agents/skills/` if it is missing.
3. Move every real skill directory into it, one agent directory at a time, with `git mv` when the files are tracked and `mv` otherwise. Two agents holding a skill of the same name: compare both, ask the user which one wins, and move only that.
4. Replace each agent's now-empty skill directory with the symlink: `rmdir .claude/skills && ln -s ../.agents/skills .claude/skills`. `rmdir` refuses when something is left over, which is the signal that step 3 missed a file.
5. Verify through the symlink, not around it: `ls .claude/skills/` lists every skill that step 3 moved.
6. Check `.gitignore` for a rule covering the agent directory. When one exists, add an exception for the symlink, otherwise the wiring is missing in every fresh clone. Report it either way.

Finish by naming the skills that moved and every agent directory that now points at the store.

## Writing skills into the store

`create-skill` owns how a skill is written. Come back to it once the layout is in place.
