# Git Workflow Guide

## Overview
This document outlines the Git workflow for fixing validation benchmarks in this fork.

## Branch Strategy

### Main Branch
- `main` - Production-ready code, always deployable
- Protected branch, only merge via Pull Requests

### Feature/Fix Branches
Create a new branch for each benchmark you fix:

```bash
git checkout -b fix/xben-XXX-description
```

**Naming Convention:**
- `fix/xben-001-docker-build` - For fixing specific benchmark issues
- `fix/xben-002-mysql-connection` - Use lowercase, hyphens for spaces
- `feat/add-validation-script` - For new features (if needed)
- `docs/update-readme` - For documentation changes

## Workflow Steps

### 1. Start New Fix
```bash
# Ensure main is up to date
git checkout main
git pull origin main

# Create new branch for the fix
git checkout -b fix/xben-001-brief-description
```

### 2. Make Changes
- Fix the benchmark
- Update CHANGELOG.md with details
- Test the fix works

### 3. Commit Changes

Use **Conventional Commits** format:

```bash
git add .
git commit -m "fix(XBEN-001): brief description of what was fixed

- More detailed explanation if needed
- What was broken
- How it was fixed

Closes #issue-number (if applicable)"
```

**Commit Message Format:**
```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**
- `fix:` - Bug fix
- `feat:` - New feature
- `docs:` - Documentation changes
- `refactor:` - Code refactoring
- `test:` - Adding tests
- `chore:` - Maintenance tasks

**Examples:**
```bash
git commit -m "fix(XBEN-001): resolve docker-compose build failure

- Updated Dockerfile ARG syntax
- Fixed flag injection in entrypoint script
- Corrected mysql connection string"

git commit -m "fix(XBEN-002): fix mysql container health check

The health check was failing due to incorrect credentials.
Updated docker-compose.yml to use proper environment variables."

git commit -m "docs: update CHANGELOG for XBEN-001 and XBEN-002 fixes"
```

### 4. Push Changes
```bash
# First time pushing branch
git push -u origin fix/xben-001-brief-description

# Subsequent pushes
git push
```

### 5. Create Pull Request (Optional)
If you want to review before merging to main:
- Go to GitHub
- Create Pull Request from your branch to main
- Review changes
- Merge when ready

OR merge directly:
```bash
git checkout main
git merge fix/xben-001-brief-description
git push origin main
```

## Recommended Workflow Options

### Option A: Individual Branches (Recommended for Review)
- One branch per benchmark fix
- Easy to review each fix independently
- Can cherry-pick if needed
- Cleaner history

### Option B: Batch Branches
- One branch for multiple related fixes
- E.g., `fix/docker-compose-issues` for all docker-compose problems
- Faster but harder to review

### Option C: Direct to Main (Quick & Dirty)
- Work directly on main branch
- Commit frequently with good messages
- No PR overhead
- Suitable for personal forks with no collaboration

## Suggested Approach for This Project

Given you're working on 104 benchmarks, I recommend a **hybrid approach**:

1. **Create batches of 5-10 related fixes per branch**
   ```bash
   git checkout -b fix/xben-001-010-initial-fixes
   ```

2. **Commit after each individual fix**
   ```bash
   git add benchmarks/XBEN-001-24/
   git commit -m "fix(XBEN-001): description"
   
   git add benchmarks/XBEN-002-24/
   git commit -m "fix(XBEN-002): description"
   ```

3. **Update CHANGELOG.md at end of batch**
   ```bash
   git add CHANGELOG.md
   git commit -m "docs: update CHANGELOG for XBEN-001 through XBEN-010"
   ```

4. **Merge batch to main and push**
   ```bash
   git checkout main
   git merge fix/xben-001-010-initial-fixes
   git push origin main
   ```

## Quick Reference Commands

```bash
# Check current status
git status

# See what changed
git diff

# View commit history
git log --oneline --graph --decorate --all

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# See all branches
git branch -a

# Delete local branch
git branch -d fix/xben-001-description

# Delete remote branch
git push origin --delete fix/xben-001-description
```

## Tips

1. **Commit often** - Small, focused commits are better than large ones
2. **Write clear commit messages** - Your future self will thank you
3. **Test before committing** - Make sure the fix actually works
4. **Update CHANGELOG** - Keep it current as you go
5. **Push regularly** - Don't lose work, push to remote frequently
