---
name: review-direction
description: Step back from individual notes and review the research at the meta level — propose new contribution candidates and revisions to the research direction. Use this skill when the user asks to review the direction, step back, look at the big picture, find new contributions, reconsider the goal or scope, or asks where the research is heading. It is invoked explicitly, or offered only when concrete evidence — a baseline-drift finding, or an experiment result refuting a Working line in Direction.md — says the direction may have gone stale. It surveys the whole vault and files its suggestions as proposals.
---

# review-direction

## Purpose

The other skills work note by note. This skill works at the level of the whole
research arc. It answers two meta questions:

- **New contribution candidates** — given everything accumulated so far, what
  novel contribution could this research make to its field?
- **Direction revision** — do the accumulated findings suggest the goal or scope
  in `Direction.md` should change: narrow, widen, or shift?

It is **evidence-gated by design**. Direction-level review is valuable
occasionally, not constantly — running it on a hunch would just produce noise. So
the agent never raises it because the direction *feels* off. It raises it only
once something concrete has shown that a **Working** section of `Direction.md`
may be stale, and otherwise waits to be asked.

## When to use

- **Explicit** — the user asks for a direction review, a big-picture check, a
  look at new contributions, or a reconsideration of the goal/scope.
- **On evidence** — offer it, in one line, when either of these has happened:
  - a `verify-consistency` report recorded **baseline drift** — two or more
    notes, at least one an experiment result or a reference, pulling against a
    **Working** section of `Direction.md`;
  - an experiment result directly refutes a line in a Working section, plainly
    enough that no audit is needed to see it.

The two bars differ on purpose, and merging them would break both. Baseline
drift is a pattern the agent digs up while sweeping the whole vault
mechanically, where a false positive is cheap to produce and easy to believe —
so it takes several notes and real evidence. A result that refutes a Working
line in front of both of you needs no such corroboration; the context is already
plain.

Offer and wait — never start this skill unprompted, and never offer it over a
**Settled** section on your own. An offer the user declines is dropped for the
session.

## Procedure

1. **Survey the whole vault.** Read `Direction.md`, then skim `notes/`,
   `references/`, `experiments/`, and the recent `journal/` reports. Look for
   patterns: recurring themes, clusters of related notes, dead ends, surprising
   results, gaps.
2. **New contribution candidates.** Identify what novel contribution the
   accumulated work points toward. Be concrete — not "this could be useful" but
   "given X, Y, and Z, this research could contribute <specific claim or
   artifact>." Propose one, at most two.
3. **Direction revision.** Judge whether the **Working** sections of
   `Direction.md` — `## Topic`, `## Goal`, `## Scope` — still fit the
   accumulated evidence. If they do, say so explicitly — "no revision needed" is
   a valid and useful outcome. If they do not, describe the specific revision and
   what evidence drives it. A **Settled** section is in scope here only when the
   user raised it; do not reopen one on the strength of the survey alone.
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
