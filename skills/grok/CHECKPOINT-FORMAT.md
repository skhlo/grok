# CHECKPOINT.md Format

`CHECKPOINT.md` captures the latest stopping point. It is overwritten at each confirmed checkpoint.

## Template

```md
# Checkpoint: {Topic}

Updated: YYYY-MM-DD HH:MM KST

## Why This Came Up

{The coding, research, writing, or other task that triggered this learning branch.}

## Current Understanding

{Concise summary of what the user now understands.}

## User Level

{What the user appears to understand, what still seems shaky, and any misconception corrected.}

## Resume From Here

{The next best prompt, question, example, or exercise.}

## Open Loops

- {Unanswered question, claim to verify, or edge case to revisit}
```

## Rules

- Do not turn this into a session transcript.
- Include a retrieval result only if the user answered a checkpoint question.
- Keep it short enough to read before resuming.
