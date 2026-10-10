---
name: push
description: Push the current branch to its remote, committing first when the working tree is dirty. Run it on the user's explicit request or /push, never because a task just finished.
---

The user asking for the push is the approval. Do not ask for it again at any point below.

When this fires while a task is still in progress, the push queues behind it. Finish the task first, through whatever verification it calls for, then run the steps below. The push goes out with the finished work, never with a half-done tree.

1. `git status --short`. If anything is uncommitted, run the `commit` skill and let it stage and write the message.
2. Push: `git push`, or `git push -u origin HEAD` when the branch has no upstream yet.
3. If a pre-push hook rejects the push, read its output, fix the actual cause, run the `commit` skill again, and push again. `--no-verify` stays off unless the user asks for it.

When the remote rejects the push because it has moved ahead, report that and stop. Reconciling the histories, and anything involving a force push, is the user's call.

Report the branch, its remote, and the subjects of the commits that went out.
