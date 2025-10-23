# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This repository provides a collection of reusable slash commands for Claude Code. Slash commands are custom workflows defined in markdown files that extend Claude Code's capabilities with project-specific or workflow-specific automation.

## Slash Command Structure

Slash commands in this repository follow a specific format:

**Frontmatter (YAML):**
- `allowed-tools`: Specifies which Claude Code tools can be used when executing the command
  - Format: `Bash(command:*), Read, Write, Edit, Grep, Glob`
  - Bash commands can be scoped: `Bash(git add:*)` allows only `git add` commands
- `description`: Brief one-line description shown in Claude Code's command list

**Body (Markdown):**
- Instructions for Claude on how to execute the command
- Process steps, best practices, and examples
- Can include argument definitions using `$1`, `$2`, etc.

## Command Development Guidelines

When creating or modifying slash commands:

1. **Document in README**: After creating a new command, update [README.md](README.md) with:
   - Command name and description
   - Usage instructions
   - Available arguments (if any)
   - Features and capabilities
   - Example outputs
   - Any special requirements (e.g., Git, GitHub CLI)

2. **Conventional Commits**: Commands that work with Git should enforce conventional commit format
   - Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`
   - Scope: package/component name
   - Description: imperative mood, no AI attribution

3. **Monorepo Support**: Commands should be designed to work with monorepo workflows
   - Separate commits by package when changes span multiple packages
   - Use package name as scope
   - Group related changes logically, not just by file

4. **Commit Atomicity**: Each commit should be a coherent, testable unit
   - Avoid mixing refactoring with feature changes
   - Separate by functionality
   - Include context in commit body for complex changes

## Installation Paths

Commands can be installed in two locations:
- **Project-specific**: `.claude/commands/` in project root
- **Global**: `~/.claude/commands/` for use across all projects

## Tool Restrictions

Commands use `allowed-tools` to restrict which tools Claude can access during execution. This ensures commands stay focused and secure. Be specific about which tools and commands are needed for each slash command to maintain security and clarity.
