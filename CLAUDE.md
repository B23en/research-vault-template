# Research Vault — Agent Instructions

## What this agent is

This is **Research Vault** — a knowledge repository for a **single research
topic**. The agent records, verifies, and expands the research exploration
process: idea fragments, synthesized ideas, approaches, supporting evidence,
experiments, problems, and the refinement that connects them.

The agent's behavior is defined by this file (always-on guidance) and by six
working skills plus a general-purpose `grill-me` skill in `.claude/skills/`
(invokable procedures). Read the relevant skill's `SKILL.md` before performing
its task.

**Agent entry points.** This file is the authoritative configuration, and Claude
Code loads it automatically. Agents that read `AGENTS.md` instead — Codex and
others following that convention — are sent here by the root `AGENTS.md`, which
is a pointer only and carries no rules of its own, so there is never a second
copy of these rules to keep in sync. Whichever agent is running, this file plus
the skills in `.claude/skills/` define the behavior.

## Vault structure (canonical definition)

This section documents the canonical vault layout — the template repository
embodies it, and the `init-vault` bootstrapper verifies a freshly created vault
against it. Keep it accurate.

Folders — note files live here, and **a note's folder is its lifecycle stage**:

- `inbox/` — raw fragments: small ideas, stray information, snippets. Unprocessed material.
- `ideas/` — small ideas synthesized from one or more `inbox/` fragments.
- `approaches/` — approaches and strategies for tackling the research, built on ideas.
- `references/` — evidence and prior work supporting approaches, gathered by active web search.
- `experiments/` — experiment setups, settings, and their results.
- `problems/` — problems encountered during experiments: concrete obstacles
  tied to a specific experiment and linked to it, not the abstract unresolved
  questions tracked in `Memory.md` `## Open Questions`.
- `proposals/` — the agent's change-proposals awaiting human approval.
- `archived/` — discarded or superseded notes (original filenames kept).
- `journal/` — daily and verification reports (append-only history).
- `outputs/` — generated deliverables the user explicitly asked for: progress summaries, visualizations, HTML exports, and the like. Not part of the note pipeline.
- `workspace/` — experiment work area: code, fetch scripts, and the datasets
  experiments run on. Not part of the note pipeline. Large data is not
  git-tracked; code, fetch scripts, and the `datasets.md` registry are. Datasets
  are shared — one copy serves many experiments. See `## Workspace` below.

Master files at the vault root:

- `CLAUDE.md` — this file. Agent configuration and vault rules.
- `AGENTS.md` — entry point for agents that read `AGENTS.md` rather than
  `CLAUDE.md` (Codex, and other tools following that convention). It holds no
  rules of its own: it points at this file and requires that it be read first.
- `Direction.md` — the overall research direction and confirmed decisions. This
  is the **verification baseline**: everything in it is treated as decided.
- `Memory.md` — three sections. `## Conventions` holds standing rules that
  apply across the vault (e.g. authoring language). `## Open Questions` holds
  long-term unresolved questions — abstract uncertainties about the research,
  distinct from the concrete experiment-tied failures recorded as notes in
  `problems/`. `## Working Context` holds short-term context the agent
  maintains in real time.
- `Glossary.md` — canonical registry of project-coined codes and abbreviations
  (experiment-variant codes, contribution labels, hypothesis IDs, route/option
  letters, custom metric names). A descriptive index, not a decision baseline:
  it records what each code means and links to where it is defined. General
  domain terms and model names do not belong here.

## Note naming

Every note filename follows `<prefix>-<NNNN>-<short-title>.md`, where `NNNN` is a
zero-padded 4-digit counter that is **independent per folder**.

| Folder | Prefix | Example |
|--------|--------|---------|
| `inbox/` | `inbox-` | `inbox-0007-gpu-memory-trick.md` |
| `ideas/` | `idea-` | `idea-0003-adaptive-batching.md` |
| `approaches/` | `approach-` | `approach-0002-curriculum-schedule.md` |
| `references/` | `ref-` | `ref-0011-vaswani-2017.md` |
| `experiments/` | `exp-` | `exp-0005-batch-ablation.md` |
| `problems/` | `prob-` | `prob-0004-oom-on-long-seq.md` |
| `proposals/` | `prop-` | `prop-0009-revise-scope.md` |

To get the next number for a folder, list it, find the highest existing `NNNN`,
and add 1. `journal/` does not use this scheme — its files are
`YYYY-MM-DD-daily.md` and `YYYY-MM-DD-verify.md`. `archived/` keeps each note's
original filename so links to it still resolve. `outputs/` files are named
descriptively for what they are (e.g. `2026-05-23-progress-summary.md`,
`idea-graph.html`) — no prefix, no counter. `workspace/` likewise uses no prefix
or counter — `code/` is organized as the work requires, and `datasets.md` is a
single registry file.

Short titles are lowercase, hyphen-separated, 2–5 words, English.

## Frontmatter

Every note starts with YAML frontmatter:

```yaml
---
id: idea-0003
created: 2026-05-23
updated: 2026-05-23
tags: [batching, efficiency]
source: "conversation 2026-05-23; synthesized from inbox-0007, inbox-0009"
related: ["[[inbox-0007-gpu-memory-trick]]", "[[approach-0002-curriculum-schedule]]"]
---
```

- `id` matches the filename's prefix and number.
- `created` / `updated` are ISO dates (`updated` changes on every edit).
- `source` records where the note came from — which fragments, which
  conversation, which reference.
- `related` lists Obsidian wiki-links to connected notes — see the Linking
  section below.

Experiment notes additionally carry `approach: "[[approach-NNNN-...]]"`, and —
when they use the workspace — `datasets:` (wiki-links to entries in
`workspace/datasets.md`, e.g. `["[[datasets#imagenet-1k]]"]`) and `code:` (the
path to their code under `workspace/code/`).

## Linking

Links are what make the vault a connected graph instead of a pile of files, and
they are how verification traces a claim back to its source. Use Obsidian
wiki-links — `[[note-filename-without-extension]]` — in two places:

- **In note bodies.** Whenever a note's prose refers to another note — an idea
  it builds on, a reference it cites, an approach it serves — write that mention
  as a `[[wiki-link]]`, not as plain text. A cross-reference you can click is
  worth far more than one a reader has to go search for.
- **In frontmatter `related`.** Mirror every wiki-link used in the body into the
  `related` field, so the connection shows up in the note's metadata and in
  Obsidian's graph and backlink panels.

Link by filename stem, e.g. `[[idea-0003-adaptive-batching]]`. Because promotion
creates new notes instead of renaming, and `archived/` keeps original filenames,
these links stay valid for the life of the vault.

## Glossary

`Glossary.md` at the vault root is the canonical registry of **project-coined
codes** — the local symbols the research invents (experiment-variant codes like
`B1`, contribution labels like `C1`, hypothesis IDs, route/option letters,
custom metric or parameter names). Its purpose is traceability: a code stays
readable months later instead of forcing a hunt through old notes.

- **Scope.** Only symbols this project coins. General domain terms and
  model/method names belong in `Memory.md` `## Conventions` or are external — not
  here.
- **Format.** One entry per code: the symbol, a one-line definition, and a
  `[[wiki-link]]` to the note where it is authoritatively defined. Codes are
  grouped into category sections so the same letter in two different families
  does not collide; a genuinely overloaded symbol is marked and disambiguated.
- **Authority.** The Glossary is a descriptive index, not a baseline —
  `Direction.md` stays ground truth. Defining a new code is additive (write it
  directly). Redefining an existing code is a *change* and goes through
  `proposals/`, because downstream notes and filenames depend on the old meaning.
- **Upkeep.** `verify-consistency` flags codes used in notes but missing from
  the Glossary, used in a way that conflicts with their entry, or Glossary
  entries whose defining note has been archived or removed.

## Workspace (experiment code, datasets & run outputs)

`workspace/` is the agent's experiment work area — where a Claude Code session
downloads datasets, runs experiment code, and writes run outputs. Like
`outputs/`, it sits **outside the note pipeline**: no frontmatter, no naming
counter, and verification leaves its data and run outputs alone.

- `workspace/code/` — experiment code and fetch scripts. **Git-tracked.**
- `workspace/data/` — input datasets, downloaded here at run time. Shared across
  experiments. **Not git-tracked** (only `.gitkeep` is); large and often
  redistribution-restricted, so they never enter history.
- `workspace/runs/` — run outputs: checkpoints, logs, metrics. Organized
  **per-experiment** (`runs/<exp-id>/`). **Not git-tracked** — large binaries
  that belong to a single run.
- `workspace/datasets.md` — the dataset registry. **Git-tracked.**

Rules:

- **Reproducibility lives in git, the bytes do not.** A fresh clone has empty
  `workspace/data/` and `workspace/runs/`. What git holds is the *recipe* — the
  fetch scripts, the experiment code, the registry, and pointers — never the
  heavy bytes. The canonical form of "where this came from" is an executable
  fetch script, not just a URL.
- **Datasets are shared; run outputs are per-experiment.** One dataset copy
  serves many experiments — each registry entry pins a **version and checksum**;
  a different version or preprocessing is a **separate entry**, so sharing never
  silently breaks reproducibility. Checkpoints and logs instead belong to the
  single run that produced them, under `runs/<exp-id>/`.
- **Checkpoint preservation — two policies.**
  - **(A) Regenerate by default.** Mid-training / throwaway checkpoints are not
    preserved: they stay local and git-ignored, and the note records only the
    recipe (config, seed, code commit) so the run can be re-done. Use when
    re-running is cheap.
  - **(B) Preserve precious checkpoints to Hugging Face Hub.** A final/best
    checkpoint that is expensive or impossible to reproduce is uploaded to an HF
    **model repo**, and only a *pointer* is kept in the vault — the experiment
    note's `## Results` records the **repo id**, the **revision (commit hash)**,
    a **sha256**, the **download command**, and the local path under
    `runs/<exp-id>/`. Use when losing the file costs more than a quick re-run.
  - Rule of thumb: recovery > ~1 hour (or irreproducible) → (B); else (A). A
    typical experiment uses both.
- **Secrets never enter git.** The Hugging Face token is read from the
  `HF_TOKEN` environment variable — never written into a note, script, or commit.
- **Scope.** Only experiment code, the data it runs on, and the outputs it
  produces — not a scratch drawer.
- Experiment notes link the datasets and code they use via frontmatter (below);
  preserved (B) checkpoints are recorded in the note's `## Results`.

## Lifecycle: folders are stages

There is no `status` field. A note's **folder** is its stage. Moving up the
pipeline is never a rename or a file move — it is the creation of a **new note**
at the higher stage that links its source notes:

```
inbox fragments  --synthesize-->  an ideas/ note
ideas            --develop----->  an approaches/ note
approaches       --specify----->  an experiments/ note  (+ references/ notes)
```

Source notes stay where they are — they are the raw material. A note that is
discarded or superseded is moved to `archived/`, keeping its filename. Because
promotion creates new notes rather than renaming, wiki-links never break.

## Operating principles

**Additive is automatic; changes are proposed.** Creating a new note is additive
and low-risk — do it directly. Modifying `Direction.md`, editing or archiving an
existing note, or any non-additive change is a *change*: do not do it silently.
Write a proposal note in `proposals/` describing what to change, which file(s),
the rationale, and the concrete edit. The human reviews proposals in
conversation; on approval you apply the change and move the proposal note to
`archived/`. `Direction.md` is the verification baseline — if it is corrupted,
every future consistency check is wrong, which is why it is never edited without
an approved proposal.

**Adaptive always-on behaviors.** When the conversation is about the research
itself — ideas, approaches, experiments, problems — apply three behaviors:
critically analyze (surface weaknesses, hidden assumptions, feasibility concerns
rather than only affirming), expand (offer adjacent branches, variants,
alternatives), and end with a question that pushes the research forward. Do not
apply these to simple factual lookups, questions about how this system works, or
casual exchange — there they are just noise.

**Memory.md in real time.** When something is worth remembering temporarily — a
decision in progress, a thread to pick up later, session context — record it
under `## Working Context` in `Memory.md` as you go. When an item becomes
invalid or is promoted into a permanent note, remove it immediately. The
`## Open Questions` section is long-term; do not auto-prune it.
`## Conventions` section holds standing rules (authoring language, formatting
norms, naming overrides); add to it only on explicit user instruction and
never auto-prune it.

**Promotion is conversational.** Moving the research forward a stage happens with
the user. When material looks ready, propose it adaptively ("Shall I synthesize
these fragments into an idea note?") rather than acting unprompted.

**Capture.** Save a fragment to `inbox/` immediately on explicit request. When a
meaningful fragment surfaces on its own, offer to capture it rather than
capturing silently — this keeps `inbox/` from flooding.

**Evidence.** Ground claims about feasibility and prior work. Use active web
search to find prior work, and record it as `references/` notes.

**User-requested deliverables.** When the user explicitly asks for a generated
artifact — a progress summary, a visualization, an HTML export, a converted
document — save it in `outputs/` with a descriptive filename. These are derived
presentation artifacts, not research notes: they carry no frontmatter, follow no
naming counter, and the verification procedure leaves them alone. Only write to `outputs/` on an explicit request; research content belongs
in the pipeline folders, not here.

**Git.** The whole vault is version-controlled with git. Commit at your own
discretion once you have completed a meaningful unit of work — a captured
fragment, an approved promotion batch, an applied proposal — using a short,
descriptive message (e.g. `capture: gpu-memory-trick`, `promote: 3 inbox -> ideas`,
`apply prop-0009: revise scope`). Two rules bound the discretion: commit only
complete, consistent states — never a half-finished change or an unapproved
modification — and commit locally only; do not push unless the user asks.

## Skills

Skills are this vault's procedures. Each lives at
`.claude/skills/<skill-name>/SKILL.md`, with YAML frontmatter naming it and
describing when it applies. The directory name is historical — it is where the
skills live regardless of which agent is running.

**Dispatch rule.** When a request matches a skill's `description`, read that
`SKILL.md` and follow its workflow in full before implementing anything
yourself — the whole procedure, never an abbreviated version. When no request
matches, proceed normally; do not open a `SKILL.md` just in case, since reading
one costs context. Skills that write to the vault still obey the operating
principles above: additive actions are direct, changes go through `proposals/`.

Six working skills live in this vault's `.claude/skills/`:

- `capture-idea` — save a discussed fragment to `inbox/`.
- `promote-notes` — explicit, batched promotion from `inbox/` to `ideas/` and
  from `ideas/` to `approaches/`; presents a candidate slate for approval before
  writing anything.
- `verify-consistency` — audit live notes against `Direction.md` and report
  conflicts, ambiguity, duplication, orphans, broken links, and stale/dangling
  references.
- `specify-methodology` — turn an approach into an experiment design backed by
  web-researched evidence.
- `explain-direction` — read-only: explain `Direction.md` in plain language,
  element by element, plus an overall summary. Proposes no changes.
- `review-direction` — manual meta-review: new-contribution candidates and
  direction revisions.

One general-purpose skill also ships in `.claude/skills/`, outside the note
pipeline:

- `grill-me` — interview the user relentlessly about a plan or design,
  resolving each branch of the decision tree, to stress-test a research
  direction, approach, or experiment before committing to it.

`init-vault` is **not** in the vault. It is installed globally
(`~/.claude/skills/`) and bootstraps a new vault by fetching this whole
environment — this file, the skills above, and the master-file templates —
from the template repository. Because these skills are fetched from that
repository, improving one means editing it once there; new vaults then pick up
the latest version.
