# Glossary

> Canonical registry of **project-coined codes and abbreviations** — the local
> symbol namespace this research invents as it goes (experiment-variant codes,
> contribution labels, hypothesis IDs, option/route letters, custom metric or
> parameter names). It exists so a code like `B1` or `θ-002` stays traceable
> instead of turning unreadable months later.
>
> **Scope.** Only symbols *this project* coins. General domain terms and
> model/method names (VLM, SAM, …) do **not** go here — those live in
> `Memory.md` `## Conventions` or are external vocabulary. If a reader could look
> a term up in a textbook, leave it out.
>
> **Authoring language** follows the vault's `## Conventions`; code symbols keep
> their original form. No frontmatter, no naming counter — a master file like
> `Direction.md` and `Memory.md`.

## How to use this file

- **One entry per code:** the symbol, a one-line definition/expansion, and a
  `[[wiki-link]]` to the note where it is authoritatively defined or first used.
- **Group by family.** Put each code under a category section (examples below).
  This is what prevents collisions — the same letter can safely appear in two
  families as long as each lives in its own section and the entry names the family.
- **Overloaded symbols:** if one symbol genuinely carries two meanings, mark it
  ⚠️ and spell out how context disambiguates. Prefer renaming one of them.

## Authority

This file is a **descriptive index, not a decision baseline** — `Direction.md`
stays the single source of truth. The Glossary only records what a code *means*
and points to where it is decided.

- **Adding a new code is additive** — write the entry directly.
- **Changing the meaning of an existing code is a *change*** — file a proposal in
  `proposals/`, because downstream notes, filenames, and results depend on the
  old meaning. Never silently redefine a code.

---

<!-- Replace the example sections below with this project's actual code families.
     These categories are illustrative, not mandatory. -->

## Experiment / config variants

<!-- Codes for experiment runs and their settings. Example:
     - **B1** — RemoteCLIP-ViT-L/14, SimFeatUp off. Operational default. [[exp-0002-...]]
     - **β (beta)** — GeoRSCLIP-ViT-B/32 + SimFeatUp. Lowest spillover. [[exp-0002-...]] -->

## Contributions

<!-- Codes for the paper's claimed contributions. Example:
     - **C1** — the editable object-region representation. [[approach-0001-...]] -->

## Hypotheses

<!-- Codes for stated hypotheses. Example:
     - **H1** — node label quality matches human judgement. [[exp-0002-...]] -->

## Risks / open-question codes

<!-- Codes labelling risks or open questions. Watch for collisions with other
     families — disambiguate explicitly. Example:
     - **R1 (Q)** — feature-vs-research framing risk. cf. R1 under Routing. [[Memory]] -->

## Routes / options

<!-- Letter codes for decision branches or solution options. Example:
     - **(가) route** — image excluded from VLM input. [[Direction]] -->
