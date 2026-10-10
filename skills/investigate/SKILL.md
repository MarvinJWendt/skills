---
name: investigate
description: Find out why something failed or behaves the way it does, using read-only commands only, and report the cause back in chat.
disable-model-invocation: true
---

# Investigate

The user wants an explanation, not a fix. Find the cause and report it in chat. Editing files, applying a patch or fixing it on the way is a separate task they start themselves.

Every command you run only reads: `cat`, `grep`, `git log`, `git diff`, `journalctl`, `docker logs`, `kubectl get/describe/logs`, a `--dry-run`, a `--help`. Anything that writes, installs, restarts, deletes or touches remote state waits for the user to ask for it. If the investigation dead-ends without such a command, name the command and let him decide.

Dig until you have the actual cause. "The build failed" is the symptom, "the lockfile pins X 2.0 while the code calls the 1.x API" is the cause. Follow the chain backwards: the error, the code that raised it, the state that got it there, the change that created that state. A guess stays labelled as a guess.

## The report

Run the `unslop` skill over it. Short and concrete, with enough detail that the user can act on it without a follow-up question.

- Lead with the cause, one or two sentences.
- Then the chain that proves it, carrying its evidence: file paths with line numbers, log lines, commit SHAs, command output. Quote the parts that make the point.
- Name what stayed unclear and why.
- Close with what would fix it, a few lines. Whether you do it is the user's call.
