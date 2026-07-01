# CHECKPOINT.md Format

`CHECKPOINT.md` captures the latest stopping point — the volatile resume cursor. It is overwritten at each confirmed checkpoint. The durable knowledge state (why the topic matters, current handle) lives in the topic's [`INDEX.md`](./INDEX-FORMAT.md); this file is only where you stopped and how to resume.

## Template

```md
# Checkpoint: {Topic}

Updated: YYYY-MM-DD HH:MM KST

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
