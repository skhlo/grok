# Grok Vault

The schema of the grok learning vault (`~/Vault/grok`): how a learned concept is stored, found, and resumed. Defines the vocabulary for the vault's structure, distinct from how the grok skill is distributed.

The vault is **dual-audience**: a human browses it, *and* an agent reads it to reconstruct the user's knowledge state — what they know, how solidly, how it connects, and where learning is mid-flight — to teach at the right level rather than from scratch. Schema choices serve both readers; where they conflict, agent-reconstructability wins, since the human can always read prose but the agent needs structure.

## Language

**Topic**:
The canonical unit of the vault: one folder per concept, holding that concept's files (`INDEX.md`, `CHECKPOINT.md`, etc.). One folder per concept; alternate names go in `aliases`, never duplicate folders.
_Avoid_: Entry, note, page

**Topic frontmatter**:
The YAML block at the top of a topic's `INDEX.md`. The **single source of truth** for that topic's index-level metadata (type, status, tags, timestamps, aliases). Everything else that summarizes a topic is derived from this.
_Avoid_: Topic metadata, header

**Root index**:
The vault-root `INDEX.md`: a **derived projection** (rollup table) of every topic's frontmatter, regenerated from all frontmatters on checkpoint and never hand-edited. The browsable registry for "what do I already know?" — its columns *are* the authoritative frontmatter fields.
_Avoid_: Master index, catalog, table of contents

**Derived projection**:
Any artifact computed from the topic frontmatters rather than authored directly. The root index is the only one today. Derived artifacts are regenerated, not edited, so they cannot drift from their source.
_Avoid_: Cache, generated view

**Type**:
A topic's dominant *knowledge nature*, from a **closed** four-value set: `concept` (what/why something is — Explanation/Declarative), `how-to` (how to drive a tool or task — Procedural), `reference` (lookup material — Information), `decision` (when/which/trade-offs — Conditional/Heuristic). Grounded in Diátaxis + ACT-R; singular per topic; the set does not grow.
_Avoid_: Category, kind, class

**Tags**:
Cross-cutting facets for grouping *across* topics (e.g. `tooling`, `devx`). Many per topic. Carry all *thematic* relatedness, maintenance-free. Distinct from `aliases`, which are alternate names for the *same* topic.
_Avoid_: Labels, keywords, categories

**Edge** (`related_topics`):
A directed, labeled connection from one topic to another, stored in frontmatter as `{topic, relation}`. The vault's navigable graph. `relation` is a **closed** set of the two things a tag *cannot* express: `builds-on` (directed prerequisite — order) and `contrasts-with` (alternative — read as symmetric). A merely thematic connection is **not** an edge; it routes to a shared `tag`.
_Avoid_: Link, reference, see-also

**Relation**:
The label on an edge, from the closed set `{builds-on, contrasts-with}`. `builds-on` is one-sided (stored on the dependent topic); `contrasts-with` is stored once and read symmetrically. The only write-time rule is referential integrity (the target slug must exist) — no bidirectional bookkeeping.
_Avoid_: Edge type, link kind
