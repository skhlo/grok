# Topic edges are directed and labeled

**Status:** accepted

`related_topics` is the vault's knowledge graph: a frontmatter list of `{topic, relation}` edges, where `relation` is a closed set `{builds-on, contrasts-with}`. Edges are directed (`builds-on` stored on the dependent only; `contrasts-with` stored once and read as symmetric) and validated only for referential integrity (the target slug must resolve). Purely thematic relatedness is **not** an edge — it routes to a shared `tag`.

## Why labeled and directed

The vault is dual-audience: an agent reconstructing the user's knowledge needs to reason about *order and relationship*, not just adjacency. `pi-vs-claude-code --builds-on--> pi-agent` tells an agent to establish pi-agent first; a bare symmetric link cannot. This mirrors OKF, whose knowledge graph is explicitly a *directed* graph of semantically-meaningful links.

Adopted now, with five topics, on a one-way-door argument: stripping labels later is trivial, but back-filling relations onto dozens of bare edges (re-deriving how each pair relates) is expensive. Cheap to revert, costly to adopt late — so adopt early.

## Considered options

- **Inline body links (OKF's literal form)** — rejected: edges in prose are a second source of truth that can drift and can't be projected into the root index. We keep OKF's directed+labeled *semantics* but store edges in frontmatter (the single source of truth).
- **Symmetric bare edges** — rejected: undirected and meaningless; loses the prerequisite ordering that is the main value for the agent-view, and requires bidirectional write bookkeeping.
- **Including a `part-of` relation** — rejected: thematic/compositional grouping is what `tags` already do, maintenance-free. Edges carry only what tags cannot — dependency and contrast.

## Consequences

- The relation set is closed (like `type`); a connection that fits neither `builds-on` nor `contrasts-with` is by definition a tag, not an edge. No escape-hatch relation, so nothing to fragment, and `related_topics` stays out of junk-drawer territory.
- No symmetry enforcement: the only maintenance burden is integrity-checking the target slug exists.
