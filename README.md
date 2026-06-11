# Research Vault Template

[![Built for Claude](https://img.shields.io/badge/Built%20for-Claude-D97757?logo=anthropic&logoColor=white)](https://claude.com)

Template for a single-topic research knowledge vault — an Obsidian vault paired
with a Claude agent that records, verifies, and expands a research exploration
process (ideas, approaches, evidence, experiments, problems).

> **Designed for Claude.** The agent runs on Claude (via Claude Code or Cowork):
> `CLAUDE.md` provides its always-on instructions and `.claude/skills/` holds the
> skills it invokes. Outside a Claude environment, the files are just Markdown.

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
| `Direction.md` | Research direction — the verification baseline |
| `Memory.md` | Open questions + working context |
| `Glossary.md` | Registry of project-coined codes and abbreviations |
| `inbox/` | Raw fragments |
| `ideas/` | Synthesized ideas |
| `approaches/` | Approaches built on ideas |
| `references/` | Evidence, gathered by web search |
| `experiments/` | Experiment setups and results |
| `problems/` | Problems found during experiments |
| `proposals/` | Agent change-proposals awaiting review |
| `archived/` | Discarded notes |
| `journal/` | Daily and verification reports |
| `outputs/` | User-requested generated deliverables (summaries, visualizations, HTML) |
| `.claude/skills/` | Six working skills + general-purpose `grill-me` |

## Skills

Six working pipeline skills: `capture-idea`, `promote-notes`,
`verify-consistency`, `specify-methodology`, `daily-routine`,
`review-direction`. Plus a general-purpose `grill-me` skill for stress-testing
a plan or design. (`init-vault` is installed globally, not in the vault.)

## After creating a vault

Fill in `Direction.md` with the research topic, then set up a daily scheduled
task (07:00, cron `0 7 * * *`) that runs `daily-routine`.
