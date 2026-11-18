---
name: full
description: Implement a task completely and correctly without check-ins, to the repo's quality bar and the language's best practice, then push.
disable-model-invocation: true
metadata:
  requires: push
---

# Full

The user wants the task done in full: the implementation a senior maintainer of this repo would merge, not the shortest path to something that runs. Work autonomously from start to push. Invoking this skill is also the user's request for the push at the end.

## Deciding

Every open question is yours. Before you decide one, find out how it is solved properly, in this order: the repo's own conventions and the neighboring code, the documented practice of the language and libraries involved, then the web. Dig as deep as the decision weighs: a name needs a glance, a data model or a public interface deserves real research.

Take the option you judge correct, even when it is more work than the alternative. Note each decision that shaped the result, with its reason, for the report.

A few decisions belong to the user alone: breaking a public API, spending money, deleting data you did not create, touching production. Leave that part undone, finish everything around it, and report it as a blocker with your recommendation.

## The bar

The work is done when all of these hold:

- Every part of the task is implemented for real, including the edge cases, the error paths, and the callers, docs and config the change reaches.
- Tests cover the behavior that changed, where the repo has tests.
- The repo's own checks pass: its test, lint, typecheck and build tasks.
- The full diff has been reviewed as a stranger would review it, with the `code-review` skill where it is available, and every confirmed finding is fixed.

## Push

When the bar holds, run whatever finish sequence the repo's agent instructions define (an apply, a generated file to refresh), then run the `push` skill. A rejecting hook is part of the task: fix its cause. When the push triggers CI, wait for the checks and fix what fails. Done means green.

## Report

Close with what changed, how you verified it, the decisions with their reasons, and any blockers.
