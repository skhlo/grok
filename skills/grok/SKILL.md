---
name: grok
description: Quickly branch into learning a concept during coding, research, writing, or other work; search or update a global learning vault, teach at the user's current level, save resumable checkpoints, and maintain reusable Markdown learning materials. Use when the user invokes /grok, asks to grok a concept, wants a fast learning branch, wants to resume prior learning, or asks to save/update learning material.
---

The user wants a fast learning branch inside whatever work they are already doing. Keep the session moving, teach only what is needed now, and save durable Markdown material only when the user asks or confirms a checkpoint.

## Vault

Use `/Users/skhl/Vault/grok` as the global learning vault. Do not store grok topics inside the current repository unless the user explicitly asks.

Each canonical topic lives in:

```text
/Users/skhl/Vault/grok/<topic-slug>/
  INDEX.md
  CHECKPOINT.md
  REFERENCE.md
  REFERENCES.md
  HISTORY.md
  GLOSSARY.md
```

Only create files that are useful for the topic. `INDEX.md`, `CHECKPOINT.md`, and `HISTORY.md` are the default checkpoint files. `REFERENCE.md`, `REFERENCES.md`, and `GLOSSARY.md` are updated only when they add value or the user asks for learning materials.

## Topic Selection

When invoked, identify the concept the user wants to understand. Search `/Users/skhl/Vault/grok` before creating anything. Match against folder names, frontmatter `topic`, `aliases`, headings, `REFERENCE.md`, `REFERENCES.md`, and `GLOSSARY.md`.

If one existing topic is clearly the same concept, use it. If several topics may match, show the top matches and ask which one to continue. If none match, create a canonical topic slug when writing is allowed. If a new concept overlaps with an existing one, add `related_topics` metadata instead of duplicating or merging silently.

Use one canonical folder per concept. Put alternate names in `aliases` for search.

## Write Discipline

Never create or modify vault files just because this skill was invoked.

You may read and search `/Users/skhl/Vault/grok` automatically. Write only when:

- The user explicitly says to save, checkpoint, remember, update, revise, or create learning materials.
- The user confirms after you ask whether to save a checkpoint.

Before writing, briefly state what files will change. If the user declines, do not write.

If a learning branch was substantial and no save was requested, ask a lightweight checkpoint question at the end:

```text
Want me to save this as a checkpoint in `Vault/grok/<topic-slug>/`?
```

## Teaching Mode

Optimize for fast inline learning with durable resumability.

Keep the useful teaching concepts from `/teach`:

- Ground the explanation in why the concept came up during the current task.
- Estimate the user's zone of proximal development from the prompt, prior vault material, and the user's follow-up questions.
- Teach just beyond the user's current level, not from first principles unless needed.
- Use trusted references for factual, current, API-specific, legal, medical, financial, or otherwise high-stakes claims.
- Separate fluency from storage strength: a smooth explanation is not proof the user can retrieve the idea later.
- Record misconceptions and corrected assumptions when checkpointing.

Speed comes first during the learning branch. Do not quiz the user or interrupt for understanding checks while answering. At checkpoint time, ask at most one lightweight retrieval question if it would improve the saved learning state. Skip it if the user wants a quick save.

## Checkpoints

A checkpoint saves where the user stopped and how to resume. It is not the same as polishing all learning material.

On confirmed checkpoint:

- Update `INDEX.md`: topic metadata, aliases, status, revisit count, KST timestamps, and lightweight context.
- Overwrite `CHECKPOINT.md`: current understanding, stopping point, resume prompt, open loops, and optional retrieval result.
- Append `HISTORY.md`: dated KST entry for what happened in this revisit.
- Update `REFERENCES.md` only if references were actually used.
- Update `REFERENCE.md` only when the user explicitly asks to update learning material, or when checkpoint confirmation includes updating the material.
- Update `GLOSSARY.md` only when terminology matters and the user has shown enough understanding to make the term durable.

Increment `revisits` only when opening an existing topic and materially using or updating it. Searching, listing, or linking to a topic does not count.

Use KST timestamps, for example `2026-06-26 15:42 KST`.

## Lightweight Context

Context metadata exists for search, not session reconstruction. Keep it light.

Prefer:

```yaml
contexts:
  - touched_at: "2026-06-26 15:42 KST"
    workspace: "Repositories"
    repo: "project-name"
    branch: "feature/name"
    task: "short reason this concept came up"
```

Do not include diffs, file contents, environment variables, secrets, dirty status, or commit hashes by default. Avoid absolute paths unless the user asks or the path itself is the useful context.

If no Git context exists, use a short workspace or document label instead.

## Status And Staleness

Use a small status set:

- `active`: useful and likely to be revisited.
- `parked`: paused, not currently needed, but worth keeping.
- `solid`: understood well enough for current needs.
- `stale`: explicitly marked as needing recheck before relying on it.

Do not mark material stale just because time passed. Use `review_after` only when the topic is time-sensitive, version-sensitive, or depends on changing products, APIs, laws, prices, model behavior, schedules, or best practices. Warn when `review_after` has passed; do not silently change status.

## File Formats

Use the formats in:

- [INDEX-FORMAT.md](./INDEX-FORMAT.md)
- [CHECKPOINT-FORMAT.md](./CHECKPOINT-FORMAT.md)
- [REFERENCE-FORMAT.md](./REFERENCE-FORMAT.md)
- [REFERENCES-FORMAT.md](./REFERENCES-FORMAT.md)
- [HISTORY-FORMAT.md](./HISTORY-FORMAT.md)
- [GLOSSARY-FORMAT.md](./GLOSSARY-FORMAT.md)
