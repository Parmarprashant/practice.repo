## Git and GitHub Commands Cheat Sheet

This repository contains notes about Git workflows. Below is a curated list of commonly used Git/GitHub commands, followed by a short list of commands commonly used while creating these notes. 

### Core Workflow
- `git init` — Initialize a new Git repository
- `git clone <url>` — Clone an existing repository
- `git status` — Show working tree status
- `git add <path>` / `git add .` — Stage changes
- `git restore --staged <path>` — Unstage a file
- `git commit -m "message"` — Commit staged changes
- `git commit --amend` — Amend the last commit
- `git diff` — Show unstaged changes
- `git diff --staged` — Show staged changes
- `git log --oneline --graph --decorate --all` — Compact, visual history

### Branching
- `git branch` — List local branches
- `git branch <name>` — Create a branch
- `git switch <name>` — Switch to a branch
- `git switch -c <name>` — Create and switch in one step
- `git checkout <name>` — Older alternative to switch
- `git branch -d <name>` — Delete merged branch locally
- `git branch -D <name>` — Force delete branch locally

### Merging and Rebasing
- `git merge <branch>` — Merge a branch into the current branch
- `git merge --no-ff <branch>` — Create a merge commit even if fast-forward is possible
- `git rebase <base>` — Rebase current branch onto another base
- `git rebase -i <base>` — Interactive rebase (reorder/squash/fixup)
- `git rebase --continue` / `--abort` — Continue or abort a rebase

### Resolving Conflicts
- Edit conflicting files, then: `git add <files>` and `git merge --continue` or `git rebase --continue`
- Abort if needed: `git merge --abort` or `git rebase --abort`

### Stash (Saving WIP)
- `git stash push -m "message"` — Stash tracked changes with a message
- `git stash list` — List stashes
- `git stash show -p stash@{n}` — Show a stash patch
- `git stash apply stash@{n}` — Apply a stash (keep it)
- `git stash pop` — Apply and drop the latest stash
- `git stash push -u` — Include untracked files

### Remotes and GitHub
- `git remote -v` — List remotes
- `git remote add origin <url>` — Add a remote
- `git fetch` — Fetch remote refs without merging
- `git pull` — Fetch and merge remote changes into current branch
- `git push` — Push current branch to its upstream
- `git push -u origin <branch>` — Push and set upstream
- `git push origin --delete <branch>` — Delete remote branch
- `git tag <vX.Y.Z>` — Create a lightweight tag
- `git tag -a <vX.Y.Z> -m "message"` — Create an annotated tag
- `git push origin <tag>` / `--tags` — Push tags

### Inspect and Navigate History
- `git show <ref>` — Show details about a ref (commit, tag)
- `git blame <file>` — Show last modification per line
- `git reflog` — Show reference log of branch tips (recover lost work)

### Fixing Mistakes (Safety First)
- `git restore <path>` — Restore file from index or commit
- `git restore --source=<ref> <path>` — Restore from a specific commit
- `git reset --soft <ref>` — Move HEAD; keep index and working tree
- `git reset --mixed <ref>` — Move HEAD and reset index (default)
- `git reset --hard <ref>` — Reset HEAD, index, and working tree (destructive)
- `git revert <commit>` — Create a new commit that undoes a commit

### Cleanup and Maintenance
- `git clean -n` — Preview removal of untracked files
- `git clean -fd` — Remove untracked files and directories
- `.gitignore` — Configure ignored files

### Configuration and Aliases
- `git config --global user.name "Your Name"`
- `git config --global user.email "you@example.com"`
- `git config --global init.defaultBranch main`
- Example aliases:
  - `git config --global alias.co switch`
  - `git config --global alias.br branch`
  - `git config --global alias.ci commit`
  - `git config --global alias.st status`
  - `git config --global alias.lg "log --oneline --graph --decorate --all"`

---

## Commands Commonly Used to Create These Notes

These reflect typical commands used while structuring and committing the materials in this repo:

1) Repository setup and structure
- `git init`
- `mkdir <topic>/notes` and add markdown files
- `git add .`
- `git commit -m "Add initial notes structure"`

2) Iterating on content
- `git status`
- `git add -p` (stage changes interactively)
- `git commit -m "Add notes for <topic>"`

3) Branching for topics and merging
- `git switch -c <topic-branch>`
- Edit/add files under `<topic>/notes/`
- `git add . && git commit -m "Add <topic> notes"`
- `git switch main`
- `git merge <topic-branch>`
- `git branch -d <topic-branch>`

4) Conflict practice and resolution (where relevant to lessons)
- `git merge <branch>` → resolve conflicts in editor
- `git add <resolved-files>`; `git merge --continue`

5) Remote/GitHub integration (if connected)
- `git remote add origin <repo-url>`
- `git push -u origin main`
- `git push -u origin <branch>`

6) History review and cleanup
- `git log --oneline --graph --decorate --all`
- `git stash push -m "wip"` and `git stash pop` (when parking WIP)
- `git tag -a v0.1 -m "first notes set"` (optional)

---

Tip: Use `git lg` (alias above) to keep an always-useful, compact view of your history.


