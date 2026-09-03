---
name: verify-consistency
description: Audits the vault's live notes against Direction.md and reports note conflicts, baseline drift, ambiguity, duplication, orphan notes, broken wiki-links, undefined or colliding codes, and stale or dangling references. Use when the user asks to verify, check consistency, audit the vault, find contradictions, or clean up stale references — and offer it proactively when a new note or experiment design looks like it may clash with a confirmed decision, after a batch of notes has just been created, when Direction.md itself has just changed, or when the user is about to build on material that has not been checked in a while. It detects and reports only — fixes go through proposals/.
---

# verify-consistency

## Purpose

A research vault accumulates fast. Without periodic checking, notes drift away
from `Direction.md` (the agreed baseline), silently duplicate each other, or
float disconnected from the rest of the graph. This skill finds those problems
so they can be resolved before they compound.

Drift runs both ways. Usually the note is what went wrong, but a **Working**
section of `Direction.md` can itself go stale as evidence accumulates, and this
skill reports that case too rather than assuming the baseline is always right.

This skill **detects and reports** — it does not fix. Fixes to existing notes or
to `Direction.md` are *changes*, and changes go through `proposals/`.

## When to use

- **Explicit** — the user asks to verify, check consistency, audit the vault,
  find contradictions, or clean up stale references. Run it.
- **Proactive** — reach for it unasked when a new note or experiment design
  looks like it may clash with a confirmed decision in `Direction.md`; right
  after a batch of notes has been created; when `Direction.md` itself has just
  changed; or when the user is about to build on material that has not been
  checked in a while.

Proactive means **offer in one line and wait**, not start. A full audit reads
every live note, so it never runs unprompted. Name the specific worry when
offering — "this may cut against the scope line in `Direction.md`; want me to
run a check?" beats a generic offer to audit.

## Baseline: settled, working, tentative

Everything in `notes/` and `experiments/` is **tentative** — work in progress.
`Direction.md` is the baseline it is measured against, and that baseline has two
tiers, marked on each of its sections:

- **Settled** — `## Confirmed decisions` and `## Constraints`. Ground truth.
  Either the line is not the kind of claim an experiment can refute (a resource
  limit, a deadline), or changing it would invalidate work already done (the
  model family under study, the evaluation metric). When a note disagrees with a
  Settled line, **the note is what is wrong.**
- **Working** — `## Topic`, `## Goal`, `## Scope`. The current best direction,
  written when the least was known and expected to move. When enough evidence
  piles up against a Working line, **the baseline may be what is stale**, and
  saying so is part of this skill's job.

Tentative notes are also compared against each other. Neither tier is edited
here — see the procedure. The tier decides which side a disagreement is reported
against, nothing more, and a Settled line is not sealed: the user can question
one at any time; this skill just does not do it unprompted.

## Scope

- **Full audit** — check every note in `notes/` and `experiments/`.
- **Incremental** — when a quick re-check is wanted, focus on notes created or
  modified since the last `journal/` verify report, plus any notes they link to.

## What to detect

1. **Note conflict** — a tentative note directly contradicts a **Settled** line
   in `Direction.md`, or two notes contradict each other. The note is the
   problem; report it against the line it breaks.
2. **Baseline drift** — the evidence has turned against a **Working** line in
   `Direction.md`. Two conditions must both hold, or this is not drift: at least
   **two independent live notes** pull the same way against that line, **and at
   least one of them is an `experiments/` result or a `references/` finding** —
   evidence, not opinion. One note, or a cluster of untested ideas, is a note
   conflict at most. "This feels stale" is never a reason. Report drift; do not
   file a proposal for it (see the procedure).
3. **Ambiguity** — a note is open to readings that diverge from `Direction.md`,
   or uses a key term inconsistently with how the rest of the vault uses it.
4. **Duplication** — two notes cover substantially the same ground without
   linking each other.
5. **Orphan** — a note has no incoming or outgoing `related` links; it is
   disconnected from the graph and likely to be forgotten.
6. **Undefined or colliding code** — a note uses a project-coined code that has
   no entry in `Glossary.md`, or uses one with a meaning that conflicts with its
   Glossary entry or collides with another code's.
7. **Broken link** — a `[[wiki-link]]` whose target note does not exist in the
   vault. Because promotion creates new notes and `archived/` keeps original
   filenames, a broken link usually means a typo or a note that was deleted
   rather than archived.
8. **Stale or dangling reference** — a `Glossary.md` entry whose defining note
   is missing or has been moved to `archived/`; a resolved question still
   sitting in `Memory.md` `## Open Questions`; a `## Working Context` item
   that is no longer valid; or an experiment note's `datasets:` link pointing to
   a heading absent from `workspace/datasets.md`, or its `code:` path that does
   not exist. (The contents of `workspace/data/` and `workspace/runs/` are out
   of scope — like `outputs/`, verification leaves them alone.) Report these —
   removing one edits a master file, which is a *change*, so it goes through a
   proposal, not a direct edit. File that proposal for the `Glossary.md` and
   `datasets:`/`code:` cases. The two `Memory.md` cases stay in scope to
   *detect* but not to act on —
   pruning the master files belongs to `prune-master-files`. Report them, name
   that skill as the fix, and offer to run it, rather than filing a proposal here
   that would compete with the one it writes.

## Procedure

1. **Read `Direction.md` in full.** This is the baseline for every comparison —
   note which sections are marked **Settled** and which are **Working**, because
   that decides how a disagreement gets reported.
   Also read `Glossary.md` — the registry of project-coined codes — so codes used
   in notes can be checked against their definitions, and each Glossary entry's
   defining note can be checked for existence. Read `Memory.md` too, so stale
   `## Open Questions` and `## Working Context` items can be flagged. Read
   `workspace/datasets.md` as well, so experiment notes' `datasets:` links can be
   checked against the registry.
2. **Read the in-scope notes** (see Scope above).
3. **Check each note** against every category above. Be concrete — quote the
   exact lines that conflict, name the exact notes that duplicate, name the codes
   that are undefined or collide, name the missing link targets.
4. **Write the report** to `journal/YYYY-MM-DD-verify.md` using the template
   below.
5. **File proposals for serious issues.** A *serious* issue is one whose
   resolution requires editing or archiving an existing note, or editing
   `Direction.md` — that is a change, not an addition, so create a proposal note
   in `proposals/` (template below). Minor issues (orphans, light ambiguity that
   the user can fix in passing) stay in the report only. Two findings hand off
   instead of being filed here. Stale `Memory.md` items go to
   `prune-master-files` (see **Stale or dangling reference**). **Baseline drift**
   goes to `review-direction` — revising a Working section is direction-level
   work, so report the drift, name that skill as the fix, and offer to run it.
6. **Never edit notes or `Direction.md` directly.** Detection and reporting
   only.

## Verification report template

```markdown
# Verification Report — YYYY-MM-DD

## Scope
<!-- Which notes were checked. -->

## Note conflicts
<!-- Each: [[link]] the note, the Settled Direction.md line or [[other note]] it
     breaks, and why. -->

## Baseline drift
<!-- Each: the Working Direction.md line under pressure, [[links]] to the two or
     more notes pulling against it, and which of them is the experiment result or
     reference that clears the evidence bar. Say plainly that this is a report,
     not a proposal, and offer to run review-direction. Leave empty if none. -->

## Ambiguities
<!-- Each: [[link]] the note, the ambiguous wording, the divergent readings. -->

## Duplications
<!-- Each: [[link]] the pair of notes, the overlapping content. -->

## Orphans
<!-- [[Link]] the notes that have no links in or out. -->

## Undefined / colliding codes
<!-- Each: [[link]] the note, the code, and whether it is undefined in Glossary.md or conflicts. -->

## Broken links
<!-- Each: [[link]] the note, and the missing target the wiki-link points to. -->

## Stale / dangling
<!-- Glossary entries whose defining note is gone; resolved Open Questions or dead
     Working Context items in Memory.md; experiment-note datasets:/code: links with
     no matching workspace/datasets.md entry or missing code path. Note which were
     filed as proposals, and which were handed to prune-master-files. -->

## Summary
<!-- Counts per category, and which items were filed as proposals (prop-NNNN). -->
```

## Proposal note template

When a serious issue needs a change, create `proposals/prop-NNNN-short-title.md`:

```markdown
---
id: prop-NNNN
created: YYYY-MM-DD
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
