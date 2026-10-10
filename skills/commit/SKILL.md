---
name: commit
description: Commit the current changes with a message written in the repo's own style. Run it on the user's explicit request or /commit, never because a task just finished.
---

Goal: one commit whose subject would pass unnoticed in the middle of `git log --oneline`. Aim for a single sentence and stop there.

## 1. See what changed

```sh
git status --short
git diff --stat
```

Stage everything with `git add -A`, then get at the intent behind the change:

- **Cold start**, no context on these changes: read `git diff` and work out why the change was made, not only which files moved.
- **Warm**, you made the changes this session: use what you already know. Read the diff only for files you did not touch yourself, the stat above shows which those are.

One commit. Split only when the user asks for it.

## 2. Learn the convention

```sh
git log --no-merges -n 10 --pretty=format:'%s'
```

Read the sample for prefix style (`feat:`, `fix(scope):`, or none at all), tense, capitalization, trailing period, typical length, and language. Match what is there instead of correcting it. Reuse an existing scope rather than inventing one.

**Ticket IDs.** If the sample carries them, this commit carries one too, in the exact position and bracket style the sample uses (`ABC-123: subject`, `subject (ABC-123)`, a trailer). Take it from what the user said, otherwise from the branch name (`git rev-parse --abbrev-ref HEAD`). If neither has one, ask the user. An invented ID, or one borrowed from an older commit, is worse than the question.

## 3. Write it and commit

Write like an engineer telling a colleague what changed: plain technical English, specific to this change. "fix null check in session refresh" beats "fix bug". Someone scanning the log in six months should know what happened without opening the diff.

- Imperative present tense by default: "add retry to the upload path", not "added", "adds", or "adding". Where the log from step 2 disagrees, the log wins.
- Single sentence, subject only, around 70 characters. Add a body only when the subject alone leaves a reader unable to tell what happened, and keep it to a couple of lines.
- Punctuate with a comma or a second sentence, never an em dash.
- Describe the change itself, not the act of committing, and not the list of files.
- No trailers, no co-authors, no tool attribution.

```sh
git commit -m "<subject>"
```

If a hook rejects the commit, read its output and fix the actual cause yourself, then tell the user what you fixed and wait for their go-ahead before committing again. `--no-verify` stays off unless they ask for it.

Report the subject line and the short SHA. Pushing is the user's call, leave it to them.
