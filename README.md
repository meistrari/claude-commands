# Claude Commands

A collection of custom slash commands for [Claude Code](https://claude.com/claude-code) to automate common development workflows.

## Overview

This repository contains reusable slash commands that extend Claude Code's capabilities. Slash commands allow you to create custom workflows that Claude can execute with simple commands like `/commit` or `/pr`.

## Available Commands

### `/commit` - Create a Git Commit

Automatically analyzes your code changes and creates well-structured commits following conventional commit format.

**Usage:**
```
/commit
```

**Features:**
- Reviews git diff to understand changes
- Identifies affected components and packages
- Creates commits using conventional format: `type(scope): description`
- Supports monorepo workflows with package-specific commits
- Groups related changes logically
- Generates atomic, testable commits

**Example Output:**
```
feat(workflow): implement parallel step execution
fix(api): resolve race condition in task processing
docs(application): update component usage examples
```

### `/pr` - Create a Pull Request

Automates the creation of pull requests with comprehensive descriptions and structured commit history.

**Usage:**
```
/pr [mode] [include-tests]
```

**Arguments:**
- `mode` (optional, default: `ready`) - Set to `draft` to create a draft PR
- `include-tests` (optional, default: `false`) - Include "How to Test" section

**Features:**
- Analyzes all changes from current branch compared to `main`
- Creates structured commits before PR generation
- Generates comprehensive PR description with context
- Shows PR content for review before creation
- Supports draft and ready-for-review modes

## Installation

### Option 1: Use in a Specific Project

Copy the command files to your project's `.claude/commands/` directory:

```bash
mkdir -p .claude/commands
cp commit.md .claude/commands/
cp pr.md .claude/commands/
```

### Option 2: Use Globally

Copy the command files to your global Claude Code commands directory:

```bash
mkdir -p ~/.claude/commands
cp commit.md ~/.claude/commands/
cp pr.md ~/.claude/commands/
```

The commands will be automatically available in Claude Code.

## Creating Your Own Commands

Slash commands are markdown files with frontmatter that define:

1. **allowed-tools** - Which tools Claude can use when executing the command
2. **description** - Brief description of what the command does
3. **Body** - Instructions for Claude on how to execute the command

**Example structure:**
```markdown
---
allowed-tools: Bash(npm:*), Read, Write
description: Run tests and generate coverage report
---
# Run Tests with Coverage

## Instructions
1. Run the test suite with coverage enabled
2. Generate a coverage report
3. Summarize the results
```

Save as `.claude/commands/test-coverage.md` and use with `/test-coverage`.

## Requirements

- [Claude Code](https://claude.com/claude-code) CLI
- Additional requirements vary by command:
  - `/commit` and `/pr` require Git
  - `/pr` requires GitHub CLI (`gh`)

## Contributing

Contributions are welcome! To add a new command:

1. Create a new `.md` file with appropriate frontmatter
2. Document the command in this README
3. Submit a pull request

## License

MIT
