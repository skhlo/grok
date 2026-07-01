# Vault Schema

How grok stores what you learn. The vault lives at **`~/Vault/grok/`** and is **plain Markdown with YAML frontmatter** — no database, no lock-in. You can read, grep, edit, and version it like any other folder of notes.

The format is based on the [**Open Knowledge Format (OKF)**](https://cloud.google.com/blog/products/data-analytics/how-the-open-knowledge-format-can-improve-data-sharing): a directory of Markdown concept files with structured frontmatter and a nested index, designed so both humans and AI agents can read it. grok's vault is **dual-audience** — browsable by you, and machine-readable so an agent can reconstruct what you already know and teach accordingly.

## Layout

```text
~/Vault/grok/
├── INDEX.md                  ← root registry: every topic, at a glance (derived)
├── git/                      ← one folder per topic (the topic "slug")
│   ├── INDEX.md              ← the topic's frontmatter + orientation (always present)
│   ├── CHECKPOINT.md         ← where you stopped and how to resume
│   ├── HISTORY.md            ← dated log of each revisit
│   ├── REFERENCE.md          ← distilled learning material (optional)
│   ├── REFERENCES.md         ← curated sources — the topic's grounding
│   └── GLOSSARY.md           ← canonical terms for the topic (optional)
└── vitest/
    └── …
```

One folder per concept. Alternate names live in `aliases` (frontmatter) — never as duplicate folders.

## A topic's files

| File | Holds | When |
|------|-------|------|
| `INDEX.md` | Frontmatter (the source of truth) + why it matters, current handle — the durable knowledge state | Always |
| `CHECKPOINT.md` | The volatile resume cursor: user level, stopping point, resume prompt, open loops | On checkpoint |
| `HISTORY.md` | Append-only dated log of each revisit | On checkpoint |
| `REFERENCE.md` | Reusable distilled material (with optional `## Explanation` / `## How To` sections) | When useful |
| `REFERENCES.md` | Annotated source list — the topic's grounding | On checkpoint |
| `GLOSSARY.md` | Tight, opinionated definitions of the topic's terms | When terms are durable |

Files are created **only when they add value** — a sparse topic with just `INDEX.md` is correct, not incomplete.

## Topic frontmatter

The heart of the schema. A topic's `INDEX.md` opens with YAML that is the single source of truth for that topic:

```yaml
---
topic: "lazygit"
type: how-to                 # closed set: concept | how-to | reference | decision
description: "A terminal UI for moving code through git states: working tree → staged → commit → remote."
aliases:                     # other names, for search
  - "lazy git"
  - "Git TUI"
tags:                        # cross-cutting themes, for grouping across topics
  - "git"
  - "tooling"
status: active               # active | parked | solid | stale
revisits: 1
created_at: "2026-06-27 01:19 KST"
last_touched: "2026-06-27 01:19 KST"
review_after:                # optional date; when past, the topic is "due" for recheck
related_topics:              # directed, labeled edges to other topics
  - topic: "git"
    relation: builds-on      # builds-on | contrasts-with
contexts:                    # lightweight: where/why the topic came up
  - touched_at: "2026-06-27 01:19 KST"
    workspace: "Repositories"
    repo: "my-project"
    branch: "main"
    task: "Understand lazygit through the git states it moves code between"
---
```

### Field reference

- **`type`** — the topic's dominant *knowledge nature*, from a **closed** set (it never grows):
  - `concept` — what/why something is (a mental model)
  - `how-to` — how to drive a tool or task (procedure)
  - `reference` — lookup material (syntax, flags, API)
  - `decision` — a choice and its trade-offs (when/which)
- **`description`** — a one-line glance; the summary column in the root index. Distinct from the body's richer `## Current Handle`.
- **`tags`** — cross-cutting themes (`tooling`, `testing`, `ai-agents`). Group topics *across* types. Reused before new ones are coined, so they don't fragment.
- **`status`** — `active` (likely to revisit), `parked` (paused), `solid` (understood enough), `stale` (needs recheck).
- **`review_after`** — an optional date for time-sensitive topics (changing APIs, prices, model behavior). When it's in the past, the topic is surfaced as **due**.
- **`related_topics`** — the knowledge graph, as directed, labeled edges:
  - `builds-on` — a prerequisite (stored on the dependent topic; e.g. lazygit builds-on git)
  - `contrasts-with` — an alternative (read as symmetric)
  - Every edge points at a real topic. A merely *thematic* link is a shared `tag`, not an edge.
- **`aliases`** — alternate names for search. **`contexts`** — light breadcrumbs (workspace/repo/branch/task), never diffs or secrets.

### Body

Below the frontmatter, two short sections holding the durable knowledge state: **Why This Matters** (why it came up) and **Current Handle** (what you understand now). The resume cursor (where you stopped, next step) lives in `CHECKPOINT.md`, not here.

## The root index

`~/Vault/grok/INDEX.md` is a registry of every topic — the "what do I already know?" entry point:

```md
| Topic | Type | Status | Tags | Updated | Summary |
|-------|------|--------|------|---------|---------|
| [lazygit](./lazygit/INDEX.md) | how-to | active | git, tooling | 2026-06-27 | A terminal UI for moving code through git states… |
```

It is a **derived projection**: every column comes straight from a topic's frontmatter, it is regenerated (never hand-edited), and topics that are **due** for recheck are marked with ⚠. Because it's purely derived, it can never drift from the topics it summarizes.

## How it maps to OKF

| OKF idea | In grok |
|----------|---------|
| Directory of Markdown + YAML frontmatter | The whole vault |
| Nested `index.md` (root + per-concept) | Root `INDEX.md` + per-topic `INDEX.md` |
| `type` as the one required classification | `type` (closed enum) |
| `tags` for discovery | `tags` |
| Directed knowledge graph via links | `related_topics` edges (`builds-on` / `contrasts-with`) |
| Chronological `log` | `HISTORY.md` |
