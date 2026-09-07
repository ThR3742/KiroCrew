---
name: papyrus-review-paper
description: Review a LaTeX paper and leave feedback as non-destructive comments. Use when the author asks for a review, critique, or feedback — on the whole paper, on one section, or along a single axis (e.g. "are my claims supported?", "is the contribution clear?", "is notation consistent?"). Comments only; does not rewrite.
triggers: review, critique, feedback, referee, read my paper, is my contribution clear
---

# Review Paper

Feedback mode: read, judge, and leave tagged comments — never rewrite the prose.
Use `papyrus-latex-comments` for the mechanics (review preamble +
`\aicomment`/`\aiinline`) and `papyrus-writing` for the comment taxonomy,
behaviour, and the paper-quality principles you judge against.

## Step 0 — Pick the scope
- **whole** — the entire paper.
- **section** — one section/subsection the author points at.
- **axis** — one lens swept across the whole paper (claims supported?
  contribution clear? notation consistent? body over-claiming vs the abstract?).

If the ask is vague ("what do you think?"), ask ONE sharp question first: clarity,
correctness, completeness, or persuasiveness?

## Step 1 — Gather context FIRST (never critique in a vacuum)
Load the paper-context note (`<project-dir>/.papyrus/paper-context.md`) for the
central contribution, the venue + page/word limit, and the mental map. Then:
- **section scope**: read the target section AND its neighbours + the
  abstract/intro, so feedback is tied to what this section must DO for the paper
  and whether it serves the one contribution.
- **whole / axis scope**: skim top-to-bottom once to hold the structure before
  commenting.

Refresh the note only on a structural change (see `papyrus-writing`); otherwise
read the live `.tex` for exact claims/numbers/wording.

## Step 2 — Make sure the comment layer exists
Ensure the review preamble is present (see `papyrus-latex-comments` Step 1).
Idempotent — don't duplicate it.

## Step 3 — Comment, don't rewrite
Walk the text and attach a tagged comment at each issue via `\aicomment{[tag] …}`
/ `\aiinline{…}`. Tags: `[claim] [cite] [clarity] [structure] [contribution]
[rigor] [style] [typo]`. Say WHY, and point at a direction where useful — but
leave the fix to the author. Never fabricate a citation for a `[cite]` note.

## Step 4 — Report, highest value first
Summarise in chat ordered by impact: `[contribution]`/`[rigor]` →
`[structure]`/`[claim]`/`[cite]` → `[clarity]`/`[style]`/`[typo]`. Lead with the 3
issues that most threaten acceptance. End by offering to polish (hand off to
`papyrus-make-fluent`) or to address a specific batch.
