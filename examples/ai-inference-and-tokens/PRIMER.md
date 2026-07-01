# AI inference and tokens Reference

## Core Idea

AI inference is the AI model being used after it has already been trained.

Tokens are the small chunks of text the model reads and writes while doing inference.

Short version:

```text
Inference = the AI doing the work.
Tokens = the pieces of text it works with.
```

## Working Model

Training is like teaching the model.

Inference is like asking the trained model to do a job.

When you send a message, the model breaks your text into tokens. It then predicts the next
token, then the next token, then the next token, until it has produced an answer.

## Examples

If you ask:

> Summarize this article.

The input tokens are your request plus the article. The output tokens are the summary.

If you ask:

> Write a shorter version.

The input tokens are your instruction plus any previous context the model can still see. The
output tokens are the shorter version it writes.

## Common Confusions

- Inference vs training: Training is how the model learns patterns. Inference is using the trained model.
- Tokens vs words: Tokens are not exactly words. A token can be a word, part of a word, punctuation, or spacing.
- More tokens is not always better: More context can help, but it also costs more, takes longer, and can make the model sort through more noise.

## Use This When

- You see AI pricing based on input tokens and output tokens.
- You wonder why long chats get slower or compressed.
- You want to understand what the model is actually doing when it answers.
- You need a simple mental model for context windows.
