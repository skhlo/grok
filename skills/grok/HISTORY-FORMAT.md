# HISTORY.md Format

`HISTORY.md` is an append-only revisit log. Add one entry per confirmed checkpoint or material update.

## Template

```md
# {Topic} History

## YYYY-MM-DD HH:MM KST

- Context: {short task or workspace reason}
- Learned: {what changed in understanding}
- Updated: {files changed}
- Next: {best continuation point}
```

## Rules

- Append; do not rewrite prior history except to fix clear errors.
- Keep entries short.
- Record material updates separately from simple checkpoints when that distinction matters.
