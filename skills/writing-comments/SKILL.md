---
name: writing-comments
description: "How code comments get written: what earns one, how it reads, the sediment to keep out, and the passes it goes through. Load before you write or change any comment in a source file, including doc comments (godoc, JSDoc, docstrings), file headers and TODO markers; when porting, renaming or retiring a predecessor, where comments turn into changelogs; when auditing the comments already in a file; and whenever you weigh whether something needs a comment at all."
---

# Writing comments

A comment is the one part of a source file addressed to a human. Write it for the next reader of the code, never for the user and never for the diff.

## What earns a comment

- **The why.** The reason, the constraint, the bug that forced this shape. The code already states the what. State the constraint as it stands today rather than the story of meeting it: "node-notifier forwards only exit status -1, so a failed toast reports success" earns its place, "that failure used to be invisible" is the same fact wearing a diff.
- **The definition below it.** Functions, types, classes, exported constants: what it does and how it is meant to be used, in the language's own doc format.
- **The surprise.** A workaround, an ordering that matters, a magic number, a link to the issue or spec behind it.
- **The gap.** A `// TODO: short explanation` says what is missing, not that something is missing.

Lines that speak for themselves stay bare. A comment that repeats its code in English costs the reader twice: once to read it, once to check it still matches.

## How it reads

- Describe the code as it stands. The reader carries no memory of the previous version.
- One comment, one idea, in the shortest form that carries it.
- Name the mechanism or the number. "Retries twice, the gateway drops the first connect" beats "handles connection issues gracefully".
- Follow the file. Doc format, tense and person come from the code around it.
- Keep it true. When you change code, the comments around it move with it, including the ones you did not write. A comment also goes stale when what it points at moves: a renamed badge in an example, a doc section that now lives somewhere else, a count that no longer matches the list beneath it.

## Sediment

A comment carries **sediment** when it describes the repository's past instead of the code in front of the reader. It feels like context to whoever just did the work and reads as noise to everybody after them, because the version it argues with is not on screen and never will be again. The rewrite is always the same move: keep the fact, drop the chronology.

| Sediment | What it was trying to say |
| --- | --- |
| `the old templates repeated this nine times` | this helper is the one place that knowledge lives |
| `a port of the Go tool, same flags and sequence` | the sequence is notify, then minimize, then mute |
| `stopping at the first dash made the two runs different` | a global flag is legal anywhere on the line |
| `nix-darwin owned this path once and took the rule with it` | nix-darwin claims this path and its uninstaller takes the rule |
| `kept from the original`, `exactly as before`, `as it always has` | nothing: the sentence is finished without the clause |

Migration is when sediment settles. Porting a file, renaming a tool, retiring a predecessor, cleaning up after a refactor: your context is full of the version that is going away, so the new comment documents the move, and nothing you run afterwards flags it. Phase numbers, the name of the tool that used to do this, and "now" in any form all belong to that moment and to no reader after it. Write each comment as though the previous version never existed.

## The passes

Comments are prose that lands in a file, so they go through the same two passes as any other. Run both over the comments you touched, once, before you hand the file back.

- `technical-writing` for plainness: short sentences, active voice with a named actor, the common word over the fancy one. Aim at the rules rather than enforce them. A comment is usually one sentence or a fragment, so the sentence-length limits are a ceiling you rarely reach, not a length to fill.
- `unslop` for voice: cut the tells, so the comment reads like the person who wrote the code wrote it.

Then read each one as somebody who has never seen any earlier version of the file. Every comment that only makes sense beside the version you just replaced is sediment, and the fact inside it still has to be said plainly or deleted.
