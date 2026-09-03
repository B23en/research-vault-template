# Research Direction

> This file is the **verification baseline** — the fixed point every consistency
> check is measured against. The agent never edits it without an approved
> proposal in `proposals/`. Keep it concise — it is ground truth, not a
> scratchpad.
>
> **Two tiers.** Sections carry different confidence, and each one says which it
> is. **Settled** sections hold what evidence cannot overturn — either the line
> is not the kind of claim an experiment can refute, or changing it would
> invalidate work already done. **Working** sections hold the current best
> direction, which accumulated evidence may yet push on. (Unrelated to
> `Memory.md` `## Working Context`, which is short-term session state.)
>
> **The tier does not change how this file is edited.** Both tiers require an
> approved proposal — a Working section is not the agent's to rewrite. The tier
> changes one thing only: **when a note and this file disagree, which one is
> presumed wrong.** Against a Settled line the note is; against a Working line
> the baseline may be, and the agent may say so. Either way the human decides,
> and questioning a Settled line is always open to the human.

## Topic

**Tier: Working** — written before any evidence exists.

<!-- One or two sentences: what is this research about? -->

## Goal

**Tier: Working** — evidence may shift what success means.

<!-- What does success look like? What question is the research trying to answer? -->

## Confirmed decisions

**Tier: Settled** — changing one of these invalidates work already done.

<!-- Settled decisions, each a short checkable statement. Examples:
     - The target model family is decoder-only transformers.
     - Evaluation uses held-out perplexity, not downstream task accuracy. -->

## Scope

**Tier: Working** — boundaries move without invalidating past work.

In scope:

<!-- - ... -->

Out of scope:

<!-- - ... -->

## Constraints

**Tier: Settled** — external facts, not claims an experiment can refute.

<!-- Resource, time, data, or tooling limits that bound the work. -->
