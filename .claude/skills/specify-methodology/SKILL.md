---
name: specify-methodology
description: Turns a notes/ note into a concrete, evidence-backed experiment design. Use whenever the user wants to work out a methodology, design an experiment, or figure out how to actually test an idea — including plain openers like "let's design the experiment" or "how would we test this" — and offer it proactively when a notes/ note has firmed up into something testable, when discussion turns from what to try toward how to measure it, or when the user starts asking about baselines, metrics, or setup. It actively web-searches for prior work, records it as reference notes, and produces an experiment note with hypothesis, variables, measurements, baselines, and risks.
---

# specify-methodology

## Purpose

A `notes/` note says *what to try*. An experiment note says *how, concretely,
and on what evidence*. This skill bridges the two. Its defining feature is
that the design is **grounded** — it actively searches for prior work rather
than relying on guesswork, so the methodology stands on real evidence.

## When to use

- **Explicit** — the user asks to design an experiment, work out a methodology,
  or figure out how to test something. Plain openers count — "let's design the
  experiment now", "how would we actually test this", "what's the setup?"
- **Proactive** — reach for it unasked when a `notes/` note has firmed up into
  something testable, when the discussion turns from *what to try* toward *how
  to measure it*, or when the user starts asking about baselines, metrics, or
  required resources.

Proactive means **offer in one line and wait**, not start. This skill runs web
searches and creates several notes, so it never runs unprompted.

## Input

A note in `notes/` — the worked-out idea or strategy to be tested. If the user
has not named one, ask which note to specify before proceeding.

## Procedure

1. **Read the context.** Read the source note and follow its `related` chain
   back to the fragments behind it. Read `Direction.md` so the design
   respects confirmed constraints (resources, scope, evaluation choices).
2. **Gather evidence actively.** Web-search for prior work: has something like
   this been tried? What did they measure? What baselines are standard in this
   area? What pitfalls are reported? For each genuinely useful source, create a
   reference note `references/ref-NNNN-short-title.md` (template below).
   Creating reference notes is additive — do it directly, no proposal.
3. **Draft the experiment design**, covering: a falsifiable hypothesis;
   independent and controlled variables; measurements and metrics; baselines to
   compare against; the procedure; required resources; risks and their
   mitigations; and the evidence (links to the `ref-` notes) behind each design
   choice.
4. **Register datasets and code (if any).** If the design needs a dataset, add
   or reuse an entry in `workspace/datasets.md` and stub a fetch script in
   `workspace/code/` so the data rebuilds from a clean clone. This is additive —
   do it directly, no proposal. Run outputs land in `workspace/runs/<exp-id>/`,
   which is git-ignored. `## Workspace detail` below has the rules for both.
5. **Create the experiment note** `experiments/exp-NNNN-short-title.md` (template
   below). Set the `note:` frontmatter field to the source note, list the
   `ref-` notes in `related`, and set `datasets:`/`code:` for any workspace
   artifacts it uses.
6. **Report and continue.** Tell the user the new filenames, note any open
   design questions, and end with a question (per `CLAUDE.md`).

The experiment note also holds the rest of the experiment's life, so it ships
with empty `## Results` and `## Problems` sections to fill in once the
experiment is actually run. There is no separate problems folder — obstacles
live in the experiment note that produced them.

## Workspace detail

`CLAUDE.md` `## Workspace` states the three rules that must hold in every
session. The operational detail lives here instead, where it is actually used.

**Pinning a dataset entry.** Each entry in `workspace/datasets.md` records the
source (URL or DOI), the version or fetch date, a checksum, the license, the
fetch command or script, and the local path. **A different version, or
different preprocessing, is a separate entry — never an edit to an existing
one.** One dataset copy serves many experiments, so quietly mutating an entry
breaks reproducibility for every experiment that already cited it.

**Checkpoint preservation — two policies.** A typical experiment uses both.

- **(A) Regenerate.** Mid-training and throwaway checkpoints are not preserved.
  They stay local and git-ignored, and the note records only the recipe —
  config, seed, code commit — so the run can be re-done. Use when re-running is
  cheap.
- **(B) Preserve to Hugging Face Hub.** A final or best checkpoint that is
  expensive or impossible to reproduce is uploaded to an HF **model repo**, and
  only a *pointer* is kept in the vault. The experiment note's `## Results`
  records the **repo id**, the **revision (commit hash)**, a **sha256**, the
  **download command**, and the local path under `runs/<exp-id>/`. Use when
  losing the file costs more than a quick re-run.

The upload token comes from the `HF_TOKEN` environment variable. It is never
written into a note, a script, or a commit.

## Reference note template

```markdown
---
id: ref-NNNN
created: YYYY-MM-DD
tags: [prior-work]
source: "<URL or full citation>"
related: ["[[note-NNNN-...]]"]
---

## Summary
<!-- What this source shows or claims, in 2–4 sentences. -->

## Relevance
<!-- Why it matters for the [[note]] — what it supports, warns against, or measures. -->

## Source
<!-- Full citation and URL. -->
```

## Experiment note template

```markdown
---
id: exp-NNNN
created: YYYY-MM-DD
tags: [experiment]
note: "[[note-NNNN-...]]"
datasets: ["[[datasets#...]]"]      # workspace/datasets.md entries it uses (omit if none)
code: "workspace/code/exp-NNNN-.../" # its code dir under workspace/ (omit if none)
source: "specify-methodology YYYY-MM-DD"
related: ["[[ref-NNNN-...]]"]
---

## Hypothesis
<!-- A falsifiable statement the experiment tests. -->

## Variables
<!-- Independent variables (what we change) and controlled variables (what we hold fixed). -->

## Measurements
<!-- Metrics and how they are measured. -->

## Baselines
<!-- What we compare against. -->

## Procedure
<!-- Concrete steps to run the experiment. -->

## Resources
<!-- Compute, data, time, tooling required. -->

## Risks
<!-- What could invalidate the experiment, and mitigations. -->

## Evidence
<!-- [[Wiki-link]] each ref- note, with the design choice it justifies. -->

## Results
<!-- Empty until the experiment is run. Record key metrics and what they mean.
     For any checkpoint preserved externally (policy B), record: HF repo id,
     revision (commit hash), sha256, download command, and local path under
     workspace/runs/<exp-id>/. -->

## Problems
<!-- Obstacles actually hit while running this, and cautions for anyone
     repeating it: what broke, what was confusing, what nearly invalidated a
     result, what to watch for next time. Distinct from ## Risks, which is
     written before the run and lists what *could* go wrong. Empty until there
     is something to record. -->
```
