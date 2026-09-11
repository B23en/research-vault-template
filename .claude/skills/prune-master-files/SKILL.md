---
name: prune-master-files
description: Prunes resolved, superseded, and abandoned material out of Direction.md and Memory.md, preserving whatever it removes or replaces as an approved proposal in archived/. Use when the user asks to prune, clean up, compact, or shorten the master files, or says Direction.md or Memory.md has grown unwieldy — and offer it proactively when an experiment result answers all or part of a standing Open Question, when an approved proposal supersedes a line in Direction.md, when Working Context holds items pointing at notes that no longer exist, or when the two files have grown long enough that reading them in full is a chore. An item that is still live but has partly changed is updated rather than dropped, and an overlong or unclear one may be reworded without changing what it says.
---

# prune-master-files

## Purpose

`Direction.md` and `Memory.md` only ever grow. Decisions pile up, questions stay
open long after something answered them, and `## Working Context` keeps
leftovers from sessions gone by. That costs more than it looks — these two files
are read by most of the skills here, in full, every time they run, so dead
weight in them is paid for on every pass.

This skill removes what is *provably* finished and preserves it as an approved
proposal in `archived/`. Nothing is lost; it is moved off the hot path. An item
that is still live but has partly changed — a question half answered, a limit
that has moved — is updated rather than dropped whole, so what still holds stays
in the file. An item that is merely overlong or unclear may be reworded, too.

## When to use

- **Explicit** — the user asks to prune, clean up, compact, or shorten the
  master files, or says `Direction.md` / `Memory.md` has got unwieldy. Run it.
- **Proactive** — reach for it unasked when an experiment's `## Results` answers
  all or part of a standing `## Open Questions` entry; when an approved proposal
  has just superseded a line in `Direction.md`; when `## Working Context` holds
  items pointing at notes that no longer exist; or when the two files have grown
  long enough that reading them in full is a chore.

Proactive means **offer in one line and wait**, not start. Phase 1 reads both
master files plus most of the vault, and the edit touches the verification
baseline. It never runs unprompted.

## What may be pruned, and under whose authority

This skill invents no permissions. Each target keeps the authority `CLAUDE.md`
already assigns it.

| Target | Editing it is | Gate |
|---|---|---|
| `Memory.md` `## Working Context` | ordinary upkeep — `CLAUDE.md` has stale items removed immediately | apply directly, but still record it |
| `Memory.md` `## Open Questions` | a *change* — `CLAUDE.md` says do not auto-prune | proposal |
| `Direction.md` — `## Confirmed decisions`, `## Scope`, `## Constraints` | a *change* — the baseline is never edited without an approved proposal | proposal |

## Out of scope

- **`Direction.md` `## Topic` and `## Goal`.** Changing what the research *is*
  is a direction revision, not upkeep. Say so and point at `review-direction`.
- **`Memory.md` `## Conventions`.** Standing rules; `CLAUDE.md` says never
  auto-prune them. Change an item only when the user names it explicitly.
- **`Glossary.md`.** Its whole purpose is that a code stays readable months
  later, so entries are meant to outlive the notes that defined them. Pruning it
  defeats the point.
- **Notes in the pipeline folders.** A superseded note moves to `archived/`
  whole — ordinary vault work, not this skill.

## The evidence bar

"This looks old" is not a reason to remove anything. The skill records what has
already been settled — elsewhere in the vault, or by the user — and never
settles anything itself. Every proposed removal or update carries a verdict and
a link that proves it, and a verdict may cover a whole item or only part of one:

| Verdict | Evidence required |
|---|---|
| **Resolved** | the note, experiment result, or decision that answers it — `[[linked]]` |
| **Superseded** | the newer `Direction.md` line, or the approved proposal that replaced it |
| **Abandoned** | the archived note, or the direction revision that dropped that branch |
| **Expired** | what changed — a date passed, a resource limit moved, a tool went away |

**No evidence, no proposal.** An item that merely smells stale goes on the
`Unresolved` list and stays in the file. This rule is the whole reason the skill
is safe to run.

A rewording — an overlong or unclear item restated in fewer or plainer words —
needs no evidence, because it must not change what the item says. Label it as
a rewording so it is reviewed as one. In `Direction.md`, where a slight shift in
meaning moves the baseline, leave an item alone when in doubt.

## Never

1. Never touch `## Topic`, `## Goal`, or `Glossary.md` — and `## Conventions`
   only for an item the user names.
2. Never change anything before the proposal is written and approved.
3. Never propose a removal or update you could not evidence.

## Procedure

### Phase 1 — survey and propose

1. **Read the targets in full** — `Direction.md` and `Memory.md`.
2. **Gather evidence.** Read `notes/`, `experiments/` (their `## Results` and
   `## Problems` especially), `references/`, the recent `journal/` reports, and
   `proposals/` plus `archived/` — those last two are where supersession is
   recorded.
3. **Classify every item** as one of:
   - `keep` — still live as written.
   - `remove` — finished; verdict + evidence.
   - `update` — part of it is finished or has changed; verdict + evidence, and
     the line as it will read.
   - `reword` — still live, but clearly overlong or unclear; the line as it will
     read, meaning unchanged.
   - `unresolved` — looks finished, but cannot be evidenced.
4. **Check the blast radius.** Before proposing any change to a `Direction.md`
   line, check whether a `Glossary.md` entry names it as its definition, and
   whether live notes lean on it. If the change would break them, drop it from
   the slate and say why.
5. **Write one proposal** covering the whole run (template below), present it in
   chat, and **stop**. Nothing is edited in this phase.

### Phase 2 — execute on approval

6. **Apply the concrete edit** exactly as written, and nothing more.
7. **Sweep the `## Working Context` items** listed as direct-apply. They needed
   no approval, but they are in the proposal anyway so that one file records
   everything this run changed.
8. **Move the proposal to `archived/`**, keeping its filename. It is now the
   record of what changed in the master files and why.
9. **Report.** What changed in each file, where the record lives, and the
   `unresolved` list for the user to rule on.

## Proposal note template

`## Concrete edit` quotes every removed passage **verbatim**, and every updated
or reworded line both before and after. That is deliberate — once archived, this
proposal *is* the record, so it has to carry the full text rather than a line
reference.

```markdown
---
id: prop-NNNN
created: YYYY-MM-DD
tags: [proposal, prune]
source: "prune-master-files YYYY-MM-DD"
related: ["[[evidence-note]]"]
---

## Proposed change
<!-- What leaves or changes in which files, in one or two sentences. -->

## Target
`Direction.md`, `Memory.md`

## Concrete edit

### Direction.md — ## Confirmed decisions
> <the removed line, verbatim>

- **Verdict** — superseded
- **Evidence** — [[note-or-proposal]]; one line on how it replaced this.

### Memory.md — ## Open Questions
> <the removed question, verbatim>

- **Verdict** — resolved
- **Evidence** — [[exp-NNNN-...]] `## Results`; one line on what answered it.

### Memory.md — ## Open Questions (updated, not removed)
> **Before** — <the item as it stands, verbatim>
>
> **After** — <the item with only the evidenced part changed>

- **Verdict** — resolved in part
- **Evidence** — [[exp-NNNN-...]] `## Results`; what it settled, and where any
  new wording comes from.

### Memory.md — ## Working Context (applied directly, no approval needed)
> <the removed item, verbatim>

- **Verdict** — expired; what changed.

### Direction.md — ## Scope (reworded, meaning unchanged)
> **Before** — <the item as it stands, verbatim>
>
> **After** — <the same meaning, in fewer or plainer words>

- **Why** — what made it overlong or unclear.

## Unresolved — needs your call
<!-- Items that look finished but could not be evidenced. Quote each, and say
     what would settle it. These stay in the files untouched. -->

## Status
Pending review.
```

If nothing is provably finished, say so plainly instead of manufacturing a
slate. "Both files are carrying their weight; here are two items I could not
settle either way" is a useful outcome.
