---
name: papyrus-latex-comments
description: Set up and use a non-destructive COMMENT layer in a LaTeX document — insert margin/inline notes (tagged by type) next to the author's text instead of rewriting it. Use when asked to comment on, review, or annotate a .tex file. For proposing actual replacement text the author can accept/reject, use papyrus-latex-suggestions.
triggers: comment, annotate, todonotes, margin note, review note, aicomment
---

# LaTeX Comments

Add a visible, attributable, removable layer of NOTES to a LaTeX document —
remarks ABOUT the text, never a rewrite of it. Insert a macro call next to the
relevant text. See `papyrus-writing` for the behaviour rules and the comment
taxonomy. To propose concrete replacement text (accept/reject), use
`papyrus-latex-suggestions`.

## Step 1 — Setup (idempotent)

```bash
kpsewhich todonotes.sty    # non-empty = installed (ships with TeX Live — usually no install)
```

If the document has no comment preamble yet, inject this once near the top of the
preamble (never duplicate it if it is already there):

```latex
% ==== Papyrus comment layer — safe to leave in; flip to hide ====
\usepackage[colorinlistoftodos,textsize=scriptsize]{todonotes}
\newcommand{\aicomment}[1]{\todo[color=cyan!25,bordercolor=cyan]{\textbf{AI:} #1}}   % margin note
\newcommand{\aiinline}[1]{\todo[inline,color=cyan!25]{\textbf{AI:} #1}}              % full-width block in the text
\newcommand{\aisuggest}[2]{#1\aicomment{suggest → #2}}                              % keep original, idea in the margin
% FINAL BUILD: change the \usepackage line to  \usepackage[disable]{todonotes}
% ================================================================
```

Margin space is tight, so `textsize=scriptsize` keeps notes readable in a normal
one-column margin. In a **two-column or narrow-margin** paper the margin barely
exists and margin notes overflow — use `\aiinline` (a full-width block in the
text flow) instead of `\aicomment`.

## Step 2 — Insert comments

Add a macro call next to the relevant text. Do NOT rewrite the prose. Tag every
note with the taxonomy (`[claim] [cite] [clarity] [structure] [contribution]
[rigor] [style] [typo]`).

```latex
The method is fast.\aicomment{[claim] by how much? add a number + CI}
\aiinline{[structure] this reads like Related Work — consider moving it}
We \aisuggest{imitate}{reproduce} the baseline.   % original stays; idea in the margin
```

Put `\listoftodos` after `\maketitle` (or in an appendix) so the author gets a
review to-do list and can address each note, then delete the macro call.

## Step 3 — Finalize

Hide every note in one edit: switch the package line to
`\usepackage[disable]{todonotes}`. Remove leftover macro calls once a note is
addressed.

## Rules

- Insert macro calls; never rewrite prose the author did not ask you to change.
- Never fabricate a citation to fill a `[cite]` note.
- One sentence per line in the source keeps every suggested diff minimal.
- Never rename or "tidy" the author's macros, labels, or bib keys.
