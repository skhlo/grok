# INDEX.md Format

`INDEX.md` is the entry point for a grok topic. It should be optimized for search, quick orientation, and resuming later. Its frontmatter is the **single source of truth** for the topic: the root `INDEX.md` registry is a derived projection of these fields (see [ROOT-INDEX-FORMAT.md](./ROOT-INDEX-FORMAT.md)), so everything the registry shows must live here.

## Template

```md
---
topic: "{canonical topic name}"
type: concept            # one of: concept | how-to | reference | decision
description: "{one-line glance — the registry summary column}"
aliases:
  - "{alternate name}"
tags:
  - "{cross-cutting theme}"
status: active
revisits: 1
created_at: "YYYY-MM-DD HH:MM KST"
last_touched: "YYYY-MM-DD HH:MM KST"
review_after:
related_topics:
  - topic: "{existing-topic-slug}"
    relation: builds-on   # one of: builds-on | contrasts-with
contexts:
  - touched_at: "YYYY-MM-DD HH:MM KST"
    workspace: "{short workspace label}"
    repo: "{repo name if useful}"
    branch: "{branch if useful}"
    task: "{short reason this came up}"
---

# {Canonical Topic Name}

## Why This Matters

{The practical reason this concept came up. Keep it tied to the user's work.}

## Current Handle

{The richer statement of what the user currently understands — 1-3 sentences. This is the resume detail; `description` is the one-line glance.}

## Resume Here

{The next best question, example, or task to continue from.}
```

## Field rules

- **`type`** — the topic's dominant knowledge nature, from the **closed** set `{concept, how-to, reference, decision}`. Singular. The set does not grow: never coin a new value — if none seems to fit, pick the closest.
- **`description`** — one line, the registry's summary column. Distinct from `Current Handle` (the glance vs the resume detail).
- **`tags`** — cross-cutting themes for grouping *across* topics. Curated-open: reuse an existing in-use tag before coining a new one; surface a near-duplicate for merge-or-keep at checkpoint.
- **`related_topics`** — directed, labeled edges as `{topic, relation}`, `relation ∈ {builds-on, contrasts-with}`. `builds-on` is stored once on the *dependent* topic; `contrasts-with` once on either side, read as symmetric. Every `topic` must resolve to an existing topic folder. A merely *thematic* connection is **not** an edge — make it a shared `tag`.

## Rules

- Keep context metadata light and search-oriented.
- Increment `revisits` only when an existing topic is materially used or updated.
- Use KST timestamps.
- Prefer aliases over duplicate topic folders.
