# Example: AI inference and tokens

This folder shows what a saved grok can look like.

The user started with a small question:

```text
@grok what is ai inference and tokens
```

The first useful handle was simple:

```text
Inference = the AI doing the work.
Tokens = the pieces of text it works with.
```

That was enough for the moment, so grok saved a checkpoint instead of trying to turn the
answer into a complete course.

## What to look at

- [INDEX.md](INDEX.md): what the topic is and what the user currently understands
- [CHECKPOINT.md](CHECKPOINT.md): where to resume next time
- [REFERENCE.md](REFERENCE.md): a cleaned-up explanation for rereading
- [REFERENCES.md](REFERENCES.md): sources searched and why they mattered
- [HISTORY.md](HISTORY.md): when the topic was revisited and what changed

## Why this example matters

grok is incremental.

You can explore a concept only until it becomes useful, save that stopping point, and come
back later for the next layer. For this topic, the first pass explains inference and tokens.
The next pass might explain context windows, pricing, latency, or why long chats get
compressed.
