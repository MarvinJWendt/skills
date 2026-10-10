---
name: set-up-agents
description: Set up a repository's whole agent configuration in one go, instructions and skills. Use when asked to set up agents in a repo, to bootstrap a fresh project for agent work, or when it is unclear which parts of the setup a repo is missing.
---

# set-up-agents

Two skills do the work. Run both, in this order:

1. `set-up-agents-md` for the instructions: `AGENTS.md` as the source of truth, each agent's own file symlinked to it.
2. `set-up-skills` for the skills: `.agents/skills/` as the source of truth, each agent's own directory symlinked to it.

Both migrate whatever already exists, so a half-configured repo is fine. Both default to Claude alone. When the user named other agents, pass that on to each.
