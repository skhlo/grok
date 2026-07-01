---
name: grok
description: Quickly branch into learning a concept during coding, research, writing, or other work; search or update a global learning vault, teach at the user's current level, save resumable checkpoints, and maintain reusable Markdown learning materials. Use when the user invokes /grok, asks to grok a concept, wants a fast learning branch, wants to resume prior learning, or asks to save/update learning material.
---

The user wants a fast learning branch inside whatever work they are already doing. Keep the session moving, teach only what is needed now, and save durable Markdown material only when the user asks or confirms a checkpoint.

## Vault

Use `~/Vault/grok` as the global learning vault. Do not store grok topics inside the current repository unless the user explicitly asks.

Each canonical topic lives in:

```text
~/Vault/grok/<topic-slug>/
  INDEX.md
  CHECKPOINT.md
  REFERENCE.md
  REFERENCES.md
  HISTORY.md
  GLOSSARY.md
```

Only create files that are useful for the topic. `INDEX.md`, `CHECKPOINT.md`, and `HISTORY.md` are the default checkpoint files. `REFERENCE.md`, `REFERENCES.md`, and `GLOSSARY.md` are updated only when they add value or the user asks for learning materials.

## Topic Selection

When invoked, identify the concept the user wants to understand. Search `~/Vault/grok` before creating anything. Start from the root `INDEX.md` registry — it lists every topic (name, type, tags, summary) in one file, so it is the cheapest way to see what already exists. If that is inconclusive, match more deeply against folder names, frontmatter `topic`, `aliases`, headings, `REFERENCE.md`, `REFERENCES.md`, and `GLOSSARY.md`.

If one existing topic is clearly the same concept, use it. If several topics may match, show the top matches and ask which one to continue. If none match, create a canonical topic slug when writing is allowed. If a new concept connects to an existing one, add a `related_topics` edge (see Topic Schema) instead of duplicating or merging silently.

Use one canonical folder per concept. Put alternate names in `aliases` for search.

## Topic Schema

Every topic's `INDEX.md` frontmatter is the single source of truth; the root `INDEX.md` registry is a derived projection of it. Maintain these fields (full spec in [INDEX-FORMAT.md](./INDEX-FORMAT.md)):

- **`type`** — the topic's dominant knowledge nature, from the **closed** set `{concept, how-to, reference, decision}`. Singular. The set does not grow: never coin a new value — if none seems to fit, pick the closest.
- **`tags`** — cross-cutting themes for grouping across topics. Curated-open: before tagging, read the tags already in use across the vault and **reuse an existing tag** rather than coin a near-duplicate. If a genuinely new tag is needed, surface it at checkpoint ("new tag `dx` — you already use `devx`; merge or keep?") before writing it.
- **`description`** — a one-line summary; the registry's glance column. Keep it distinct from `Current Handle` (the richer resume detail).
- **`related_topics`** — the knowledge graph, as directed labeled edges `{topic, relation}`, `relation ∈ {builds-on, contrasts-with}`. `builds-on` is a prerequisite (stored once on the dependent topic); `contrasts-with` marks alternatives (stored once, read symmetric). Every `topic` must resolve to an existing topic folder — never point at a non-topic. A connection that is neither a prerequisite nor a contrast is **not** an edge; express it as a shared `tag`.

## Write Discipline

Never create or modify vault files just because this skill was invoked.

You may read and search `~/Vault/grok` automatically. Write only when:

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

- Update `INDEX.md`: frontmatter (`type`, `description`, `tags`, `related_topics` edges, aliases, status, revisit count, KST timestamps, lightweight context) and the body's durable knowledge state (`Why This Matters`, `Current Handle`).
- Overwrite `CHECKPOINT.md` (the volatile resume cursor): user level, stopping point, resume prompt, open loops, and optional retrieval result. Knowledge state lives in `INDEX.md`, not here.
- Append `HISTORY.md`: dated KST entry for what happened in this revisit.
- Update `REFERENCES.md` only if references were actually used.
- Update `REFERENCE.md` only when the user explicitly asks to update learning material, or when checkpoint confirmation includes updating the material.
- Update `GLOSSARY.md` only when terminology matters and the user has shown enough understanding to make the term durable.
- Regenerate the root `INDEX.md`: rewrite the registry table from **all** topic frontmatters. It is a derived projection — never hand-edit it. See [ROOT-INDEX-FORMAT.md](./ROOT-INDEX-FORMAT.md).

Increment `revisits` only when opening an existing topic and materially using or updating it. Searching, listing, or linking to a topic does not count.

Use KST timestamps, for example `2026-06-26 15:42 KST`. Read the actual current time from the system before writing any timestamp — run `TZ='Asia/Seoul' date '+%Y-%m-%d %H:%M KST'` — never guess a time or copy one from an example. KST is this vault's default; to use another timezone, change the `TZ` value and the `KST` label consistently across the vault.

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

Do not mark material stale just because time passed. Use `review_after` only when the topic is time-sensitive, version-sensitive, or depends on changing products, APIs, laws, prices, model behavior, schedules, or best practices.

## Surfacing Due Topics

A topic is **due** when its `review_after` is in the past, or its `status` is `stale`. Surface due topics so learning does not silently rot:

- On invocation, if any topic is due, mention it in one concise, non-blocking line (e.g. "2 topics due for recheck: `pi-vs-claude-code`, `vitest`"). Do not interrupt the learning branch beyond that line; surface at most once per session.
- On demand ("what's due in my vault"), list the due topics.
- The root `INDEX.md` marks due rows with ⚠, but that marker is only a snapshot from the last regeneration; this live check on invocation is authoritative.

Surface only — never auto-change `status` or `review_after`. Offer to re-grok the topic or bump `review_after`, and act only on confirmation.

## File Formats

Use the formats in:

- [INDEX-FORMAT.md](./INDEX-FORMAT.md)
- [ROOT-INDEX-FORMAT.md](./ROOT-INDEX-FORMAT.md)
- [CHECKPOINT-FORMAT.md](./CHECKPOINT-FORMAT.md)
- [REFERENCE-FORMAT.md](./REFERENCE-FORMAT.md)
- [REFERENCES-FORMAT.md](./REFERENCES-FORMAT.md)
- [HISTORY-FORMAT.md](./HISTORY-FORMAT.md)
- [GLOSSARY-FORMAT.md](./GLOSSARY-FORMAT.md)
