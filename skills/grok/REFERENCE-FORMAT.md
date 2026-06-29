# REFERENCE.md Format

`REFERENCE.md` is the reusable distilled learning material for a topic. Update it only when the user asks to update learning material, or when checkpoint confirmation includes updating the material.

## Template

```md
# {Topic} Reference

## Core Idea

{The compressed explanation.}

## Working Model

{A practical mental model the user can apply.}

## Examples

{Short examples tied to real use.}

## Common Confusions

- {Misconception}: {Correction}

## Use This When

- {Situation where this concept should be recalled}
```

## Diátaxis sections (optional menu)

Beyond the core sections above, a topic may draw from a menu of Diátaxis-aligned content modes, adding **only** the ones with real content:

- **`## Explanation`** — understanding-oriented: the why, the mental model. (`concept` topics lead here.)
- **`## How To`** — task-oriented procedural steps. (`how-to` topics lead here; closes grok's previous gap where procedure got buried in prose.)
- **`## Reference`** — dry, complete lookup material (syntax, flags, API). (`reference` topics lead here.)
- Tutorial (learning-oriented walkthrough) is in the menu but expected to be rare; do not scaffold it.

`type` *predicts* which section a topic emphasizes but never *dictates* which must exist.

## Rules

- **Never force inputs.** Add a section only when it has content. A sparse topic is correct, not incomplete — do not emit empty headings to "complete" a template.
- Prefer useful compression over completeness.
- Keep examples concrete.
- Link to `REFERENCES.md` for source details instead of cluttering this file.
