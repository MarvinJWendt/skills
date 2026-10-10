# AGENTS.md

This repository publishes agent skills in the [Agent Skills](https://agentskills.io/specification) format, installable with the `skills` CLI: `npx skills add marvinjwendt/skills`.

- `skills/<name>/SKILL.md` holds one skill per directory, and the directory name equals the frontmatter `name`. The CLI discovers skills in `skills/`, `.agents/skills/` and `.claude/skills/`, so this repo keeps nothing of its own in the latter two: whatever sits there is offered to everyone who installs from it.
- A publishing tool writes `skills/` and the table between the `forked-skills` markers in `README.md` from a private source, and overwrites edits made here on its next run. Change a skill at its source.
- A forked skill keeps its upstream `LICENSE` inside its own directory.
- Published content carries no secrets and no personal information.
