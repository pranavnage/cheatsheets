# Git Cheatsheet

## Table of Contents

- [Git Basics](#git-basics)
- [Repository Management](#repository-management)
- [Branch Management](#branch-management)
- [Staging and Commits](#staging-and-commits)
- [Remote Operations](#remote-operations)
- [Merging and Rebasing](#merging-and-rebasing)
- [Tagging](#tagging)
- [Stashing](#stashing)
- [Logging and History](#logging-and-history)
- [Undoing Changes](#undoing-changes)
- [Configuration](#configuration)
- [Advanced Commands](#advanced-commands)
- [Workflows](#workflows)
- [Best Practices](#best-practices)

## Git Basics

| Command | Description |
|---------|-------------|
| `git --version` | Show Git version |
| `git help` | Show help |
| `git help <command>` | Show help for specific command |
| `git status` | Show working tree status |
| `git status -s` | Show short status |
| `git status --porcelain` | Show porcelain status |

## Repository Management

### Initialization

| Command | Description |
|---------|-------------|
| `git init` | Initialize new repository |
| `git init --bare` | Initialize bare repository |
| `git clone <url>` | Clone repository |
| `git clone <url> <dir>` | Clone to specific directory |
| `git clone --depth 1 <url>` | Shallow clone (latest commit only) |
| `git clone --branch <branch> <url>` | Clone specific branch |
| `git clone --recursive <url>` | Clone with submodules |

### Repository Information

| Command | Description |
|---------|-------------|
| `git remote` | List remotes |
| `git remote -v` | List remotes with URLs |
| `git remote show <remote>` | Show remote details |
| `git remote add <name> <url>` | Add remote |
| `git remote remove <name>` | Remove remote |
| `git remote rename <old> <new>` | Rename remote |
| `git remote set-url <name> <url>` | Change remote URL |

## Branch Management

### Basic Branch Operations

| Command | Description |
|---------|-------------|
| `git branch` | List local branches |
| `git branch -r` | List remote branches |
| `git branch -a` | List all branches |
| `git branch -v` | List branches with last commit |
| `git branch --merged` | List merged branches |
| `git branch --no-merged` | List unmerged branches |
| `git branch <name>` | Create branch |
| `git branch -d <name>` | Delete branch (safe) |
| `git branch -D <name>` | Force delete branch |
| `git branch -m <old> <new>` | Rename branch |

### Branch Navigation

| Command | Description |
|---------|-------------|
| `git checkout <branch>` | Switch to branch |
| `git checkout -b <name>` | Create and switch to branch |
| `git checkout -b <name> <start-point>` | Create branch from specific point |
| `git switch <branch>` | Switch to branch (newer syntax) |
| `git switch -c <name>` | Create and switch to branch |
| `git switch -` | Switch to previous branch |

### Remote Branch Operations

| Command | Description |
|---------|-------------|
| `git checkout -b <branch> origin/<branch>` | Create local branch from remote |
| `git branch -u origin/<branch>` | Set upstream branch |
| `git branch --set-upstream-to=origin/<branch>` | Set upstream (alternative) |
| `git push -u origin <branch>` | Push and set upstream |
| `git push origin --delete <branch>` | Delete remote branch |
| `git branch -dr origin/<branch>` | Delete remote tracking branch |

## Staging and Commits

### Staging Files

| Command | Description |
|---------|-------------|
| `git add <file>` | Stage specific file |
| `git add .` | Stage all changes |
| `git add -A` | Stage all changes (including deletions) |
| `git add -u` | Stage modified files only |
| `git add -p` | Stage interactively (patch mode) |
| `git add -i` | Interactive staging |
| `git restore --staged <file>` | Unstage file |
| `git reset HEAD <file>` | Unstage file (older syntax) |

### Committing

| Command | Description |
|---------|-------------|
| `git commit` | Commit staged changes |
| `git commit -m "message"` | Commit with message |
| `git commit -am "message"` | Stage and commit all changes |
| `git commit --amend` | Amend last commit |
| `git commit --amend -m "new message"` | Amend with new message |
| `git commit --amend --no-edit` | Amend without changing message |
| `git commit --allow-empty -m "message"` | Create empty commit |
| `git commit --fixup <commit>` | Create fixup commit |
| `git commit --squash <commit>` | Create squash commit |

## Remote Operations

### Fetching and Pulling

| Command | Description |
|---------|-------------|
| `git fetch` | Fetch from default remote |
| `git fetch <remote>` | Fetch from specific remote |
| `git fetch --all` | Fetch from all remotes |
| `git fetch --prune` | Fetch and remove stale references |
| `git pull` | Fetch and merge |
| `git pull --rebase` | Fetch and rebase |
| `git pull --ff-only` | Pull only if fast-forward |
| `git pull origin <branch>` | Pull specific branch |

### Pushing

| Command | Description |
|---------|-------------|
| `git push` | Push to default remote |
| `git push origin <branch>` | Push specific branch |
| `git push -u origin <branch>` | Push and set upstream |
| `git push --all` | Push all branches |
| `git push --tags` | Push all tags |
| `git push --force` | Force push (dangerous) |
| `git push --force-with-lease` | Safer force push |
| `git push --delete origin <branch>` | Delete remote branch |

## Merging and Rebasing

### Merging

| Command | Description |
|---------|-------------|
| `git merge <branch>` | Merge branch into current |
| `git merge --no-ff <branch>` | Force merge commit |
| `git merge --ff-only <branch>` | Only fast-forward merge |
| `git merge --squash <branch>` | Squash merge |
| `git merge --abort` | Abort current merge |
| `git merge --continue` | Continue merge after resolving conflicts |

### Rebasing

| Command | Description |
|---------|-------------|
| `git rebase <branch>` | Rebase current branch onto another |
| `git rebase -i <commit>` | Interactive rebase |
| `git rebase --continue` | Continue rebase after resolving conflicts |
| `git rebase --skip` | Skip current commit during rebase |
| `git rebase --abort` | Abort rebase |
| `git rebase --onto <new-base> <old-base> <branch>` | Rebase onto different base |

### Interactive Rebase Commands

| Command | Description |
|---------|-------------|
| `pick` | Use commit as-is |
| `reword` | Use commit but edit message |
| `edit` | Use commit but stop for amending |
| `squash` | Combine with previous commit |
| `fixup` | Like squash but discard message |
| `drop` | Remove commit |

## Tagging

| Command | Description |
|---------|-------------|
| `git tag` | List all tags |
| `git tag -l "v1.*"` | List tags matching pattern |
| `git tag <name>` | Create lightweight tag |
| `git tag -a <name> -m "message"` | Create annotated tag |
| `git tag -a <name> <commit>` | Tag specific commit |
| `git show <tag>` | Show tag information |
| `git tag -d <name>` | Delete local tag |
| `git push origin <tag>` | Push specific tag |
| `git push --tags` | Push all tags |
| `git push origin --delete <tag>` | Delete remote tag |

## Stashing

| Command | Description |
|---------|-------------|
| `git stash` | Stash current changes |
| `git stash push -m "message"` | Stash with message |
| `git stash -u` | Stash including untracked files |
| `git stash -a` | Stash including ignored files |
| `git stash list` | List all stashes |
| `git stash show` | Show stash contents |
| `git stash show -p` | Show stash patch |
| `git stash pop` | Apply and remove latest stash |
| `git stash apply` | Apply stash without removing |
| `git stash apply stash@{2}` | Apply specific stash |
| `git stash drop` | Delete latest stash |
| `git stash drop stash@{2}` | Delete specific stash |
| `git stash clear` | Delete all stashes |

## Logging and History

### Basic Logging

| Command | Description |
|---------|-------------|
| `git log` | Show commit history |
| `git log --oneline` | Compact one-line format |
| `git log --graph` | Show branch graph |
| `git log --all` | Show all branches |
| `git log --decorate` | Show branch/tag names |
| `git log -n 10` | Limit to last 10 commits |
| `git log --since="2 weeks ago"` | Commits since date |
| `git log --until="2023-01-01"` | Commits until date |
| `git log --author="name"` | Commits by author |
| `git log --grep="pattern"` | Search commit messages |

### Advanced Logging

| Command | Description |
|---------|-------------|
| `git log --stat` | Show file statistics |
| `git log --shortstat` | Show summary statistics |
| `git log --name-only` | Show only file names |
| `git log --name-status` | Show file names with status |
| `git log -p` | Show patch (diff) |
| `git log --follow <file>` | Follow file renames |
| `git log <branch1>..<branch2>` | Commits in branch2 not in branch1 |
| `git log --left-right <branch1>...<branch2>` | Show commits unique to each branch |

### Formatting

| Command | Description |
|---------|-------------|
| `git log --pretty=format:"%h %s"` | Custom format |
| `git log --format="%h - %an, %ar : %s"` | Custom format with author |
| `git log --pretty=fuller` | Full format |

### Other History Commands

| Command | Description |
|---------|-------------|
| `git show <commit>` | Show commit details |
| `git show --stat <commit>` | Show commit statistics |
| `git diff` | Show unstaged changes |
| `git diff --staged` | Show staged changes |
| `git diff <commit1> <commit2>` | Compare commits |
| `git diff <branch1>..<branch2>` | Compare branches |
| `git blame <file>` | Show line-by-line author |
| `git annotate <file>` | Alternative to blame |

## Undoing Changes

### Working Directory

| Command | Description |
|---------|-------------|
| `git restore <file>` | Restore file from index |
| `git checkout -- <file>` | Restore file (older syntax) |
| `git restore --source=<commit> <file>` | Restore from specific commit |
| `git clean -n` | Show what would be removed |
| `git clean -f` | Remove untracked files |
| `git clean -fd` | Remove untracked files and directories |
| `git clean -fx` | Remove untracked and ignored files |

### Commits

| Command | Description |
|---------|-------------|
| `git reset --soft HEAD~1` | Undo commit, keep changes staged |
| `git reset HEAD~1` | Undo commit, keep changes unstaged |
| `git reset --hard HEAD~1` | Undo commit and changes |
| `git reset --soft <commit>` | Reset to commit, keep changes staged |
| `git reset <commit>` | Reset to commit, keep changes unstaged |
| `git reset --hard <commit>` | Reset to commit, discard changes |
| `git revert <commit>` | Create commit that undoes another |
| `git revert -n <commit>` | Revert without committing |

### Advanced Undoing

| Command | Description |
|---------|-------------|
| `git reflog` | Show reference log |
| `git reflog expire --expire=90.days.ago --all` | Clean old reflog entries |
| `git fsck --lost-found` | Find lost commits |
| `git cherry-pick <commit>` | Apply specific commit |
| `git cherry-pick -n <commit>` | Cherry-pick without committing |

## Configuration

### Global Configuration

| Command | Description |
|---------|-------------|
| `git config --list` | Show all configuration |
| `git config --global --list` | Show global configuration |
| `git config --system --list` | Show system configuration |
| `git config --local --list` | Show repository configuration |
| `git config user.name "Your Name"` | Set username |
| `git config user.email "you@example.com"` | Set email |
| `git config --global user.name "Your Name"` | Set global username |
| `git config --global user.email "you@example.com"` | Set global email |

### Editor and Tools

| Command | Description |
|---------|-------------|
| `git config --global core.editor "code --wait"` | Set VS Code as editor |
| `git config --global core.editor "vim"` | Set Vim as editor |
| `git config --global merge.tool vimdiff` | Set merge tool |
| `git config --global diff.tool vimdiff` | Set diff tool |
| `git config --global core.autocrlf true` | Handle line endings (Windows) |
| `git config --global core.autocrlf input` | Handle line endings (Unix) |

### Aliases

| Command | Description |
|---------|-------------|
| `git config --global alias.st status` | Create status alias |
| `git config --global alias.co checkout` | Create checkout alias |
| `git config --global alias.br branch` | Create branch alias |
| `git config --global alias.ci commit` | Create commit alias |
| `git config --global alias.unstage 'reset HEAD --'` | Create unstage alias |
| `git config --global alias.last 'log -1 HEAD'` | Create last commit alias |
| `git config --global alias.visual '!gitk'` | Create visual alias |

## Advanced Commands

### Submodules

| Command | Description |
|---------|-------------|
| `git submodule add <url> <path>` | Add submodule |
| `git submodule init` | Initialize submodules |
| `git submodule update` | Update submodules |
| `git submodule update --init --recursive` | Init and update recursively |
| `git submodule foreach <command>` | Run command in each submodule |
| `git submodule status` | Show submodule status |

### Worktrees

| Command | Description |
|---------|-------------|
| `git worktree add <path> <branch>` | Add new worktree |
| `git worktree list` | List all worktrees |
| `git worktree remove <worktree>` | Remove worktree |
| `git worktree prune` | Clean up worktree references |

### Bisect (Binary Search)

| Command | Description |
|---------|-------------|
| `git bisect start` | Start bisect session |
| `git bisect bad` | Mark current commit as bad |
| `git bisect good <commit>` | Mark commit as good |
| `git bisect reset` | End bisect session |
| `git bisect run <script>` | Automate bisect with script |

### Archive

| Command | Description |
|---------|-------------|
| `git archive --format=zip HEAD > archive.zip` | Create zip archive |
| `git archive --format=tar.gz --prefix=project/ HEAD \| gzip > archive.tar.gz` | Create tar.gz archive |

### Maintenance

| Command | Description |
|---------|-------------|
| `git gc` | Garbage collection |
| `git gc --aggressive` | Aggressive garbage collection |
| `git prune` | Remove unreachable objects |
| `git fsck` | File system check |
| `git count-objects -v` | Show repository size |

## Workflows

### Feature Branch Workflow

```bash
# Create feature branch
git checkout -b feature/new-feature

# Work on feature
git add .
git commit -m "Add new feature"

# Push feature branch
git push -u origin feature/new-feature

# Create pull request (via GitHub/GitLab)
# After review and approval, merge via web interface

# Clean up local branch
git checkout main
git pull
git branch -d feature/new-feature
```

### Gitflow Workflow

```bash
# Initialize gitflow
git flow init

# Start new feature
git flow feature start new-feature

# Finish feature
git flow feature finish new-feature

# Start release
git flow release start 1.0.0

# Finish release
git flow release finish 1.0.0

# Start hotfix
git flow hotfix start hotfix-1.0.1

# Finish hotfix
git flow hotfix finish hotfix-1.0.1
```

### Forking Workflow

```bash
# Fork repository on GitHub/GitLab
# Clone your fork
git clone https://github.com/yourusername/repo.git

# Add upstream remote
git remote add upstream https://github.com/originalowner/repo.git

# Create feature branch
git checkout -b feature/new-feature

# Work and commit
git add .
git commit -m "Add feature"

# Push to your fork
git push origin feature/new-feature

# Create pull request
# Keep fork synchronized
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

## Best Practices

### Commit Messages

```
feat: add user authentication
fix: resolve memory leak in parser
docs: update API documentation
style: format code according to style guide
refactor: simplify user validation logic
test: add unit tests for user service
chore: update dependencies

# Conventional Commits format:
# type(scope): description
# 
# [optional body]
#
# [optional footer]
```

### Branch Naming

```
feature/user-authentication
bugfix/memory-leak-parser
hotfix/security-vulnerability
release/v1.2.0
```

### .gitignore Examples

```gitignore
# Dependencies
node_modules/
vendor/

# Build outputs
dist/
build/
*.o
*.so

# Environment files
.env
.env.local
.env.production

# IDE files
.vscode/
.idea/
*.swp
*.swo

# OS files
.DS_Store
Thumbs.db

# Logs
*.log
logs/
```

---

**Pro Tips:**

- Always pull before pushing to avoid conflicts
- Use meaningful commit messages that explain the "why"
- Commit early and often with logical units of work
- Use branches for features, never commit directly to main
- Review changes before committing with `git diff --staged`
- Use `git stash` to temporarily save work when switching branches
- Set up SSH keys for easier authentication
- Use `git rebase` instead of `git merge` for cleaner history
- Always test before committing
- Use `.gitignore` to exclude unnecessary files
- Tag releases for easy reference
- Use `git blame` to understand code history
- Keep repositories clean with regular `git gc`
- Use descriptive branch names
- Never force push to shared branches
- Use pull requests/merge requests for code review
- Keep commits atomic (one logical change per commit)
- Use `git bisect` to find problematic commits
- Backup important work with remotes
- Learn to read and understand Git logs
