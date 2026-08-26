---
name: specify-methodology
description: Turn a notes/ note into a concrete, evidence-backed experiment design. Use this skill whenever the user wants to work out a methodology, design an experiment, figure out how to actually test or implement an approach, or asks for a concrete experimental plan or setup. It actively web-searches for prior work and evidence, records what it finds as reference notes, and produces an experiment note with a hypothesis, variables, measurements, baselines, and risks.
---

# specify-methodology

## Purpose

A `notes/` note says *what to try*. An experiment note says *how, concretely,
and on what evidence*. This skill bridges the two. Its defining feature is that the
design is **grounded** — it actively searches for prior work rather than relying
on guesswork, so the methodology stands on real evidence.

## When to use

- The user points at a note and wants it made concrete and testable.

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
   or reuse an entry in `workspace/datasets.md` (source, version, checksum,
   license, fetch command) and stub a fetch script in `workspace/code/` so the
   data rebuilds from a clean clone. This is additive — do it directly, no
   proposal. Run outputs (checkpoints, logs, metrics) land in
   `workspace/runs/<exp-id>/`, which is git-ignored; once a run produces a
   checkpoint worth keeping, preserve it per policy (B) (Hugging Face Hub) and
   record the pointer in the note's `## Results`.
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

## Reference note template

```markdown
---
id: ref-NNNN
created: YYYY-MM-DD
updated: YYYY-MM-DD
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
updated: YYYY-MM-DD
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
