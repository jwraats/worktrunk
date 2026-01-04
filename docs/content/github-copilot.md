+++
title = "GitHub Copilot Integration"
weight = 24

[extra]
group = "Reference"
+++

Worktrunk works seamlessly with GitHub Copilot, both the IDE integration and the standalone CLI. Use worktrees to run multiple Copilot agents in parallel, each with its own isolated working directory.

## Using Copilot CLI with Worktrunk

[GitHub Copilot CLI](https://github.com/github/copilot-cli) brings Copilot's AI coding agent directly to your terminal. Combined with Worktrunk, you can spin up multiple parallel agents easily.

### Create worktree and start Copilot CLI

```bash
wt switch -c -x copilot feature-branch
```

This creates a new worktree, switches to it, and launches Copilot CLI in one command.

### Run multiple agents in parallel

```bash
# Terminal 1
wt switch -c -x copilot feature-auth

# Terminal 2
wt switch -c -x copilot feature-api

# Terminal 3
wt switch -c -x copilot bugfix-login
```

Each agent works in its own worktree, so they don't step on each other's changes.

### Monitor progress

```bash
wt list
```

Shows all worktrees with their status, uncommitted changes, and position relative to main.

### Clean up after merging

```bash
wt merge  # squash, rebase, merge, clean up
```

## Agent Skills

The Worktrunk skill (`.github/skills/worktrunk/`) teaches Copilot how to:

- Set up LLM-powered commit message generation
- Configure project hooks (post-create, pre-merge, etc.)
- Customize worktree paths and templates
- Troubleshoot configuration issues

### Example Prompts

Ask Copilot to help with Worktrunk configuration:

- "Set up LLM commit messages for this project"
- "Add a post-create hook to install npm dependencies"
- "Configure pre-merge to run tests before merging"
- "Show me how to use template variables in hooks"

## Project Instructions

The repository includes `.github/copilot-instructions.md` which gives Copilot context about:

- Project structure and technology stack
- Development guidelines and testing commands
- Terminology and conventions
- Available configuration options

## IDE Integration

For Copilot in VS Code or other IDEs:

```bash
wt switch -c feature-branch
# Then open the worktree in your IDE with Copilot enabled
```

Each worktree can have an independent Copilot session in a separate IDE window.

## Comparison with Claude Code Integration

| Feature | Claude Code | GitHub Copilot |
|---------|-------------|----------------|
| CLI launch | `wt switch -c -x claude` | `wt switch -c -x copilot` |
| Configuration skill | ✅ `.claude-plugin/skills/` | ✅ `.github/skills/` |
| Activity tracking | ✅ 🤖/💬 markers | — |
| Statusline | ✅ `wt list statusline --claude-code` | — |
| Plugin marketplace | ✅ Available | — |

Both integrations share the same skill content — the configuration guidance and reference documentation is identical.

## Installation

### Prerequisites

- A [GitHub Copilot subscription](https://github.com/features/copilot) (Pro, Pro+, Business, or Enterprise)
- Node.js v22 or later
- npm v10 or later

### Installing Copilot CLI

**Using npm (recommended):**

```bash
npm install -g @github/copilot
```

**Using Homebrew (macOS/Linux):**

```bash
brew install github/copilot/copilot
```

### Authentication

After installation, authenticate with your GitHub account:

```bash
copilot
# Use /login to authenticate via browser
```

Alternatively, set a personal access token with `GH_TOKEN` or `GITHUB_TOKEN` environment variable.

For complete installation instructions and troubleshooting, see the [official Copilot CLI documentation](https://docs.github.com/en/copilot/concepts/agents/about-copilot-cli).

### Agent Skills

GitHub Copilot automatically detects skills in `.github/skills/` — no manual installation required. Just ensure you have:

1. Copilot enabled in your IDE or CLI
2. The repository cloned with the `.github/skills/` directory

## Further Reading

- [About GitHub Copilot CLI](https://docs.github.com/en/copilot/concepts/agents/about-copilot-cli) — Official documentation
- [GitHub Copilot CLI repository](https://github.com/github/copilot-cli) — Source code and issues
- [GitHub Copilot Agent Skills](https://github.blog/changelog/2025-12-18-github-copilot-now-supports-agent-skills/) — Skills announcement
- [VS Code Agent Skills](https://code.visualstudio.com/docs/copilot/customization/agent-skills) — IDE integration
