# INDEX.md Format

`INDEX.md` is the entry point for a grok topic. It should be optimized for search, quick orientation, and resuming later.

## Template

```md
---
topic: "{canonical topic name}"
aliases:
  - "{alternate name}"
status: active
revisits: 1
created_at: "YYYY-MM-DD HH:MM KST"
last_touched: "YYYY-MM-DD HH:MM KST"
review_after:
related_topics: []
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

{The shortest useful statement of what the user currently understands.}

## Resume Here

{The next best question, example, or task to continue from.}
```

## Rules

- Keep context metadata light and search-oriented.
- Increment `revisits` only when an existing topic is materially used or updated.
- Use KST timestamps.
- Prefer aliases over duplicate topic folders.
