# Topic `type` is a closed, framework-grounded enum

**Status:** accepted

Each vault topic carries a singular `type` from a **closed** four-value set — `concept`, `how-to`, `reference`, `decision` — used as a grouping/filter column in the derived root index. The set is fixed: there is no mechanism for the skill to grow it.

## Why closed, and why these four

A growing vocabulary ("add a type when one is genuinely needed") relies on a stateless model checking the existing set before coining a term — exactly the actor that fragments vocab (`tool` vs `cli-tool` vs `utility`). Rather than gate growth on confirmation, we remove growth: anchor `type` to an established taxonomy wide enough to be complete. The four values are the *knowledge-nature* axis from **Diátaxis** (theoretical/practical) sharpened by **ACT-R** (declarative/procedural/conditional): `concept`=Explanation/Declarative, `how-to`=How-To/Procedural, `reference`=Reference/Information, `decision`=Conditional/Heuristic. All five seed topics map cleanly (git, pi-agent → concept; lazygit, vitest → how-to; pi-vs-claude-code → decision).

## Considered options

- **Growing vocab gated on confirmation** — rejected: still treats `type` as expandable; closed-and-complete is simpler and removes the failure mode entirely.
- **A matrix (Diátaxis × ACT-R, etc.)** — rejected: 4×3 = 12 mostly-empty cells for a vault wanting ~4-6 buckets. Combinatorial explosion against the simplicity rule.
- **Cynefin / DIKW as `type`** — rejected: Cynefin (problem complexity) gives no discrimination here; DIKW (synthesis maturity) is what `status` already encodes.

## Consequences

- Multi-dimensionality lives in **separate orthogonal fields**, not a compound type: `type` (knowledge nature), `status` (DIKW-style maturity), `tags` (cross-cutting facets).
- **Diátaxis classifies content modes within a topic, not the topic itself** — so it is the right lens for deciding *which files a topic should contain* (REFERENCE.md = Reference, teaching = Explanation), a separate decision from `type`.
