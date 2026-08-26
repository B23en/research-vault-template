---
name: promote-notes
description: Surveys inbox/ for fragments ripe for synthesis and, after user approval, creates notes/ notes one stage up the pipeline. Scoped to one transition — inbox/ → notes/. Use when the user asks to promote, synthesize, advance, level up, or move notes forward — and offer it proactively when several inbox/ fragments have accumulated around the same thought, when the user keeps returning to a topic or says it feels settled, or when a research discussion has just produced a batch of fragments. Always presents the candidate slate for review before writing anything.
---

# promote-notes

## Purpose

Promotion is how the research moves up the pipeline: raw fragments crystallise
into worked-out notes. The base agent already offers this conversationally when
material looks ready (per the suggest-don't-spring rule in `CLAUDE.md`
`## Skills`). This skill covers the **batched,
deliberate** case — the user wants the agent to sweep the current state, judge
what is ripe, and propose a whole slate of promotions in one pass.

Synthesis is a judgment-heavy additive action: getting it wrong produces a
misleading note that downstream work then builds on. So this skill always
**presents first, writes second**. Nothing is created until the user approves
the slate.

## Scope

One transition is in scope:

- `inbox/` → `notes/` — synthesise one or more fragments into a `note-NNNN` note.

Other transitions are out of scope: `notes/` → `experiments/` belongs to
`specify-methodology`; direction-level changes belong to `review-direction`;
verification is handled by `verify-consistency`.

## When to use

- **Explicit** — the user says "promote", "synthesize these", "advance the
  pipeline", "level up", "what's ready to move forward", or otherwise asks to
  move fragments forward. Run it.
- **Proactive** — reach for it unasked when the vault arrives at the moment.
  Signals worth acting on are several `inbox/` fragments accumulating around
  the same thought, the user circling back to a topic or calling it settled,
  and a research discussion that has just produced a batch of fragments.

Proactive means **offer in one line and wait**, not start. Phase 1 reads the
whole of `inbox/` and `notes/`, so it never runs unprompted. An offer the user
declines or ignores is dropped — do not re-offer for the same fragments in the
same session.

## Procedure

The skill has two phases. **Do not collapse them — present, wait, then write.**

### Phase 1 — Survey & present

1. **Read the baseline.** Read `Direction.md` so judgments respect confirmed
   constraints. Skim `Memory.md` for working context and open questions.
2. **Survey the source folder.** List `inbox/` in full and read every fragment.
   Then read `notes/` and follow each note's `related` to see which fragments
   already feed it, so the same fragment is not re-promoted into a second note.
3. **Cluster and judge.** Group fragments that point at the same underlying
   thought. A cluster of two or more related fragments is a strong candidate; a
   single fragment that is already substantial and standalone is a weaker but
   valid candidate. Skip fragments that are still raw, off-topic against
   `Direction.md`, or already synthesised into an existing note.
4. **Draft the slate.** For each candidate, prepare:
   - **Proposed title** in the standard `short-title` style (lowercase,
     hyphen-separated, 2–5 words).
   - **Sources** — one line per fragment: its `[[wiki-link]]` *and what that
     fragment actually says*, in the fragment's own terms. A bare list of
     filenames is not enough. The user is being asked whether these belong
     together, and cannot judge that from names alone — most fragments were
     captured weeks earlier and are no longer in anyone's head. Keep each line
     faithful to the original rather than pre-arguing the merge, and say so
     plainly when a fragment is too tangled to compress honestly.
   - **Synthesis preview** — 2–3 sentences describing what the new note will
     say. This is what the user is approving.
   - **Judgment** — one sentence on why this is worth promoting now.
   - **Caveats** — anything the user should know before approving: a weak link,
     a competing interpretation, a missing piece.
5. **List deliberate exclusions.** For each source fragment the agent
   considered but left out, give both what it says and why it was skipped —
   "still raw" means little without a line on what the raw thing is. The user
   often wants to override these.
6. **Present and stop.** Send the slate to the user as a numbered list (so they
   can accept, reject, or amend by number) using the format below, and **wait**.
   Do not create any notes in this phase.

### Phase 2 — Execute on approval

Run this phase only after the user approves — fully, partially, or with edits.

7. **Confirm the final set.** If the user said "do 1, 3, 5", restrict to those.
   If they renamed or reframed an item, use the updated version. If they
   rejected the whole slate, stop and report.
8. **Allocate ids up front.** Before writing, compute the next `note-NNNN` id
   for the *whole batch* so multiple new notes get sequential numbers without
   collision (per `CLAUDE.md` numbering rules: list the folder, find the highest
   existing `NNNN`, increment per item in order).
9. **Create the notes.** For each approved item, write the file using the
   template below. In the new note's `related`, link every source fragment as
   `[[wiki-link]]`. **Do not modify the source notes** — promotion creates a
   new note; the originals stay where they are (per `CLAUDE.md` lifecycle:
   "folders are stages", promotion is never a move or rename).
10. **Report back.** List the new filenames, note any items the user dropped
    from the slate, and end with a question that pushes the next move — which
    note to specify into an experiment, which one to develop further, etc.

## Note template

`notes/` also holds discussion and writing material that never came from a
promotion; those are free-form. This template is for the synthesis case only —
a note built out of `inbox/` fragments.

```markdown
---
id: note-NNNN
created: YYYY-MM-DD
tags: [topic-tag]
source: "promote-notes YYYY-MM-DD; synthesized from inbox-XXXX, inbox-YYYY"
related: ["[[inbox-XXXX-...]]", "[[inbox-YYYY-...]]"]
---

## Idea
<!-- The synthesized idea in 3–6 sentences. State what the idea *is*, not just
     what the fragments said. -->

## Why this is a coherent idea
<!-- What ties the source fragments together; the underlying thought. -->

## Open threads
<!-- What is unresolved; what would need to be true for this to matter. -->

## Sources
<!-- [[Wiki-link]] each source fragment, one line on what it contributed. -->
```

## Slate presentation format

Use this exact shape in Phase 1 so the user can reply by number:

```markdown
## Proposed promotions (review before I write anything)

1. **note-NNNN — proposed-title**
   - Sources
     - [[inbox-XXXX-...]] — <what this fragment says>
     - [[inbox-YYYY-...]] — <what this fragment says>
   - Synthesis: <2–3 sentences describing what the new note will say>
   - Judgment: <one sentence on why now>
   - Caveats: <weak link / competing reading / missing piece — if any>

2. **note-NNNN — proposed-title**
   - Sources
     - [[inbox-ZZZZ-...]] — <what this fragment says>
   - Synthesis: <2–3 sentences>
   - Judgment: <one sentence>
   - Caveats: <if any>

## Deliberately excluded

- [[inbox-WWWW-...]] — <what it says> — <why it was left out>

---

Reply with the numbers to promote (e.g. "1 and 3", "all", "1 but rename to X"),
or tell me what to change. The one-line summaries above are my compression of
each fragment — open any of them directly if you want to check my reading
against the original before deciding.
```

If the survey turns up nothing worth promoting, say so plainly instead of
manufacturing a slate. "Nothing is ripe yet, here is what is closest and what
it still needs" is a valid and useful outcome.
