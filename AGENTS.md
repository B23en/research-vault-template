# AGENTS.md

**Read `./CLAUDE.md` in full before doing anything else in this repository.**

This repository is a Research Vault — a knowledge repository for a single
research topic, operated by an agent. `CLAUDE.md` is the authoritative
configuration: vault structure, note naming, frontmatter, linking rules,
lifecycle stages, and the operating principles that decide what you may do
directly versus what must go through a proposal.

This file deliberately contains **no rules of its own**. Duplicating them here
would create a second source of truth that drifts out of sync. It exists only
because Codex and other `AGENTS.md`-reading agents do not load `CLAUDE.md` on
their own.

## Required first step

1. Read `./CLAUDE.md` end to end.
2. Read `./Direction.md` — the research direction, and the baseline that every
   consistency check is measured against. It holds the current direction, and
   changes only through an approved proposal.
3. Read `./Memory.md` `## Conventions` — standing rules for this vault,
   including the language notes are written in.

Until you have done this you do not know this vault's rules: do not create,
edit, move, or archive any file.

## Skills

This vault's procedures live in `.claude/skills/<skill-name>/SKILL.md`. The
directory name is historical — it is where the skills live regardless of which
agent is running. `CLAUDE.md` `## Skills` lists them, says what each one is for,
and states the dispatch rule: when a request matches a skill's `description`,
read that `SKILL.md` and follow its workflow in full before implementing
anything yourself.

## If you are Claude Code

You already loaded `CLAUDE.md` automatically. Ignore this file.
