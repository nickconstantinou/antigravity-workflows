---
description: GitHub Operations (Branching, PRs, Issues)
---

# 🐙 Workflow: GitHub Operations

This workflow enforces a clean git history and efficient use of the GitHub CLI.

## 🛠️ Core Commands

### 1. Feature Branch Protocol
* **Branching**: `git checkout -b feat/[feature-name]`
* **Status**: `gh pr status`

### 2. Atomic Commits
* **Conventional Commits**: Use `feat:`, `fix:`, `docs:`, `chore:`, `refactor:`, `test:`.
* **Commit**: `git add . && git commit -m "<type>: <description>"`

### 3. Pull Request Management
* **Create PR**: `gh pr create --title "<type>: <title>" --body "<description>"`
* **Merge (Squash)**: `gh pr merge --squash --delete-branch`

### 4. Issue Tracking
* **Create Issue**: `gh issue create --title "[title]" --body "..."`
* **Close Issue**: `gh issue close [number]`

## 🛡️ Constraints
- **Security**: NEVER commit `.env` files.
- **Clean History**: Always use `--squash` when merging to keep `main` linear.
