<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/banner-dark.svg">
  <img src="assets/banner-light.svg" alt="skills: SKILL.md files for coding agents" width="100%">
</picture>

<p>
  <a href="https://agentskills.io"><img src="https://img.shields.io/badge/format-Agent%20Skills-d97757?style=flat-square" alt="Agent Skills format"></a>
  <a href="skills"><img src="https://img.shields.io/github/directory-file-count/MarvinJWendt/skills/skills?type=dir&label=skills&style=flat-square&color=e8a87c" alt="Skill count"></a>
  <a href="https://github.com/MarvinJWendt/skills/commits/main"><img src="https://img.shields.io/github/last-commit/MarvinJWendt/skills?style=flat-square&label=updated&color=59636e" alt="Last commit"></a>
  <a href="LICENSE"><img src="https://img.shields.io/github/license/MarvinJWendt/skills?style=flat-square&color=59636e" alt="License"></a>
</p>

<p>
  <b>Claude Code</b> &nbsp;·&nbsp; <b>Codex</b> &nbsp;·&nbsp; <b>Cursor</b> &nbsp;·&nbsp; <b>Gemini CLI</b> &nbsp;·&nbsp; <b>OpenCode</b> &nbsp;·&nbsp; any agent that reads <code>SKILL.md</code>
</p>

<p>
  <a href="#install">Install</a> &nbsp;|&nbsp;
  <a href="#skills">Skills</a> &nbsp;|&nbsp;
  <a href="#license">License</a>
</p>

</div>

<br>

The agent skills I use every day. They commit, pull and push, chase down failures, edit prose and code comments, and set up repositories for agents. Each one is a single `SKILL.md` in the [Agent Skills](https://agentskills.io) format, and most take a minute to read, so read before you install.

## Install

Pick from the list:

```sh
npx skills add marvinjwendt/skills
```

Or install one skill for every project:

```sh
npx skills add marvinjwendt/skills -s unslop -g
```

<details>
<summary>More ways to install</summary>
<br>

| Command | What it does |
| --- | --- |
| `npx skills add marvinjwendt/skills --list` | Lists the skills, installs nothing |
| `npx skills add marvinjwendt/skills -s commit push` | Installs a few into the current project |
| `npx skills add marvinjwendt/skills -s '*' -g -y` | Installs all of them globally, no prompts |
| `npx skills use marvinjwendt/skills@unslop` | Prints a prompt that uses one skill once, without installing it |

</details>

## Skills

Click a name to read the whole file.

<!-- skills:start -->
<!-- skills:end -->

<!-- forked-skills:start -->
<!-- forked-skills:end -->

## License

[MIT](LICENSE), except for forked skills, which keep the license in their own directory.
