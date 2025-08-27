# GitHub CLI (gh) Cheatsheet

Essential GitHub CLI commands for daily development workflow.

## Authentication

| Command | Description |
|---------|-------------|
| `gh auth login` | Login to GitHub |
| `gh auth status` | Check login status |
| `gh auth logout` | Logout |

## Repositories

| Command | Description |
|---------|-------------|
| `gh repo create <name>` | Create repository |
| `gh repo create --private` | Create private repo |
| `gh repo clone <repo>` | Clone repository |
| `gh repo fork <repo>` | Fork repository |
| `gh repo view` | View current repo |
| `gh browse` | Open repo in browser |

## Issues

| Command | Description |
|---------|-------------|
| `gh issue create` | Create new issue |
| `gh issue list` | List issues |
| `gh issue view <number>` | View issue |
| `gh issue close <number>` | Close issue |
| `gh issue comment <number>` | Add comment |

## Pull Requests

| Command | Description |
|---------|-------------|
| `gh pr create` | Create pull request |
| `gh pr list` | List pull requests |
| `gh pr view <number>` | View PR details |
| `gh pr checkout <number>` | Checkout PR branch |
| `gh pr merge <number>` | Merge PR |
| `gh pr close <number>` | Close PR |
| `gh pr review <number> --approve` | Approve PR |
| `gh pr diff <number>` | Show PR diff |

## Releases

| Command | Description |
|---------|-------------|
| `gh release create <tag>` | Create release |
| `gh release list` | List releases |
| `gh release view <tag>` | View release |
| `gh release download <tag>` | Download release assets |

## Workflows (Actions)

| Command | Description |
|---------|-------------|
| `gh workflow list` | List workflows |
| `gh workflow run <name>` | Run workflow |
| `gh run list` | List workflow runs |
| `gh run view <id>` | View run details |
| `gh run logs <id>` | View run logs |

## Gists

| Command | Description |
|---------|-------------|
| `gh gist create <file>` | Create gist |
| `gh gist list` | List your gists |
| `gh gist view <id>` | View gist |
| `gh gist clone <id>` | Clone gist |

## Common Flags

| Flag | Description |
|------|-------------|
| `--web` | Open in web browser |
| `--draft` | Create as draft |
| `--title "text"` | Set title |
| `--body "text"` | Set body/description |
| `--assignee @me` | Assign to yourself |
| `--label <name>` | Add label |

## Quick Examples

```bash
# Create and clone new repo
gh repo create my-project --private --clone

# Create issue
gh issue create --title "Bug fix" --body "Description here"

# Create PR from current branch
gh pr create --title "Feature update" --body "Changes made"

# Quick PR review
gh pr view 123 --web

# Create release
gh release create v1.0.0 --title "Version 1.0" --notes "Release notes"
```

---

**Pro Tips:**

- Use `--web` to quickly open items in browser
- Set up aliases for frequently used commands
- Use `gh pr create` without flags for interactive mode
- Combine with git commands for complete workflow
