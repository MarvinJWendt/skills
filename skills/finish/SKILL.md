---
name: finish
description: "Carry the work to the end while the user is AFK: decide every open question yourself, verify, and leave a report with a decision log. Use on /finish, when the user says they are away or asleep and expects the work done on return, and when another skill hands off unattended work."
---

# Finish

The user is AFK and expects the work done when they come back. Nobody answers questions until then, so every decision is yours, and the user trusts you to make the right ones. The decision log in the final report takes the place of every question you would have asked.

## Deciding

When you are unsure, investigate instead of guessing. Use every source you can reach: the code and its history, docs, the web, the user's memory, every connected tool. Dig as deep as the decision weighs. A naming choice needs a glance; a schema change deserves the hour.

Then take the option you judge best, even when it is the harder one to reverse. Record it in the decision log: what you chose, why, and how to undo it.

A standing rule of the user's to ask before acting is suspended in this mode. Act, and log the decision instead.

## Limits

The user's trust covers these too, with care:

- **Production deploys** are part of the job. After each one, verify that production works: health checks, logs, a browser check where the repo calls for one. When it broke, roll back first, then fix.
- **Money**: free first. A few cents in total are fine, such as test prompts against a small model. Anything beyond pocket change, or any recurring cost (a new paid resource, a bigger instance, a subscription), becomes a blocker.
- **Messages to people** (email, chat, comments on someone else's issue): only when sending them is part of the task.
- **Force pushes, history rewrites, breaking a public API, deleting data you did not create**: only when the task has no other way through. Each one goes into the decision log.

## Git

Follow the repo's agent instructions on committing and pushing. Where they say nothing, commit the finished work locally with the `commit` skill. Push when the user queued a push in the same prompt, for example with `/push`.

When a push or a PR triggers CI, wait for the checks and fix what fails. Done means green.

## Scope

The task is the goal. Fix small bugs you hit along the way and list them in the report. Leave big ones alone and report them: anything that needs a large change or touches production data.

When the prompt holds several tasks or queued commands, finish all of them in the order given. A shutdown always runs last.

## Getting stuck

After a few failed attempts, step back and ask whether the approach is wrong. Switch when it is; keep going when it holds. A part you cannot finish becomes a blocker, written up with what you tried, and the rest of the work continues around it.

## The report

Before writing it, run the verification the repo calls for and wait for every background job you started (subagents, workflows, background commands) to complete.

Run the `unslop` skill over the report. It is the first thing the user reads on return:

1. **Done**: what got finished and how you verified it.
2. **Decisions**: a table of decision, reason, and how to reverse it. Every spend and every risky operation from the limits above is a row.
3. **Blockers**: what is unfinished, why, and what it needs from the user.
4. **Fixed on the way** and **noticed, not touched**.
5. **Look at first**: the one or two things the user should check before anything else.

When the harness offers a push notification tool, send a one-line summary through it at the end.
