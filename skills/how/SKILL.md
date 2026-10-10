---
name: how
description: "Use for \"how does X work\", code walkthroughs before changing something, and placement / ownership / layering questions (\"where should this live\", \"which package owns this\", \"is this the right layer\"). Explains subsystem architecture, runtime flow, onboarding mental models."
disable-model-invocation: true
---

# How

Explore the codebase to answer "how does X work?" questions. Produce architectural explanations at the level of a senior engineer onboarding onto a subsystem, enough to build a working mental model, not so much that it reads like annotated source code.

## Step 1. Assess complexity

If the scope is ambiguous, state your interpretation and explore. The user can redirect.

- **Simple** (a single module, a small utility, a narrow question such as "how does function X work"): no explorers. One explainer explores and explains in a single pass. Go to Step 2b.
- **Complex** (a subsystem spanning multiple files or services, a cross-cutting feature, a full architectural overview): spawn parallel explorers first, then hand off to the explainer. Go to Step 2a.

When in doubt, take the simple path.

## Step 2a. Explore (complex questions only)

Decompose the question into 2 to 4 exploration angles, each a distinct slice of the subsystem. Spawn every explorer with the Agent tool in a single message, so they run concurrently:

- `subagent_type`: `Explore` (read-only, so an explorer cannot touch the tree)
- `model`: `sonnet`
- `description`: the angle in 3 to 5 words
- `prompt`: `references/explorer-prompt.md` with its placeholders filled in

Then go to Step 3.

## Step 2b. Direct explain (simple questions)

Spawn one Agent that explores and explains in one pass:

- `subagent_type`: `general-purpose`
- `model`: omit it, so the explainer runs on the same model as this session
- `prompt`: `references/explainer-prompt.md` without the explorer-findings section

Go to Step 4.

## Step 3. Synthesize (complex questions only)

Once every explorer has returned, spawn one Agent to merge their findings into one explanation:

- `subagent_type`: `general-purpose`
- `model`: omit it
- `prompt`: `references/explainer-prompt.md` with every explorer's findings filled in

## Step 4. Present

Present the explainer's output to the user. Light edits for clarity or context from the conversation are fine. Do not substantially rewrite it. An explainer's report is not shown to the user on its own, so everything worth reading has to land in your message.

## Output format

The explanation uses the sections defined in `references/explainer-prompt.md`, dropping any that do not apply: Overview, Key Concepts, How It Works, Where Things Live, Gotchas.
