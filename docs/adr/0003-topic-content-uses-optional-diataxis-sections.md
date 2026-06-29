# Topic content uses optional Diátaxis sections, never a fixed template

**Status:** accepted

A topic's learning material (`REFERENCE.md`) draws from a **menu** of Diátaxis-aligned sections — `## Explanation`, `## How To`, plus the existing reference material — adding only the sections that have real content. The four Diátaxis modes (Explanation, How-To, Reference, Tutorial) are the documented menu; they are not mandatory headings. This closes grok's missing home for procedural "how-to" knowledge (previously crammed into prose) without multiplying files.

## Why a menu, not a template

The skill must **not force inputs**: no empty `## How To` scaffolding on a pure-concept topic, no padding to "complete" a template. A sparse topic is correct, not unfinished — this extends grok's existing "only create files that are useful" rule down to the section level. A future reader (human or agent) seeing a topic with only `## Explanation` should read that as "this is a concept, it has no procedure," not "someone forgot the how-to."

## Considered options

- **Type-driven separate files** (`HOW-TO.md` per `how-to` topic) — rejected: more files and a `type`→file rule to maintain than a ~30-topic vault needs. Sections compose with `type` more cheaply (a `how-to` topic's `REFERENCE.md` simply leads with `## How To`).
- **Fixed section template** — rejected: forces empty headings, which read as incomplete and bloat the file. The no-forcing rule is the whole point.

## Consequences

- `type` predicts which section a topic emphasizes (a `how-to` topic leads with `## How To`; a `concept` topic with `## Explanation`) but never dictates which sections must exist.
- Tutorial mode is in the menu but expected to be rare in a fast-learning vault; it is not scaffolded.
