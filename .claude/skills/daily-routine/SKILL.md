---
name: daily-routine
description: The integrated daily routine for the research vault, run automatically by the 07:00 scheduled task. Use this skill when the scheduled task fires, or when the user asks to run the daily routine, the daily check, or the daily maintenance pass manually. It runs five steps in order — verify, evaluate, expand, specify, hygiene — and writes a dated report to journal/.
---

# daily-routine

## Purpose

This routine keeps the vault moving and honest every day without manual effort:
it catches drift from the agreed direction, judges what is worth pursuing,
pushes promising ideas forward, drafts methodology, and keeps the vault tidy and
version-controlled. It is self-contained — it runs all five steps itself.

## When it runs

Every day at 07:00 via the scheduled task (cron `0 7 * * *`). It can also be run
manually when the user asks.

Note: the meta-level review — proposing *new contributions* and *revisions to
`Direction.md`* — is deliberately **not** part of this routine. That is the
`review-direction` skill, which the user invokes manually when they want it.

## The five steps

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
a shortlist of high-value notes that feed steps 3 and 4.

### Step 3 — Expand

Take 1–3 high-value ideas from the evaluation shortlist and branch them:
variants, adjacent ideas, alternatives suggested by counter-examples. Create new
notes for the branches in `inbox/` or `ideas/` (additive — do it directly),
linked back to the originals. Summarise in the report's **Expansion** section.

### Step 4 — Specify

Take 1–2 mature approaches from the shortlist that have no experiment note yet,
and apply the `specify-methodology` procedure (see
`.claude/skills/specify-methodology/SKILL.md`) to draft an experiment design for
each. Summarise in the report's **Specification** section.

### Step 5 — Hygiene & close

- Scan for broken wiki-links and orphan notes. Flag them in the report. Fixing
  an existing note is a *change* — if non-trivial, file a proposal rather than
  editing directly.
- Update the `updated:` date on any notes touched today.
- Write the full report to `journal/YYYY-MM-DD-daily.md`.
- Commit the vault: `git add -A && git commit -m "daily-routine YYYY-MM-DD: <one-line summary>"`.

## Daily report template

```markdown
# Daily Report — YYYY-MM-DD

## Verification
<!-- Conflicts, ambiguity, duplication, orphans found ([[link]] the notes). Proposals filed. -->

## Evaluation
<!-- Feasibility / redundancy / research-value assessment. The shortlist. -->

## Expansion
<!-- New branch notes created (as [[links]]), and from which [[originals]]. -->

## Specification
<!-- Experiment designs drafted, as [[links]]. -->

## Hygiene
<!-- Links and orphans flagged or fixed; commit hash. -->

## Summary
<!-- What changed today, and what needs the user's attention —
     especially pending proposals in proposals/ awaiting review. -->
```

End the run by making the **Summary** genuinely useful: a person skimming it
should see at a glance what moved and what now needs their decision.
