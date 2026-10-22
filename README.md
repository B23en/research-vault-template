# Research Vault Template

[![Built for Codex](https://img.shields.io/badge/Built%20for-Codex-1a1a1a)](https://developers.openai.com/codex)
[![AGENTS.md compatible](https://img.shields.io/badge/AGENTS.md-compatible-1a1a1a)](https://agents.md)

Template for a single-topic research knowledge vault — an Obsidian vault paired
with an AI agent that records, verifies, and expands a research exploration
process (notes, evidence, experiments and their results).

> **Designed for Codex, compatible with Claude Code.** `AGENTS.md` provides the
> shared agent instructions and `.agents/skills/` holds the canonical skills.
> `CLAUDE.md` imports `AGENTS.md`, and `.claude/skills` links to the same skill
> files. Rules and skills each have one source of truth. Outside an agent
> environment, the files are just Markdown.

## Using this template

Give your agent this repository URL and a target folder, and ask it to read
this README and `AGENTS.md` before setting up or updating the vault. No global
setup skill is required.

### Create a vault

1. Inspect the target folder and any existing Git repository. Fetch this
   template into a temporary folder, then copy its master files, skills,
   `.gitignore`, and content folders into the target, preserving symlinks.
   Leave the template's `.git` and this setup README behind. In an existing
   project, preserve its files, Git history, and remotes; review conflicting
   files before merging them.
2. Verify the structure against `AGENTS.md`: `.agents/skills/` must be a real
   directory and `.claude/skills` must link to `../.agents/skills`. Check that
   `CLAUDE.md` imports `AGENTS.md` and every listed skill is readable. When
   copying files individually or using Git without symlink support, recreate
   the link in a filesystem that supports symlinks.
3. For a new standalone vault, initialize its own Git history on `main` and
   commit the scaffold. Connect and push to a separate research repository
   only when requested; never use the template's remote as the vault's remote.
4. Fill in `Direction.md` with the agreed research topic and scope.

### Update a vault

1. Fetch the latest template into a temporary folder and compare its
   `AGENTS.md`, `CLAUDE.md`, `.agents/skills/`, and `.gitignore` with the vault.
   Present the proposed changes before applying them.
2. For an older Claude-first vault, migrate its layout before applying the
   approved template updates. Merge its authoritative `CLAUDE.md` rules into
   `AGENTS.md`, preserving local instructions from both files. Remove only
   the old `.agents/skills` symlink, move the actual skills into
   `.agents/skills/`, then create `.claude/skills` as a link to
   `../.agents/skills`. Update skill references and turn `CLAUDE.md` into the
   import file.
3. Merge approved template changes while preserving local rules, custom
   skills, and ignore patterns. Keep `Direction.md`, `Memory.md`, `Glossary.md`,
   research notes, and workspace contents intact. Add missing structural files
   or folders only when absent; do not replace existing content with templates.
4. Verify the resulting structure, skill links, and diff before committing;
   push only when requested.

## Layout

| Path | Purpose |
|------|---------|
| `AGENTS.md` | Authoritative agent configuration and vault rules |
| `CLAUDE.md` | Imports `AGENTS.md` for Claude Code compatibility |
| `Direction.md` | Research direction — the verification baseline |
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
| `.agents/skills/` | Canonical working skills + general-purpose `grill-me` |
| `.claude/skills` | Symlink to `../.agents/skills` for Claude Code compatibility |

## Skills

Working skills: `capture-idea`, `promote-notes`, `verify-consistency`,
`specify-methodology`, `prune-master-files`, `review-direction`. Plus a
general-purpose `grill-me` skill for stress-testing a plan or design.

Skills are not slash commands you have to remember. Each one's `description` is
what the agent routes on, so it offers the right skill when the conversation
reaches the moment that skill covers — you can just talk. `review-direction` is
the exception — it is offered only after an audit has found a conflict with
`Direction.md`, and stays explicit-only otherwise.
