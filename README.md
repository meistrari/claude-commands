# Claude Commands

Custom slash commands for [Claude Code](https://claude.com/claude-code) to automate development workflows.

## Commands

- [`/commit`](commit.md) - Analyzes your changes and creates well-structured commits following conventional commit format
- [`/pr`](pr.md) - Creates pull requests with comprehensive descriptions and structured commit history

## Installation

### Project-specific

```bash
mkdir -p .claude/commands
cp commit.md .claude/commands/
cp pr.md .claude/commands/
```

### Global

```bash
mkdir -p ~/.claude/commands
cp commit.md ~/.claude/commands/
cp pr.md ~/.claude/commands/
```

## License

MIT
