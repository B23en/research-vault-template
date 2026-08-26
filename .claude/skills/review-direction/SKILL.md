---
name: review-direction
description: Step back from individual notes and review the research at the meta level — propose new contribution candidates and revisions to the research direction. Use this skill when the user asks to review the direction, step back, look at the big picture, find new contributions, reconsider the goal or scope, or asks where the research is heading. It is invoked manually only. It surveys the whole vault and files its suggestions as proposals.
---

# review-direction

## Purpose

The other skills work note by note. This skill works at the level of the whole
research arc. It answers two meta questions:

- **New contribution candidates** — given everything accumulated so far, what
  novel contribution could this research make to its field?
- **Direction revision** — do the accumulated findings suggest the goal or scope
  in `Direction.md` should change: narrow, widen, or shift?

It is **manual-only by design**. Direction-level review is valuable occasionally,
not constantly — running it too often would just produce noise, so it is
triggered only when the user wants it.

## When to use

- The user asks for a direction review, a big-picture check, a look at new
  contributions, or a reconsideration of the goal/scope.
- Manual invocation only.

## Procedure

1. **Survey the whole vault.** Read `Direction.md`, then skim `notes/`,
   `references/`, `experiments/`, and the recent `journal/` reports. Look for patterns: recurring themes, clusters of related
   notes, dead ends, surprising results, gaps.
2. **New contribution candidates.** Identify what novel contribution the
   accumulated work points toward. Be concrete — not "this could be useful" but
   "given X, Y, and Z, this research could contribute <specific claim or
   artifact>." Propose one, at most two.
3. **Direction revision.** Judge whether the goal and scope in `Direction.md`
   still fit the accumulated evidence. If they do, say so explicitly — "no
   revision needed" is a valid and useful outcome. If they do not, describe the
   specific revision and what evidence drives it.
4. **File proposals.** Both outputs reframe the research, so they are *changes*,
   not additions — write them as `proposals/prop-NNNN-...` notes (template
   below), never apply them directly. `Direction.md` is the verification
   baseline and changes only through an approved proposal. If the conclusion is
   "no revision needed", do not file an empty proposal — just report it.
5. **Report to the user.** Summarise what you proposed and the patterns behind
   it, and end with a question.

## Proposal note template

```markdown
---
id: prop-NNNN
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [proposal, direction]
source: "review-direction YYYY-MM-DD"
related: ["[[supporting-note]]"]
---

## Proposed change
<!-- The new contribution candidate, or the direction revision, in 1–2 sentences. -->

## Target
<!-- Which file(s) this touches, as [[wiki-links]] — usually Direction.md. -->

## Rationale
<!-- The patterns observed across the vault that drive this; [[link]] the supporting notes. -->

## Concrete edit
<!-- The exact edit to apply to Direction.md on approval. -->

## Status
Pending review.
```

The user reviews proposals in conversation. On approval, apply the concrete edit
and move the proposal note to `archived/`.
