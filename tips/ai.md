# AI Tips ([cd ..](../README.md))

- [Snapshot First, Nuke Later](#claude-code--snapshot-first-nuke-later)
- [No MCP? No Problem](#claude-code--no-mcp-no-problem)

## Claude Code 💡: Snapshot First, Nuke Later

Claude Code going off the rails? Take a snapshot of the conversation before you clear the context.

This helps in 2 ways: you won't have to start from scratch, and reviewing the snapshot can help you spot what went wrong so you can fix it before loading it again 🙌🏽

```markdown
Take a concise snapshot to .snapshots/. Summarize what we're doing, what's done, what's next, and flag anything that felt off.
```

## Claude Code 💡: No MCP? No Problem

Services you're using don't offer an MCP? Check if they have a CLI tool and turn it into a skill, that's really all you need.

You can use the official skill-creator skill to build/improve those skills 🙌🏽

```markdown
Create a skill for Forge CLI. Here's the docs: https://forge.laravel.com/docs/cli.md. <Include more context and clearly set expectations for the agent>_
```
