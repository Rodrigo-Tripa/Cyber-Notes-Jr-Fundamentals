# Git Cheat Sheet

## Repository Setup

```bash
git init
git clone <repository-url>

git remote -v
git remote add origin <repository-url>
```

## Configuration

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

git config --list
git config --global --list
```

## Status and Inspection

```bash
git status
git log
git log --oneline
git log --graph --oneline --all

git show <commit>
git diff
git diff --staged
```

## Staging

```bash
git add file.txt
git add directory/
git add .
git add -A
```

Unstage a file:

```bash
git restore --staged file.txt
```

## Commits

```bash
git commit -m "message"
git commit -am "message"
```

View a specific commit:

```bash
git show <commit>
```

## Branches

```bash
git branch
git branch <branch>

git switch <branch>
git switch -c <new-branch>

git checkout <branch>
git checkout -b <new-branch>
```

Delete a branch:

```bash
git branch -d <branch>
git branch -D <branch>
```

## Merging

```bash
git switch main
git merge <branch>
```

If conflicts occur:

```bash
git status
```

Resolve the conflicting files, then:

```bash
git add <resolved-file>
git commit
```

Abort the merge:

```bash
git merge --abort
```

## Remote Repositories

```bash
git remote -v

git fetch
git fetch origin

git pull
git push
git push -u origin <branch>
```

## Reset

```bash
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
```

`--soft` keeps changes staged.

`--mixed` keeps changes in the working tree but unstaged.

`--hard` discards changes in the working tree and should be used carefully.

## Restore

```bash
git restore file.txt
git restore --staged file.txt
```

Restore a file to its state from a specific commit:

```bash
git restore --source=<commit> file.txt
```

## Revert

Create a new commit that reverses an existing commit:

```bash
git revert <commit>
```

Prefer `git revert` for commits that have already been shared with others.

## Stash

```bash
git stash
git stash push -m "description"

git stash list
git stash pop
git stash apply
git stash drop
```

## Tags

```bash
git tag
git tag v1.0.0
git show v1.0.0

git push origin v1.0.0
git push --tags
```

## Removing Files

```bash
git rm file.txt
git rm -r directory/
```

Stop tracking a file while keeping it locally:

```bash
git rm --cached file.txt
```

## History Search

```bash
git log --all -- file.txt
git log -S "text"
git log -G "regex"
git blame file.txt
```

## Comparing Changes

```bash
git diff
git diff HEAD
git diff HEAD~1

git diff branch1..branch2
```

## Cleaning Untracked Files

Preview:

```bash
git clean -n
```

Remove untracked files:

```bash
git clean -f
```

Remove untracked files and directories:

```bash
git clean -fd
```

## Conventional Commits

```text
feat:     New functionality
fix:      Bug fix
docs:     Documentation
refactor: Code restructuring
test:     Tests
chore:    Maintenance
```

Examples:

```bash
git commit -m "feat: add authentication"
git commit -m "fix: correct input validation"
git commit -m "docs: expand networking notes"
git commit -m "refactor: simplify authentication flow"
```

## Common Workflow

```bash
git status
git pull

git add <files>
git commit -m "message"
git push
```
