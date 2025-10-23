---
allowed-tools: Bash(git add:*), Bash(git status:*), Bash(git commit:*), Bash(gh:*)
description: Create a new Pull Request
---
# Create Pull Request

## Arguments
Mode (default: ready): $1
Include how to test (default: false): $2

## Overview
Automate the creation of well-structured commits and pull requests by analyzing code changes and following established conventions.

## Process

### 1. Analyze Code Changes
- **Review the git diff** to understand the scope and nature of changes
- **Identify affected components/packages** in the codebase
- **Assess the impact** (breaking changes, new features, bug fixes, etc.)
- **Categorize changes** by functionality or package for logical grouping

### 2. Create Structured Commits
- **Use conventional commit format**: `type(scope): description`
  - **Types**: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`
  - **Scope**: package name (for monorepos) or component/module affected.
  - **Description**: concise one line summary in imperative mood. Do not add any message about the use of AI to generate the commit's message

- **For monorepos**: 
  - Separate commits by package when changes span multiple packages
  - Use package name as scope: `feat(workflow): add new step validation`
  - Include context in commit body if needed for complex changes

- **Multi-commit strategy**: Group related changes logically
  - Separate by functionality, not just by file
  - Each commit should be a coherent, testable unit
  - Avoid mixing refactoring with feature changes

### 3. Generate Pull Request
- **Title**: Brief conventional commit message about the changes
- **Description structure**:
  
  **Context:**
  - Brief explanation of what was changed and why
  - Link any related issues or requirements
  - Highlight any breaking changes or important considerations
  
  **How to Test:** *(when applicable)*
  - Specific steps to verify the changes work correctly
  - Any setup requirements or test data needed
  - Expected behavior after the changes

- **Instructions**: 
  - show me the PR content before creating the PR
  - generate the PR in draft mode if the "Mode" argument is "draft"
  - always consider `main` as the parent branch. compare changes from the current branch with the `main` branch

## Best Practices
- **Keep commits atomic**: Each commit should represent one logical change
- **Write for reviewers**: Assume they need context about the changes
- **Be specific**: Avoid vague descriptions like "fix bugs" or "update code"
- **Reference issues**: Link to tickets, requirements, or discussions when relevant
- **Update existing PRs**: If a PR already exists, update it with new relevant information

## Example Outputs

**Commit Messages:**

feat(workflow): implement parallel step execution
fix(api): resolve race condition in task processing  
docs(application): update component usage examples

**PR Description:**

## Context
Implements parallel execution for workflow steps to improve performance. Previously, steps executed sequentially even when they had no dependencies, causing unnecessary delays in workflow completion.

## How to Test
1. Create a workflow with multiple independent steps
2. Run the workflow and observe execution time
3. Verify all steps complete successfully and results are correct
4. Check workflow logs show parallel execution indicators
