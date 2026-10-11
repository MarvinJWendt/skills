---
name: grill-me
description: Grill the user relentlessly about a plan, decision, or idea until both sides share one understanding of it. Use on /grill-me, when the user wants to stress-test their thinking, or on any "grill" trigger phrase.
---

Interview the user relentlessly until you reach a shared understanding. Map the subject as a **design tree**: every decision branches into the decisions that hang off it.

Work the tree in **rounds**. The **frontier** is every decision whose prerequisites are already settled: the questions you can ask now without guessing at answers you haven't heard yet. Ask the whole frontier in one round, number each question, and give your recommended answer. Then wait for the user's answers before the next round.

Format a round like so:

```
**Q1. <question title>**: <question body, may run several paragraphs and offer choices>

> Recommended: <your answer, with the reason>

---

**Q2. <question title>**: <question body>

> Recommended: <your answer, with the reason>
```

Every answer reshapes the tree: settled decisions push the frontier outward and unblock the questions that hung off them. Recompute the frontier and ask the next round. A question that depends on another question still open in this round belongs to a later round.

Finding facts is your job, never the user's. When a frontier question needs a fact from the environment (files, tools, docs), dispatch a subagent to find it, and ask nothing you could look up yourself. A running lookup is an unsettled prerequisite: only the questions downstream of it wait for its report, so ask the rest of the frontier now. The decisions belong to the user: put each one to them and wait.

The session is done when the frontier is empty: every branch of the design tree visited, nothing silently assumed. Act on the result only after the user confirms you have reached a shared understanding.
