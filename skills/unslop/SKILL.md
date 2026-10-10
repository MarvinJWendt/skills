---
name: unslop
description: Cut AI tells from prose and give it a human voice. Load before writing or editing prose that lands in a file (markdown, HTML, README, docs, changelog, commit body, doc comment), and on a direct /unslop call against a target, such as "/unslop your last message" or "/unslop this document".
---

# Unslop

Prose that reads as machine-written fails at its job. This is the pass that fixes it.

## When it runs

- **Prose going into a file.** Apply the tells while drafting, then run the pass over what you wrote before handing the file back. Markdown, HTML, READMEs, docs, changelogs, release notes, commit bodies, doc comments.
- **A direct `/unslop <target>` call.** Rewrite the named target: a file, a section of one, or your own last message. Edit files in place. For a chat message, print the rewrite and nothing around it.

## The pass

1. Read the target once for what it is trying to say.
2. Walk every tell below against it. All of them, not the ones that come to mind.
3. Rewrite. Meaning survives, tone matches the document around it.
4. Give it a voice (see below).
5. Ask: "what still marks this as AI written?" Fix what that turns up, and repeat until it turns up nothing.

## Mechanism, not mood

The one test that catches what the catalogue misses. "The database stays close at hand", "SQL you can read", "types that follow your schema" all name a feeling. Replace each with the mechanism or the number: "`.toSQL()` returns the exact string sent to the database", "a column rename fails the build".

Ask what the sentence tells the reader to do or know, then write that. If it cannot be restated as a concrete instruction, fact, or number, cut it. Second check: a sentence that could sit unchanged in another project's docs says nothing about this one. Cut that too.

## Give it a voice

Removing tells is half the job. Voiceless writing gives itself away just as fast.

- **Have an opinion.** React to the facts instead of listing pros and cons and leaving.
- **Vary the rhythm.** Short sentences. Then a longer one that takes its time getting where it is going. Mix them.
- **Admit complexity.** "Impressive and slightly unsettling" beats "impressive".
- **Use "I" when it fits.** First person is not unprofessional.
- **Let some mess in.** Perfectly parallel structure reads as machine-made.
- **Be specific.** Not "this is concerning" but "there is something off about agents grinding away at 3am".

## Leave alone

- Text somebody else wrote: quotes, third-party docs, the user's own words. Fix your prose, not theirs.
- Wording an API, spec, error message, or established convention fixes.
- Document structure. Fix sentences. Reorganizing headings or reordering sections is a separate task, so do it only when asked.
- Hedges and qualifiers carrying real uncertainty. "usually fails" is a different claim than "fails". Accuracy outranks brevity every time.

## Tells

### Substance

1. **Puffery and promotion.** "pivotal moment", "testament to", "evolving landscape", "groundbreaking", "renowned", "vibrant", "breathtaking", "nestled", "must-visit". State what happened.
2. **Vague attribution.** "Experts believe", "industry reports suggest", "some critics argue". Name the source or drop the claim.
3. **Superficial -ing tails.** "...highlighting the need for", "...ensuring reliability", "...showcasing its power". Delete the clause, or replace it with the fact it gestures at.
4. **Formulaic arcs.** "Despite challenges, X continues to thrive." Write the specific facts instead.
5. **Cutoff disclaimers.** "While specific details are limited". Go find the detail or drop the sentence.
6. **Generic conclusions.** "The future looks bright." End on a fact or the next step, or end without a closer at all.

### Words

7. **AI vocabulary.** additionally, crucial, delve, enhance, foster, garner, interplay, intricate, landscape, leverage, pivotal, robust, seamless, showcase, tapestry, testament, underscore, utilize, vibrant. The plain word wins: use, help, many, if.
8. **Fancy ways to say "is".** "serves as", "stands as", "boasts", "features". Say "is" or "has".
9. **Abstract metaphor nouns.** substrate, wedge, vector, locus, nexus, primitive, harness, bedrock, scaffolding, modality, paradigm, gold-plating, ratchet, evacuate, endgame, north star, flywheel, surface (as in "API surface"). Each has a concrete replacement: substrate is base, wedge in is add, vector is way, gold-plating is more than the job needs, evacuate is move out, endgame is the last phase, ratchet is the mechanism's real name.
10. **Synonym cycling.** Protagonist, main character, central figure, hero across one paragraph. Pick one name and repeat it.
11. **Adverbs propping up weak verbs.** "runs quickly" is "is fast", or the measured number. A weak verb needing an adverb is the wrong verb.

### Sentence shapes

12. **"Not just X, but Y."** Say the point directly.
13. **Rule of three.** Ideas forced into a group of three. Use the number that exists.
14. **False ranges.** "from X to Y" where X and Y are not ends of a scale. List the items.
15. **Filler openers.** "In order to" is "To". "Due to the fact that" is "Because". "It is important to note that" is nothing.
16. **Stacked hedging.** "could potentially possibly be argued that it might" is "may".
17. **Passive voice with a known actor.** "queries are validated" is "the compiler validates queries". Passive holds only when the actor is unknown or genuinely does not matter.
18. **Dense sentences.** If the reader backtracks to parse it, split it or drop clauses. One idea per sentence.

### Mechanics

19. **Em dashes.** Use a comma or start a new sentence. Parentheses, en dashes, and hyphens standing in for a dash trade one tell for another, so they are not the fix.
20. **Mid-sentence colons.** Fine before a list or an example. As a connector a colon adds nothing: "If you're coming from traditional automation: instead of registering event handlers, you describe conditions" survives the colon's removal and gets better for it. Rewrite so the point stands without the comparison framing.
21. **Boldface everywhere.** Bold every proper noun and acronym and nothing stands out.
22. **Inline-header lists.** The tell is a bold label restating the line behind it ("**Performance:** Performance improved..."). Turn those into prose. A bold lead-in that names the item and is followed by genuinely new detail ("**Schema in TypeScript.** Tables live in one file.") is fine.
23. **Title case headings.** Sentence case.
24. **Decorative emojis.** None in headings or bullets.
25. **Curly quotes.** Straight quotes.

### Chat noise in a file

26. **Chatbot phrases.** "I hope this helps", "Let me know if", "Of course!", "Certainly!", "Found the smoking gun!". Remove.
27. **Sycophancy.** "Great question!", "You're absolutely right!". Say the thing and move on.
