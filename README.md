# Research Vault Template

[![Built for Claude](https://img.shields.io/badge/Built%20for-Claude-D97757?logo=anthropic&logoColor=white)](https://claude.com)
[![AGENTS.md compatible](https://img.shields.io/badge/AGENTS.md-compatible-1a1a1a)](https://agents.md)

Template for a single-topic research knowledge vault — an Obsidian vault paired
with an AI agent that records, verifies, and expands a research exploration
process (notes, evidence, experiments and their results).

> **Designed for Claude, portable to other agents.** The agent runs best on
> Claude (via Claude Code or Cowork): `CLAUDE.md` provides its always-on
> instructions and `.claude/skills/` holds the skills it invokes. Agents that
> follow the `AGENTS.md` convention — Codex among them — read the root
> `AGENTS.md`, a pointer that sends them to `CLAUDE.md`. It duplicates no rules,
> so there is only ever one source of truth. Outside an agent environment, the
> files are just Markdown.

## Using this template

This repository is the canonical source for the research-agent system. You do
not build a vault by hand — the `init-vault` skill clones this repo.

1. Install `init-vault` globally at `~/.claude/skills/init-vault/`.
2. In `init-vault/SKILL.md`, set `DEFAULT_TEMPLATE_REPO` to this repo's URL.
3. Run `init-vault` in any project folder. It clones this template there as a
   fresh vault and initialises the vault's own git history.

To update an existing vault's skills later, run `init-vault` in update mode — it
refreshes `.claude/skills/` from this repo without touching vault content.

## Layout

| Path | Purpose |
|------|---------|
| `CLAUDE.md` | Agent configuration and vault rules |
| `AGENTS.md` | Pointer sending `AGENTS.md`-reading agents (Codex, …) to `CLAUDE.md` |
| `Direction.md` | Research direction — the verification baseline, tiered Settled / Working |
| `Memory.md` | Conventions + open questions + working context |
| `Glossary.md` | Registry of project-coined codes and abbreviations |
| `inbox/` | Raw fragments |
| `notes/` | Worked-out thinking: ideas, discussion, writing |
| `references/` | Evidence, gathered by web search |
| `experiments/` | Experiment setups, results, and problems hit |
| `proposals/` | Agent change-proposals awaiting review |
| `archived/` | Discarded notes and applied proposals — including the only copy of pruned master-file content |
| `journal/` | Append-only record — verification reports, commissioned run reports |
| `outputs/` | User-requested generated deliverables (summaries, visualizations, HTML) |
| `workspace/` | Experiment code, fetch scripts, (git-ignored) datasets, and run outputs/checkpoints |
| `.claude/skills/` | Working skills + general-purpose `grill-me` |
| `.agents/skills` | Symlink to `.claude/skills/`, so Codex discovers the same files |

## Skills

Working skills: `capture-idea`, `promote-notes`, `verify-consistency`,
`specify-methodology`, `prune-master-files`, `review-direction`. Plus a
general-purpose `grill-me` skill for stress-testing a plan or design.
(`init-vault` is installed globally, not in the vault.)

Skills are not slash commands you have to remember. Each one's `description` is
what the agent routes on, so it offers the right skill when the conversation
reaches the moment that skill covers — you can just talk. `review-direction` is
the exception — it is offered only when concrete evidence says the direction may
have gone stale, and stays explicit-only otherwise.

## After creating a vault

Fill in `Direction.md` with the research topic.
