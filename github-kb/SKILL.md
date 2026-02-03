---
name: github-kb
description: GitHub Knowledge Base for managing and querying local GitHub repositories. Use when the user mentions GitHub, a repo, or a repository. This skill handles searching local repositories, downloading new repositories, querying repository contents, using gh command for GitHub API operations like issues and PRs, and analyzing code in cloned repositories.
---

# GitHub Knowledge Base

## Overview

Manage a local cache of GitHub repositories for rapid analysis and querying. This skill maintains a repository index at `@/home/logan/Projects/skills/github-kb/CLAUDE.md` with one-sentence summaries for quick reference.

## Local Repository Path

**Default location**: `/home/logan/Projects/skills/github-kb`

If this directory doesn't exist, prompt the user for the correct path and update this skill accordingly.

## Workflow

### 1. When User Mentions GitHub/Repo/Repository

1. Check if the query references a specific repository (e.g., "anthropics/claude-code", "the cli-tool repo")
2. Search the local directory at `/home/logan/Projects/skills/github-kb/` for matching repositories
3. Read `@/home/logan/Projects/skills/github-kb/CLAUDE.md` for repository summaries

### 2. Repository Found Locally

- Analyze the user's query against the local repository
- Use Read/Grep/Glob tools to examine code, docs, and structure
- Answer the user's question based on local content

### 3. Repository Not Found

1. Offer to clone the repository using `git clone`
2. Clone to `/home/logan/Projects/skills/github-kb/<repo-name>/`
3. Update `@/home/logan/Projects/skills/github-kb/CLAUDE.md` with repository summary

## Using the gh Command

Leverage the GitHub CLI for remote queries:

```bash
# Search repositories
gh search repos <query>

# View issues/PRs
gh issue list --repo <owner/repo>
gh pr list --repo <owner/repo>

# View specific issue/PR
gh issue view <number> --repo <owner/repo>
gh pr view <number> --repo <owner/repo>

# Search code
gh search code <query> --repo <owner/repo>
```

## CLAUDE.md Format

Maintain the repository index with this structure:

```markdown
## Repository Index

### [owner/repo](https://github.com/owner/repo)
One-sentence summary of the repository's purpose and key functionality.
```

## Example Queries

- "What does the anthropics/claude-code repo do?"
- "Show me the issues in facebook/react"
- "Clone the rust-lang/rust repository"
- "How does the authentication work in the cli-tool repo?"
- "Search GitHub for repositories about skill-based systems"
