---
name: verify-consistency
description: Check the research vault's live notes for consistency against Direction.md and flag conflicts, ambiguity, duplication, and orphan notes. Use this skill whenever the user asks to verify, check consistency, audit the vault, find contradictions, or sanity-check ideas against the agreed research direction — and whenever a new idea or approach might clash with established decisions. The daily routine reuses this same procedure.
---

# verify-consistency

## Purpose

A research vault accumulates fast. Without periodic checking, notes drift away
from `Direction.md` (the agreed baseline), silently duplicate each other, or
float disconnected from the rest of the graph. This skill finds those problems
so they can be resolved before they compound.

This skill **detects and reports** — it does not fix. Fixes to existing notes or
to `Direction.md` are *changes*, and changes go through `proposals/`.

## Baseline: confirmed vs tentative

`Direction.md` is **confirmed** — treat everything in it as ground truth.
Everything in `ideas/`, `approaches/`, `experiments/`, and `problems/` is
**tentative** — work in progress. Verification compares tentative notes against
the confirmed baseline, and tentative notes against each other.

## Scope

- **Standalone invocation** — check every note in `ideas/`, `approaches/`,
  `experiments/`, `problems/`.
- **Inside `daily-routine`** — focus on notes created or modified since the last
  `journal/` entry, plus any notes they link to.

## What to detect

1. **Conflict** — a tentative note directly contradicts a confirmed decision in
   `Direction.md`, or two notes contradict each other.
2. **Ambiguity** — a note is open to readings that diverge from `Direction.md`,
   or uses a key term inconsistently with how the rest of the vault uses it.
3. **Duplication** — two notes cover substantially the same ground without
   linking each other.
4. **Orphan** — a note has no incoming or outgoing `related` links; it is
   disconnected from the graph and likely to be forgotten.

## Procedure

1. **Read `Direction.md` in full.** This is the baseline for every comparison.
2. **Read the in-scope notes** (see Scope above).
3. **Check each note** against the four categories. Be concrete — quote the
   exact lines that conflict, name the exact notes that duplicate.
4. **Write the report** to `journal/YYYY-MM-DD-verify.md` using the template
   below. (When running inside `daily-routine`, contribute this content to the
   verification section of the daily report instead of a separate file.)
5. **File proposals for serious issues.** A *serious* issue is one whose
   resolution requires editing or archiving an existing note, or editing
   `Direction.md` — that is a change, not an addition, so create a proposal note
   in `proposals/` (template below). Minor issues (orphans, light ambiguity that
   the user can fix in passing) stay in the report only.
6. **Never edit notes or `Direction.md` directly.** Detection and reporting
   only.

## Verification report template

```markdown
# Verification Report — YYYY-MM-DD

## Scope
<!-- Which notes were checked. -->

## Conflicts
<!-- Each: [[link]] the note, the conflicting Direction.md line or [[other note]], and why. -->

## Ambiguities
<!-- Each: [[link]] the note, the ambiguous wording, the divergent readings. -->

## Duplications
<!-- Each: [[link]] the pair of notes, the overlapping content. -->

## Orphans
<!-- [[Link]] the notes that have no links in or out. -->

## Summary
<!-- Counts per category, and which items were filed as proposals (prop-NNNN). -->
```

## Proposal note template

When a serious issue needs a change, create `proposals/prop-NNNN-short-title.md`:

```markdown
---
id: prop-NNNN
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [proposal, consistency]
source: "verify-consistency YYYY-MM-DD"
related: ["[[affected-note]]"]
---

## Proposed change
<!-- What to change, in one or two sentences. -->

## Target
<!-- Which file(s) this touches, as [[wiki-links]]. -->

## Rationale
<!-- [[Link]] the notes involved; quote the exact contradicting lines; give the reasoning. -->

## Concrete edit
<!-- The exact edit to apply on approval: text to add, remove, or replace. -->

## Status
Pending review.
```

The user reviews proposals in conversation. On approval, apply the concrete edit
and move the proposal note to `archived/`.
