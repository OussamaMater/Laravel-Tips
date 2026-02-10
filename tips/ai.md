# AI Tips ([cd ..](../README.md))

- [Snapshot First, Nuke Later](#claude-code--snapshot-first-nuke-later)

## Claude Code 💡: Snapshot First, Nuke Later

Claude Code going off the rails? Take a snapshot of the conversation before you clear the context.

This helps in 2 ways: you won't have to start from scratch, and reviewing the snapshot can help you spot what went wrong so you can fix it before loading it again 🙌🏽

```markdown
Take a concise snapshot to .snapshots/. Summarize what we're doing, what's done, what's next, and flag anything that felt off.
```
