---
allowed-tools: Bash(git status:*), Bash(git log:*), Bash(git branch:*), Bash(git diff:*), Bash(git show:*), Bash(git rev-parse:*), Read
description: Describes changes in the current git repo to help you get back to work
---

# Help User Resume Work After Being Away

## Context

- Current git status: !`git status`
- Current branch: !`git branch --show-current`
- Recent commits: !`git log --oneline -10`
- Recent commits that are not on `main`: !`git log --oneline main..HEAD 2>/dev/null || git log --oneline -5`
- Current git diff (staged and unstaged changes): !`git diff HEAD`
- Detailed diff with file stats: !`git diff HEAD --stat`

## Your Task

The user has been away from this project and needs to quickly understand where they left off so they can resume work. Analyze the repository state and provide a clear, actionable summary:

1. **Where You Left Off**: Start with a brief overview of what branch they're on and what they were working on

2. **Completed Work**: Summarize the committed changes
   - What has been accomplished (based on recent commits)
   - Group related commits together to tell a coherent story
   - Highlight the key files that were changed

3. **Work In Progress**: Analyze uncommitted changes (staged and unstaged)
   - What modifications are currently in the working directory
   - Whether these look like work-in-progress or leftover debugging
   - Any potential next steps based on the current state

4. **Suggested Next Steps**: Based on the changes, suggest what the user might want to do next:
   - Complete unfinished work
   - Commit/push pending changes
   - Continue with the next logical task
   - Review or test recent changes

Present this in a friendly, conversational tone that helps the user quickly orient themselves and get back to being productive. Focus on answering: "What was I doing, and what should I do next?"

If there are no uncommitted changes and recent commits suggest the work is complete, indicate this is a good checkpoint to start something new or that they may be on a clean branch.
