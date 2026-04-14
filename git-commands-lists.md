# Git Commands Cheatsheet 🐙

## 🚀 Basic Setup

```bash
git config --global user.name "Your Name"
git config --global user.email "you@email.com"

git init                        # New repo
git clone <URL>                 # Clone repo
git clone <URL> --depth 1       # Shallow clone (faster, last commit only)
```

---

## 📦 Staging & Committing

```bash
git status                      # Check what changed
git add .                       # Stage all changes
git add <file>                  # Stage specific file
git add -p                      # Stage changes chunk by chunk (interactive)

git commit -m "message"         # Commit
git commit -am "message"        # Stage + Commit (tracked files only)

# Amend last commit (message ya files change karo)
git commit --amend -m "new message"   # Message change karo
git commit --amend --no-edit          # Message same rakho, files add karo
```

---

## 🌿 Branches

```bash
git branch                      # List local branches
git branch -a                   # List all branches (remote bhi)
git branch <name>               # Create branch
git checkout <name>             # Switch branch
git checkout -b <name>          # Create + Switch branch
git switch -c <name>            # Same as above (modern way)

git branch -d <name>            # Delete branch (safe)
git branch -D <name>            # Force delete branch
git branch -m <old> <new>       # Rename branch
```

---

## 🔀 Merge & Rebase

```bash
# Merge
git merge <branch>              # Merge branch into current
git merge --no-ff <branch>      # Merge with commit (no fast-forward)
git merge --abort               # Abort merge (conflict pe)

# Rebase
git rebase <branch>             # Rebase current branch onto <branch>
git rebase main                 # Rebase onto main (most common)
git rebase --abort              # Abort rebase
git rebase --continue           # Continue after fixing conflict

# Interactive Rebase (commits squash/reorder/edit karo)
git rebase -i HEAD~3            # Last 3 commits interactive
# Options inside interactive:
# pick   = keep commit as is
# reword = change commit message
# squash = merge into previous commit
# drop   = delete commit
```

---

## ⬆️ Push & Pull

```bash
git push origin <branch>                  # Push branch
git push -u origin <branch>              # Push + set upstream
git push --force origin <branch>         # Force push ⚠️ (history overwrite)
git push --force-with-lease origin <branch>  # Safer force push ✅ (fails if someone else pushed)

git pull                                  # Fetch + Merge
git pull --rebase                         # Fetch + Rebase (cleaner history)
git fetch origin                          # Fetch only (don't merge)
```

---

## ⏪ Undo & Reset

```bash
# Unstage file
git restore --staged <file>

# Discard local changes (file wapas last commit pe)
git restore <file>

# Reset (commits undo karo)
git reset HEAD~1                # Last commit undo, changes staged rakhega
git reset --soft HEAD~1         # Last commit undo, changes staged rakhega
git reset --mixed HEAD~1        # Last commit undo, changes unstaged honge (default)
git reset --hard HEAD~1         # Last commit undo, changes bhi delete ⚠️

# Force reset to remote (local sab kuch remote se match karo)
git reset --hard origin/main    # ⚠️ Local changes sab gone

# Revert (safe undo - new commit banata hai)
git revert <commit-hash>        # Public branches pe ye use karo
```

---

## 🔍 Logs & History

```bash
git log                          # Full log
git log --oneline                # One line per commit
git log --oneline --graph        # Graph with branches
git log --oneline -10            # Last 10 commits
git log --author="Yash"          # Filter by author
git log <file>                   # Log for specific file

git diff                         # Unstaged changes
git diff --staged                # Staged changes
git diff <branch1> <branch2>     # Branch comparison
```

---

## 🗄️ Stash

```bash
git stash                        # Stash current changes
git stash push -m "message"      # Stash with name
git stash list                   # List all stashes
git stash pop                    # Apply latest stash + delete it
git stash apply stash@{0}        # Apply specific stash (keep it)
git stash drop stash@{0}         # Delete specific stash
git stash clear                  # Delete ALL stashes ⚠️
```

---

## 🏷️ Tags

```bash
git tag                          # List tags
git tag v1.0.0                   # Create lightweight tag
git tag -a v1.0.0 -m "message"   # Annotated tag
git push origin v1.0.0           # Push specific tag
git push origin --tags           # Push all tags
git tag -d v1.0.0                # Delete local tag
git push origin --delete v1.0.0  # Delete remote tag
```

---

## 🧹 Cleanup

```bash
git clean -n                     # Preview what will be deleted
git clean -fd                    # Delete untracked files + folders ⚠️

git remote prune origin          # Remove stale remote branches
git fetch --prune                # Fetch + remove stale branches
```

---

## ⚡ Power Combos

```bash
# Oops wrong branch pe commit kar diya!
git checkout correct-branch
git cherry-pick <commit-hash>    # Us commit ko yahan lao

# Last commit ka author/date change karo
git commit --amend --reset-author

# Specific file ko previous version pe le jao
git checkout <commit-hash> -- <file>

# Remote ka URL change karo
git remote set-url origin <new-URL>

# See who changed what line (blame karo 😄)
git blame <file>
```
