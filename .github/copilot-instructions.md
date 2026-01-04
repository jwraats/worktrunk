# GitHub Copilot Instructions for Worktrunk

This repository contains Worktrunk, a CLI for git worktree management designed for running AI agents in parallel.

## Project Overview

Worktrunk simplifies git worktree operations with three core commands:
- `wt switch` — Switch between worktrees (with `-c` to create, `-x` to execute commands)
- `wt list` — List worktrees with status, CI info, and more
- `wt merge` — Squash, rebase, merge, and clean up in one command
- `wt remove` — Clean up worktree and branch

## Technology Stack

- **Language**: Rust (edition 2024, rust-version 1.89)
- **Build**: Cargo
- **Testing**: `cargo test` with insta for snapshot testing
- **Linting**: `pre-commit run --all-files`

## Development Guidelines

### Running Tests

```bash
# Run all tests + lints
cargo run -- hook pre-merge --yes

# Unit tests only
cargo test --lib --bins

# Integration tests
cargo test --test integration
```

### Code Quality

- All external command execution must go through `shell_exec::run()`
- Command output must stream in real-time, never buffer
- Never add `#[allow(dead_code)]` — either use the code or remove it
- Prefer failure over silent data loss

### Terminology

- **main worktree** — the primary worktree (original git directory)
- **default branch** — the branch name (main, master, etc.)
- **target** — destination branch for merge/rebase operations

## Configuration Files

- **User config**: `~/.config/worktrunk/config.toml` — personal preferences
- **Project config**: `.config/wt.toml` — team-wide hooks and automation

## Available Skills

Use the `worktrunk` skill (in `.github/skills/worktrunk/`) for:
- Setting up LLM-powered commit messages
- Configuring project hooks (post-create, pre-merge, etc.)
- Troubleshooting configuration issues

## Helpful Commands

```bash
wt --help                    # Full command reference
wt <command> --help          # Detailed command help
wt config list               # View current configuration
wt config create             # Create initial user config
```

## Further Reading

- Documentation: https://worktrunk.dev
- Repository: https://github.com/max-sixty/worktrunk
