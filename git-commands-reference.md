# Comprehensive Git Commands Reference

## Table of Contents
1. [Initial Setup](#initial-setup)
2. [Repository Operations](#repository-operations)
3. [Basic Workflow](#basic-workflow)
4. [Branch Management](#branch-management)
5. [Remote Repository Operations](#remote-repository-operations)
6. [Viewing History and Changes](#viewing-history-and-changes)
7. [Undoing Changes](#undoing-changes)
8. [Stashing](#stashing)
9. [Advanced Commands](#advanced-commands)
10. [Useful Aliases](#useful-aliases)
11. [Best Practices](#best-practices)

---

## Initial Setup

### Configure Git Identity
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```
Sets your name and email globally for Git. This information is used to identify you as the author of commits across all repositories.

### View Configuration
```bash
git config --list                    # View all configuration settings
git config user.name                 # View specific setting
git config --global --edit           # Edit global config file
```

### Set Default Branch Name
```bash
git config --global init.defaultBranch main
```

---

## Repository Operations

### Initialize and Clone
```bash
git init                             # Initialize new Git repository
git init <directory-name>            # Initialize Git repo in specific directory
git clone <repository-url>           # Clone remote repository
git clone <repository-url> <folder>  # Clone into specific folder
git clone --depth 1 <repository-url> # Shallow clone (latest commit only)
```

---

## Basic Workflow

### Check Status and Add Files
```bash
git status                           # Show repository status
git status -s                        # Short status format
git add <file(s)>                    # Add specific files to staging
git add .                            # Add all files in current directory
git add -A                           # Add all files (including deletions)
git add -u                           # Add only modified/deleted files
git add -p                           # Interactive staging (patch mode)
```

### Commit Changes
```bash
git commit -m "Commit message"       # Commit with message
git commit -am "Message"             # Add and commit modified files
git commit --amend                   # Modify last commit
git commit --amend -m "New message"  # Change last commit message
git commit --no-edit --amend         # Add changes to last commit without editing message
```

---

## Branch Management

### Create and Switch Branches
```bash
git branch                           # List local branches
git branch -a                        # List all branches (local + remote)
git branch -r                        # List remote branches
git branch <branch-name>             # Create new branch
git checkout <branch-name>           # Switch to branch
git checkout -b <branch-name>        # Create and switch to new branch
git switch <branch-name>             # Modern way to switch branches
git switch -c <branch-name>          # Create and switch to new branch (modern)
```

### Merge and Delete Branches
```bash
git merge <branch-name>              # Merge branch into current branch
git merge --no-ff <branch-name>      # Merge with no fast-forward
git merge --squash <branch-name>     # Squash merge
git branch -d <branch-name>          # Delete merged branch
git branch -D <branch-name>          # Force delete branch
git branch -m <old-name> <new-name>  # Rename branch
```

---

## Remote Repository Operations

### Remote Management
```bash
git remote -v                        # List remote repositories
git remote add <name> <url>          # Add remote repository
git remote remove <name>             # Remove remote
git remote rename <old> <new>        # Rename remote
git remote set-url <name> <new-url>  # Change remote URL
```

### Push and Pull
```bash
git push                             # Push to default remote/branch
git push <remote> <branch>           # Push to specific remote/branch
git push -u origin <branch>          # Push and set upstream
git push --force                     # Force push (dangerous!)
git push --force-with-lease          # Safer force push
git pull                             # Fetch and merge from remote
git pull --rebase                    # Pull with rebase instead of merge
git fetch                            # Fetch changes without merging
git fetch --all                      # Fetch from all remotes
```

---

## Viewing History and Changes

### View Commits and History
```bash
git log                              # Show commit history
git log --oneline                    # Compact one-line format
git log --graph                      # Show branch graph
git log --all --graph --oneline      # Visual representation of all branches
git log -p                           # Show patches (diffs) for each commit
git log --author="Name"              # Filter by author
git log --since="2 weeks ago"        # Filter by date
git log --grep="keyword"             # Search commit messages
git log <file>                       # Show commits for specific file
```

### View Differences
```bash
git diff                             # Changes in working directory vs staging
git diff --staged                    # Changes in staging vs last commit
git diff HEAD                        # Changes in working directory vs last commit
git diff <commit1> <commit2>         # Compare two commits
git diff <branch1>..<branch2>        # Compare branches
git show <commit-hash>               # Show specific commit details
```

---

## Undoing Changes

### Reset and Revert
```bash
git reset <file>                     # Unstage file (keep changes)
git reset                            # Unstage all files
git reset --soft HEAD~1              # Undo last commit, keep changes staged
git reset --mixed HEAD~1             # Undo last commit, unstage changes
git reset --hard HEAD~1              # Undo last commit, discard changes
git revert <commit-hash>             # Create new commit that undoes changes
git checkout -- <file>               # Discard changes in working directory
git restore <file>                   # Modern way to discard changes
git restore --staged <file>          # Unstage file (modern way)
```

### Clean Untracked Files
```bash
git clean -n                         # Show what would be deleted
git clean -f                         # Delete untracked files
git clean -fd                        # Delete untracked files and directories
```

---

## Stashing

### Basic Stashing
```bash
git stash                            # Stash current changes
git stash push -m "Description"      # Stash with message
git stash -u                         # Include untracked files
git stash --keep-index               # Stash but keep staged changes
```

### Managing Stashes
```bash
git stash list                       # List all stashes
git stash show                       # Show changes in latest stash
git stash show stash@{1}             # Show specific stash
git stash show -p                    # Show full diff of stash
```

### Applying and Removing Stashes
```bash
git stash apply                      # Apply latest stash (keep in stash list)
git stash apply stash@{1}            # Apply specific stash
git stash pop                        # Apply and remove latest stash
git stash pop stash@{1}              # Apply and remove specific stash
git stash drop                       # Delete latest stash
git stash drop stash@{1}             # Delete specific stash
git stash clear                      # Delete all stashes
```

---

## Advanced Commands

### Rebasing
```bash
git rebase <branch>                  # Rebase current branch onto another
git rebase -i HEAD~3                 # Interactive rebase last 3 commits
git rebase --continue                # Continue rebase after resolving conflicts
git rebase --abort                   # Cancel rebase operation
```

### Cherry Pick
```bash
git cherry-pick <commit-hash>        # Apply specific commit to current branch
git cherry-pick <commit1>..<commit2> # Apply range of commits
```

### Tagging
```bash
git tag                              # List tags
git tag <tag-name>                   # Create lightweight tag
git tag -a <tag-name> -m "Message"   # Create annotated tag
git tag -d <tag-name>                # Delete tag
git push origin <tag-name>           # Push tag to remote
git push origin --tags               # Push all tags
```

### Searching
```bash
git grep "search-term"               # Search for text in repository
git log -S "search-term"             # Search commits that added/removed text
git bisect start                     # Start binary search for bug
```

---

## Useful Aliases

Add these to your Git config for faster commands:

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

---

## Best Practices

### Commit Messages
- Use present tense ("Add feature" not "Added feature")
- Keep first line under 50 characters
- Use body to explain what and why, not how
- Reference issues and pull requests when applicable

### Branch Naming
- Use descriptive names: `feature/user-authentication`, `bugfix/login-error`
- Use lowercase and hyphens
- Include ticket numbers: `feature/JIRA-123-add-search`

### General Tips
- Commit often with small, logical changes
- Test before committing
- Pull frequently to stay up to date
- Use `.gitignore` for files that shouldn't be tracked
- Don't commit sensitive information (passwords, API keys)
- Use meaningful branch names and commit messages
- Review changes before committing with `git diff --staged`

### Useful .gitignore patterns
```
# Dependencies
node_modules/
*.log

# IDE files
.vscode/
.idea/
*.swp

# OS files
.DS_Store
Thumbs.db

# Build output
dist/
build/
*.min.js

# Environment files
.env
.env.local
```

---

## Emergency Commands

### When Things Go Wrong
```bash
git reflog                           # Show all Git operations (can recover lost commits)
git fsck --lost-found                # Find dangling commits
git reset --hard origin/main         # Reset to match remote (loses local changes!)
git clean -fd                        # Remove untracked files and directories
```

### Conflict Resolution
```bash
git status                           # See conflicted files
git mergetool                        # Open merge tool
git add <resolved-file>              # Mark conflict as resolved
git commit                           # Complete the merge
```

Remember: Git is powerful but can be dangerous. Always backup important work and understand what each command does before running it!