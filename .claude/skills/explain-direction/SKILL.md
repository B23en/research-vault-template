---
name: explain-direction
description: Explain the vault's Direction.md in plain language — walk through
  each element with an easy, intuitive gloss and give an overall summary of
  where the research is headed. Use when the user wants to understand, skim, or
  be walked through the current research direction. It is read-only — never
  edits Direction.md and proposes no changes; revisions are review-direction's
  job.
---

# explain-direction

## Purpose

`Direction.md` is the verification baseline, kept deliberately terse — it is
ground truth, not a scratchpad. This skill makes it legible: it reads the live
`Direction.md` and explains it back in plain language so the whole direction is
graspable at a glance, without touching the ground-truth wording.

Read-only and conversational: it explains in chat, writes no files, and proposes
no changes. If something looks worth revising, it says so and points to
`review-direction`, which owns direction revisions.

## When to use

- The user asks to explain, summarize, walk through, or make sense of the
  research direction / `Direction.md`.
- Not for revising the direction (that is `review-direction`) and not for
  checking notes against it (that is `verify-consistency`).

## Procedure

1. **Read the current `Direction.md` in full.** Always explain from the live
   file, never from memory. If it is still empty template stubs, say so plainly
   rather than inventing content.
2. **Annotate each element.** Go section by section — Topic, Goal, Confirmed
   decisions, Scope (in / out), Constraints — and for every concrete item give a
   one-line plain-language gloss: what it means and why it matters. Present it as
   a list. Stay faithful: explain only what is written, invent nothing.
3. **Summarize the overall direction.** One short paragraph: what this research
   is trying to do, the shape of its boundaries, and the through-line that
   connects the pieces.
4. **Flag, don't fix.** If an item reads as ambiguous, outdated, or worth
   revising, note it briefly and suggest running `review-direction` — but make
   no proposal and edit nothing here.
