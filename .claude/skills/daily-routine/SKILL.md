---
name: daily-routine
description: The integrated daily routine for the research vault, run automatically by the 07:00 scheduled task. Use this skill when the scheduled task fires, or when the user asks to run the daily routine, the daily check, or the daily maintenance pass manually. Its focus is verification and evaluation. It runs four steps in order — verify, evaluate, expand, concerns — plus a hygiene-and-close step, and writes a dated report to journal/. The routine never writes to the knowledge graph directly: it detects, evaluates, and proposes; only hygiene touches files.
---

# daily-routine

## Purpose

This routine keeps the vault honest and moving every day without manual effort.
Its centre of gravity is **verification and evaluation**: catch drift from the
agreed direction, judge what is worth pursuing, and surface concerns that need
the user's attention. It still branches promising ideas sideways, but only as
**proposals** — it does not expand the graph on its own.

The guiding principle: **the daily routine never writes to the knowledge graph
directly. It detects, evaluates, and proposes. Only the hygiene step touches
files** (date stamps, the report, the commit). Every substantive addition or
change waits for the user's explicit approval through `proposals/`.

## When it runs

Every day at 07:00 via the scheduled task (cron `0 7 * * *`). It can also be run
manually when the user asks.

Note: the meta-level review — proposing *new contributions* and *revisions to
`Direction.md`* — is deliberately **not** part of this routine. That is the
`review-direction` skill, which the user invokes manually when they want it.

Likewise, **batched promotion** (`inbox/` → `ideas/`, `ideas/` → `approaches/`)
is the `promote-notes` skill, and **methodology drafting** is the
`specify-methodology` skill — both invoked manually. Neither is part of this
routine. Methodology drafting in particular is heavyweight and does not need a
daily cadence; run `specify-methodology` on demand when an approach is ready.

## The steps

Run them in order. Each step contributes a section to the daily report.

### Step 1 — Verify

Apply the `verify-consistency` procedure (see
`.claude/skills/verify-consistency/SKILL.md`), scoped to notes created or
modified since the last daily report, plus the notes they link to. Serious
conflicts become proposals in `proposals/`. Put the findings in the report's
**Verification** section.

### Step 2 — Evaluate

This step is a gate between verification and expansion. For the live notes in
`ideas/` and `approaches/` — prioritising recently active ones — assess three
things:

- **Feasibility** — can this realistically be done within the constraints in
  `Direction.md`?
- **Redundancy** — does it overlap an existing note or well-known prior work?
- **Research value** — is it novel and worth the effort?

Record the assessment in the report's **Evaluation** section. Do **not** move or
archive notes based on this — recording only (this was a deliberate design
choice; the user reads the evaluation and decides). The evaluation also produces
a shortlist of high-value notes that feeds step 3.

### Step 3 — Expand (propose only)

Take 1–3 high-value ideas from the evaluation shortlist and branch them:
variants, adjacent ideas, alternatives suggested by counter-examples. **Do not
create the notes directly.** Instead, file each branch as an *expansion
proposal* in `proposals/` (template below), with a draft of the note and the
target folder. Summarise in the report's **Expansion** section, linking to the
proposals.

On approval, the new note is created in the proposed folder — `inbox/` for a
rough fragment, `ideas/` for a branch that is already a coherent idea — and the
proposal is moved to `archived/`.

### Step 4 — Concerns

The synthesis layer above the per-note work of Verify and Evaluate. Capture what
does not reduce to a single note or a single conflict: drift trends away from
`Direction.md`, notes that have stagnated with no progress, pending proposals
piling up in `proposals/`, and anything that needs a user decision. Keep this
distinct from Verification (specific conflicts) and Evaluation (per-note
judgment). Put it in the report's **Concerns** section.

### Step 5 — Hygiene & close

- Scan for broken wiki-links and orphan notes. Flag them in the report. Fixing
  an existing note is a *change* — if non-trivial, file a proposal rather than
  editing directly.
- Update the `updated:` date on any notes touched today.
- Write the full report to `journal/YYYY-MM-DD-daily.md`.
- Commit the vault: `git add -A && git commit -m "daily-routine YYYY-MM-DD: <one-line summary>"`.

## Daily report template

Write the **Summary** last, but place it first so a reader gets the whole
picture before the detail.

```markdown
# Daily Report — YYYY-MM-DD

## Summary
<!-- Written last, placed first. What moved today, and what now needs the user's
     decision — especially pending proposals in proposals/ awaiting review. -->

## Verification
<!-- Conflicts, ambiguity, duplication, orphans found ([[link]] the notes). Proposals filed. -->

## Evaluation
<!-- Feasibility / redundancy / research-value assessment. The shortlist. -->

## Expansion
<!-- Branch ideas filed as expansion proposals (as [[links]] to prop-NNNN),
     and from which [[originals]]. Nothing created directly. -->

## Concerns
<!-- Synthesis layer: drift trends, stagnated notes, proposal backlog, decisions needed. -->

## Hygiene
<!-- Links and orphans flagged or fixed; commit hash. -->
```

## Expansion proposal template

When step 3 branches an idea, create `proposals/prop-NNNN-short-title.md`. This
is an *addition* proposal — distinct from the *change* proposals that
`verify-consistency` files — so it carries the `expansion` tag and drafts the
note rather than an edit:

```markdown
---
id: prop-NNNN
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [proposal, expansion]
source: "daily-routine YYYY-MM-DD"
related: ["[[origin-note]]"]
---

## Proposed addition
<!-- The branch idea in one or two sentences, and how it relates to the origin. -->

## Target
<!-- The folder the note should be created in on approval: inbox/ (rough fragment)
     or ideas/ (coherent idea), with a one-line reason for the maturity call. -->

## Rationale
<!-- Why this branch is worth pursuing; [[link]] the origin note and any related notes. -->

## Draft note
<!-- The full draft of the new note to create on approval, frontmatter included. -->

## Status
Pending review.
```

The user reviews proposals in conversation. On approval, create the drafted note
in the target folder, link it back to its origin, and move the proposal note to
`archived/`.
