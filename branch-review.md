---
allowed-tools: Bash(git diff:*), Bash(git status:*), Bash(git branch:*), Read, Grep
description: Review code changes comparing current branch with main
---
# Branch Review

## Overview
Perform a comprehensive code review by comparing the current branch with main, analyzing changes for quality, security, performance, and potential risks.

## Process

### 1. Gather Branch Context
- **Verify current branch** using `git branch --show-current`
- **Get comprehensive diff** with `git diff main...HEAD --stat` for overview
- **Analyze detailed changes** with `git diff main...HEAD` for line-by-line review
- **Identify commit history** with `git log main..HEAD --oneline` to understand progression

### 2. Categorize Changes
Group changes by type and impact:
- **New Features**: Identify entirely new functionality
- **Bug Fixes**: Changes addressing existing issues
- **Refactoring**: Code improvements without behavior changes
- **Dependencies**: Package or library updates
- **Configuration**: Build, deployment, or environment changes
- **Documentation**: README, comments, or documentation updates
- **Tests**: New or modified test cases

### 3. Code Quality Review
For each modified file, analyze:

**Code Structure & Design:**
- Single Responsibility Principle adherence
- Code duplication or copy-paste patterns
- Function/method complexity (cyclomatic complexity)
- Clear and descriptive naming conventions
- Proper abstraction levels
- Error handling completeness

**Best Practices:**
- Language-specific idioms and conventions
- Consistent code style with existing codebase
- Comments where complexity requires explanation
- Appropriate use of design patterns
- Dead code or commented-out code removal

**Performance Considerations:**
- Inefficient algorithms or loops (O(n²) or worse)
- Unnecessary database queries or N+1 problems
- Memory leaks or resource management issues
- Caching opportunities
- Large file operations without streaming

### 4. Security Analysis
Identify potential security concerns:
- **Input Validation**: Unvalidated user input, injection vulnerabilities
- **Authentication/Authorization**: Proper access control checks
- **Sensitive Data**: Hardcoded secrets, exposed credentials, PII handling
- **Dependencies**: Known vulnerabilities in added/updated packages
- **API Security**: Rate limiting, CORS configuration, secure headers
- **Cryptography**: Weak algorithms, improper key management
- **Error Messages**: Information disclosure through error details

### 5. Risk Assessment
For each area of concern, classify risk level:

**High Risk (🔴):**
- Security vulnerabilities
- Data loss potential
- Breaking changes without migration
- Performance degradation in critical paths
- Missing error handling for critical operations

**Medium Risk (🟡):**
- Code smells that could lead to bugs
- Incomplete test coverage for new features
- Technical debt accumulation
- Moderate performance concerns
- Unclear or complex logic

**Low Risk (🟢):**
- Minor style inconsistencies
- Non-critical documentation gaps
- Optimization opportunities
- Refactoring suggestions

### 6. Generate Review Report
Provide a structured review with:

**Executive Summary:**
- Total files changed, lines added/removed
- Overall risk assessment
- Critical issues count by severity
- Recommendation (approve, request changes, block)

**Detailed Findings:**
For each issue found:
- **File & Location**: `path/to/file.ext:line_number`
- **Category**: Security, Performance, Quality, etc.
- **Severity**: High/Medium/Low
- **Description**: What the issue is
- **Impact**: Why it matters
- **Suggestion**: How to fix or improve

**Positive Highlights:**
- Well-implemented features
- Good test coverage
- Clear documentation
- Clever solutions

**Recommendations:**
- Prioritized list of changes to make
- Optional improvements for future consideration
- Testing suggestions
- Documentation needs

## Best Practices
- **Be Constructive**: Focus on improving code quality, not criticizing
- **Be Specific**: Reference exact file locations and line numbers
- **Prioritize**: Focus on high-impact issues first
- **Consider Context**: Take into account project constraints and deadlines
- **Balance**: Acknowledge good practices alongside issues
- **Explain Why**: Don't just point out problems, explain the reasoning

## Example Output Structure

```
# Branch Review: feature/user-authentication

## Executive Summary
- **Files Changed**: 12 files (+487, -123 lines)
- **Overall Risk**: 🟡 Medium
- **Critical Issues**: 2 high, 5 medium, 8 low
- **Recommendation**: Request changes before merge

## High Priority Issues

### 🔴 Security: Hardcoded API Key
**Location**: `src/config/api.ts:15`
**Impact**: Credentials exposed in version control
**Suggestion**: Move to environment variables and add to .gitignore

### 🔴 Error Handling: Unhandled Promise Rejection
**Location**: `src/services/auth.ts:45`
**Impact**: Application could crash on auth failure
**Suggestion**: Add try-catch block and proper error logging

## Medium Priority Issues

### 🟡 Performance: N+1 Query Pattern
**Location**: `src/controllers/user.ts:78-92`
**Impact**: Database performance degrades with user count
**Suggestion**: Use join or batch loading instead of loop queries

## Low Priority Issues

### 🟢 Code Quality: Complex Function
**Location**: `src/utils/validation.ts:23-67`
**Impact**: Hard to test and maintain
**Suggestion**: Break into smaller, focused functions

## Positive Highlights
- Excellent test coverage for auth service (95%)
- Clear documentation in README
- Good use of TypeScript types for API contracts

## Recommendations
1. Fix security issues before merge (critical)
2. Add error handling for all async operations
3. Consider refactoring complex validation logic
4. Add integration tests for authentication flow
```
