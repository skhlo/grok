# REFERENCES.md Format

`REFERENCES.md` is the curated source list for a grok topic — the grounding an agent draws its answers from. Because grok grounds answers in active search, a grok yields sources; this file persists them so a revisit builds on citations instead of re-searching.

## Template

```md
# {Topic} References

## Sources

- [{Title}](https://example.com)
  Used for: {what this source answered}
  Trust: {why this source is credible enough for this topic}

## Gaps

- {Missing source, unverified claim, or area to check later}
```

## Rules

- Prefer primary sources, official docs, papers, recognized experts, and well-moderated communities.
- Annotate every source; bare links are not useful later.
- A grounded grok always yields sources — record them. `## Gaps` lists what the search has not yet answered; that list drives the next revisit's search (fill gaps and re-verify *due* sources rather than re-fetching what is already captured).
- For current or high-stakes topics, record enough source context to know what may need rechecking.
