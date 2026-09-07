---
name: papyrus-make-fluent
description: Polish the English of a LaTeX passage — fluency, grammar, and clarity — as tracked suggestions, without changing structure or meaning. Use when the author asks to make text fluent/readable, fix the English, proofread, or tighten wording. Includes a mandatory global-consistency (ripple) check.
triggers: make fluent, polish, proofread, fix english, tighten, readable, rephrase
---

# Make Fluent

Transform mode: improve HOW it reads, never WHAT it says or WHERE it sits.
Propose changes as tracked suggestions the author accepts or rejects — do not
silently overwrite. Mechanics: `papyrus-latex-suggestions` (tracked inline
edits). Behaviour and style targets: `papyrus-writing` (conduct + Gopen & Swan
principles + LaTeX house style).

## What you MAY change
- Grammar, spelling, agreement, articles, tense.
- Awkward or wordy phrasing → tighter and clearer (topic/stress position, subject
  close to verb, old→new flow).
- Hedging and redundancy.

## What you must NOT change
- **Structure** — do not move, merge, split, add, or delete sentences/paragraphs.
  That is a `papyrus-review-paper` `[structure]` matter; flag it, don't do it.
- **Meaning** — never alter a claim, number, result, definition, or citation.
- **Voice** — match the author's terminology, notation, macros, and bib keys;
  don't flatten to generic prose.
- **Layout** — never rewrap paragraphs you weren't asked to touch (one sentence
  per line keeps diffs minimal).

## Procedure
1. First read a few passages the author has already written *fluently* to learn
   their style and level of English, then match it — "chameleon mode". Then read
   the target passage plus enough surrounding text to keep terminology consistent.
2. Propose each change as a tracked edit via `papyrus-latex-suggestions` —
   `\aisuggest[author=papyrus, id=…, status=pending]{old}{new}` — so the old text
   is preserved and the author decides.
3. Keep edits sentence-local and minimal: one suggestion per issue, each paired
   with an `\aicomment` giving the reason.

## Then: ripple / global-consistency check (mandatory — see papyrus-writing §7)
A local rewording can desync a tightly cross-referenced paper. After polishing,
sweep for and FLAG (do not silently propagate):
- a term you reworded that is used — and must still match — elsewhere, including
  the abstract, intro, and captions;
- notation or symbols defined earlier;
- whether the abstract/intro claims still match the edited body (no new over- or
  under-claiming).

Offer to propagate a rename across the whole paper; never do it silently.
