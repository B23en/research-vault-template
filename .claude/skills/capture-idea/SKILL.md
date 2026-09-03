---
name: capture-idea
description: Save a discussed idea fragment or piece of information into the research vault's inbox/ folder as a note. Use this skill whenever the user asks to save, capture, record, jot down, or note an idea — and proactively offer it whenever a meaningful idea fragment, insight, or useful fact surfaces during research discussion, even if the user does not say "inbox" or "note" explicitly. This is the entry point of the research pipeline; capturing fragments reliably keeps ideas from being lost.
---

# capture-idea

## Purpose

`inbox/` holds raw fragments — small ideas, stray information, snippets. It is
the unprocessed material that everything downstream (notes, experiments) is
synthesized from. The value of this skill is speed and consistency: a fragment
captured the moment it appears is a fragment that survives.

## When to use

- **Explicit** — the user says "save this", "capture that", "note this down",
  or similar. Act immediately.
- **Proactive** — a meaningful fragment surfaces on its own during research
  discussion. Offer to capture it ("Want me to drop this in `inbox/`?"). Do not
  capture silently on every utterance; `inbox/` should hold real fragments, not
  conversational noise.

Writing to `inbox/` is additive, so it needs no proposal — once the user agrees
(or asked explicitly), just create the note.

## Procedure

1. **Isolate the fragment.** Identify the specific idea, insight, or fact. If
   several distinct fragments came up, make one note each — `inbox/` notes are
   atomic.
2. **Find the next id.** List `inbox/`, find the highest `inbox-NNNN`, add 1.
   Zero-pad to 4 digits.
3. **Pick a short title.** Lowercase, hyphen-separated, 2–5 words, English.
4. **Create the note** at `inbox/inbox-NNNN-short-title.md` using the template
   below. Write the body in the language set by `Memory.md` `## Conventions`;
   the filename stays English either way.
5. **Confirm and continue.** Tell the user the filename. If the conversation is
   a research discussion, end with a question that pushes the fragment further
   (per the adaptive behavior in `CLAUDE.md`).

## Note template

```markdown
---
id: inbox-NNNN
created: YYYY-MM-DD
tags: [topic-tag]
source: "conversation YYYY-MM-DD"
related: ["[[note-0003-...]]"]
---

## Fragment

<!-- The idea in 1–3 sentences, in the user's own framing. -->

## Context

<!-- Where it came from and what prompted it. -->

## Open threads

<!-- What is unresolved, or what would need to be true for this to matter. -->
```

Keep it short. `inbox/` notes are fragments, not essays — a few sentences per
section is right. Refinement happens later when fragments are synthesized into
a `notes/` note.

## Example

**Input (in conversation):** "Oh — what if we warm up the batch size instead of
the learning rate? Could stabilize early training."

**Output:** `inbox/inbox-0012-batch-size-warmup.md`

```markdown
---
id: inbox-0012
created: 2026-05-23
tags: [training-stability, batching]
source: "conversation 2026-05-23"
related: ["[[note-0003-adaptive-batching]]"]
---

## Fragment

Warm up the batch size during early training instead of (or alongside) the
learning rate, to stabilize the initial steps.

## Context

Came up while discussing instability in the first few hundred steps. Connects
to [[note-0003-adaptive-batching]], which also treats batch size as a
schedulable quantity.

## Open threads

Does this interact with learning-rate warmup, or replace it? Unclear.
```
