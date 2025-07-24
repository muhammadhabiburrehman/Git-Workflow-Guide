# Git Workflow Guide

A complete guide for Git workflow from creating a branch to pushing changes, including common errors and their solutions.

## Creating and Managing Branches

### Create a New Branch
```bash
# Create and switch to new branch
git checkout -b feature-name

# Or create branch from specific branch
git checkout -b new-branch existing-branch
```

### Switch Between Branches
```bash
# Switch to existing branch
git checkout branch-name

# Or using newer syntax
git switch branch-name
```

### Check Current Branch
```bash
# See all branches and current one (marked with *)
git branch

# See remote branches too
git branch -a
```

---

## Making Changes and Committing

### Check What Changed
```bash
# See what files are modified/added/deleted
git status

# See actual changes in files
git diff
```

### Add Changes
```bash
# Add all changes
git add .

# Add specific file
git add filename.txt

# Add multiple specific files
git add file1.txt file2.txt
```

### Commit Changes
```bash
# Commit with message
git commit -m "Your commit message"

# Add and commit in one step
git commit -am "Your commit message"
```

---

## Pushing Changes

### First Time Push (New Branch)
```bash
# Push and set upstream
git push --set-upstream origin branch-name

# For autoSetupRemote
git config --global push.autoSetupRemote true

```

### Regular Push (After First Time)
```bash
git push
```

---

## Common Errors and Solutions

### ❌ Error 1: "fatal: The current branch has no upstream branch"

**What it means:** Your local branch doesn't have a remote branch to push to.

**Solution 1 (For this branch only):**
```bash
git push --set-upstream origin branch-name
```
*This creates remote branch and connects your local branch to it.*

**Solution 2 (One-time global fix):**
```bash
git config --global push.autoSetupRemote true
git push
```
*This configures Git to automatically create remote branches for all future branches.*

---

### ❌ Error 2: "Please tell me who you are" (when committing)

**What it means:** Git doesn't know your identity.

**Solution:**
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```
*This sets your identity for all Git repositories.*

---

### ❌ Error 3: "nothing added to commit but untracked files present"

**What it means:** You have new files but haven't added them to staging.

**Solution:**
```bash
git add .
git commit -m "Your message"
```
*Add all files to staging, then commit.*

---

### ❌ Error 4: "Your branch is ahead of 'origin/main' by X commits"

**What it means:** You have local commits that aren't pushed yet.

**Solution:**
```bash
git push
```
*Push your commits to remote.*

---

### ❌ Error 5: "Updates were rejected because the remote contains work"

**What it means:** Someone else pushed changes to the same branch.

**Solution:**
```bash
git pull
# Fix any conflicts if they appear
git push
```
*Pull the latest changes first, then push yours.*

---

### ❌ Error 6: "fatal: not a git repository"

**What it means:** You're not in a Git repository folder.

**Solution:**
```bash
# Initialize new repository
git init

# Or navigate to correct folder
cd your-project-folder
```

---

### ❌ Error 7: Merge Conflicts

**What it means:** Git can't automatically merge changes.

**Solution:**
1. Open conflicted files
2. Look for `<<<<<<<`, `=======`, `>>>>>>>>` markers
3. Edit the file to keep what you want
4. Remove the conflict markers
5. Add and commit:
```bash
git add .
git commit -m "Resolved merge conflict"
```

---

## Useful Commands Reference

### Status and Information
```bash
git status              # See current state
git log                 # See commit history
git log --oneline       # Compact commit history
git branch             # List branches
git remote -v          # See remote repositories
```

### Undoing Changes
```bash
git restore filename    # Undo changes in file (before adding)
git reset HEAD~1       # Undo last commit (keep changes)
git reset --hard HEAD~1 # Undo last commit (lose changes)
```

### Branch Management
```bash
git branch -d branch-name    # Delete local branch
git push origin --delete branch-name  # Delete remote branch
git checkout main           # Switch to main branch
git merge feature-branch    # Merge branch into current branch
```

### Remote Management
```bash
git remote add origin https://github.com/username/repo.git  # Add remote
git clone https://github.com/username/repo.git            # Clone repository
git pull                    # Get latest changes from remote
git fetch                   # Download remote changes (don't merge)
```

---

## Quick Reference Workflow

### For New Feature:
```bash
# 1. Create branch
git checkout -b feature-name

# 2. Make your changes in files

# 3. Check what changed
git status

# 4. Add changes
git add .

# 5. Commit
git commit -m "Add new feature"

# 6. Push (first time)
git push --set-upstream origin feature-name

# 7. For future pushes
git push
```

### For Existing Branch:
```bash
# 1. Switch to branch
git checkout branch-name

# 2. Make changes

# 3. Add and commit
git add .
git commit -m "Update feature"

# 4. Push
git push
```

---

## Pro Tips 💡

1. **Always check `git status`** before adding/committing
2. **Use descriptive commit messages** like "Fix login button bug" instead of "fix"
3. **Pull before pushing** if working with others: `git pull` then `git push`
4. **Use branches** for features, don't work directly on main
5. **Configure auto-setup once**: `git config --global push.autoSetupRemote true`

---

## Emergency Commands 🆘

```bash
# Forgot to switch branch before making changes?
git stash                    # Save changes temporarily
git checkout correct-branch  # Switch to right branch
git stash pop               # Get your changes back

# Want to completely start over?
git reset --hard HEAD       # Lose all local changes
git clean -fd               # Remove untracked files

# Accidentally committed to wrong branch?
git reset --soft HEAD~1     # Undo commit, keep changes
git checkout correct-branch # Switch to right branch
git add . && git commit -m "Your message"  # Commit to right branch
```

---

**Remember:** When in doubt, `git status` is your friend! It tells you exactly what state you're in and often suggests what to do next.
