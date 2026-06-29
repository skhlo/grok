# The root index is a derived projection, not an authored file

**Status:** accepted

The vault-root `INDEX.md` is a registry table of every topic, but it is **never hand-edited**. It is regenerated from all topic frontmatters on every checkpoint. Per-topic `INDEX.md` frontmatter is the single source of truth; the root index is a pure projection of it (its columns *are* frontmatter fields: topic, type, status, tags, last_touched, description).

## Why derived

The skill-distribution work in this repo exists because two authored copies of the same fact drift. A hand-maintained root index would re-introduce exactly that failure one level up: a row and its topic's own frontmatter could disagree. Making the index a projection means it cannot drift — it is rebuilt, not edited. Regeneration is cheap (rewriting a table from a few dozen frontmatters).

## Considered options

- **Stored + hand-maintained** — rejected: repeats the drift failure the distribution model was built to kill.
- **No stored index, computed on every invocation** — rejected: discards OKF's actual value (a browsable registry file readable by humans and agents) and taxes every invocation with a full scan.

## Consequences

- Every field shown in the root index must exist in frontmatter — this is *why* `description` was promoted to a frontmatter field rather than read from the body's `Current Handle`.
- Regeneration is triggered by a checkpoint (a write), not by read-only topic access. Searching or linking a topic does not rebuild the index.
