---
name: read-only
description: "Activates read-only mode for Claude Code. Use this skill whenever the user wants to analyze, explore, audit, or understand a project WITHOUT making any modifications. Ideal for sessions with --dangerously-skip-permissions where the user wants to guarantee nothing will be changed. Also useful when the user says things like 'just let me look', 'don't change anything', 'read mode', 'read only', 'just analyze', 'I want to understand the code without touching it', or 'explore only'."
---

# Read-Only Mode

You are operating in read-only mode. The goal is to let the user explore and analyze the project freely, using `--dangerously-skip-permissions` to avoid being interrupted by confirmation prompts, while guaranteeing that **no file or resource will be modified**.

This matters because the user trusts you to respect this constraint — if you modify something, you break that trust, and the user may lose work or end up with the project in an unexpected state.

## Core rule

Before executing any action, ask yourself:

> "Does this action create, modify, or delete any file, resource, or system state?"

- **Yes** → Do not execute. Explain what you would do and suggest the user does it manually.
- **No** → Proceed.
- **Unsure** → Do not execute.

## What you can use

| Tool | Examples |
|---|---|
| **Read** | Read any file |
| **Glob** | Search files by pattern |
| **Grep** | Search content within files |
| **Agent** (Explore) | Deep codebase exploration |
| **Bash** (read-only) | `git log`, `git diff`, `git status`, `git blame`, `git show`, `ls`, `wc`, `file`, `head`, `tail`, `find`, `tree`, `pwd`, `env`, `type`, `where` |
| **WebSearch / WebFetch** | Search and fetch web content |
| **Read-only MCP tools** | MCP tools that only read data |

## What you cannot use

**Blocked tools:** Edit, Write, NotebookEdit.

**Bash commands that alter state** — this list is not exhaustive, use your judgment:

- **Delete:** `rm`, `rmdir`, `del`, `unlink`
- **Move/rename:** `mv`, `rename`
- **Create/copy:** `cp`, `touch`, `mkdir`, `mktemp`
- **Write to file:** any use of `>`, `>>` redirecting to a file, `tee` to a file, `cat > file`
- **Edit in-place:** `sed -i`, `awk -i inplace`
- **Permissions:** `chmod`, `chown`, `chattr`, `icacls`
- **Git with side effects:** `git commit`, `git push`, `git reset`, `git checkout --`, `git stash`, `git merge`, `git rebase`, `git cherry-pick`, `git branch -d/-D`, `git tag -d`, `git clean`
- **Install packages:** `npm install`, `pip install`, `mvn install`, `dotnet add`, `cargo install`
- **Download to disk:** `curl -o`, `curl -O`, `wget`, `Invoke-WebRequest -OutFile`
- **Extract/compress:** `tar -x`, `unzip`, `7z x`
- **Docker with state:** `docker run`, `docker exec`, `docker rm`, `docker build`
- **PowerShell writes:** `New-Item`, `Set-Content`, `Out-File`, `Remove-Item`, `Copy-Item`, `Move-Item`

Pipes (`|`) are allowed when both sides are read-only (e.g., `git log | head`). They are prohibited when the destination writes to disk.

## How to respond to modification requests

When the user asks to modify something, don't just refuse — help as much as you can:

1. Explain that read-only mode is active
2. Show exactly what would be done, as a diff or pseudocode
3. Suggest the command the user can run manually

Example:
> I'm in read-only mode, so I can't edit files directly. Here's the change I would make:
> ```diff
> - const timeout = 5000;
> + const timeout = 10000;
> ```
> To apply this, you can edit `src/config.ts` at line 42, or run again without read-only mode.

## What you can actively do

- Read and analyze any file in the project
- Search for patterns, classes, functions, strings
- Explore the project's structure and architecture
- Answer questions about the code
- Generate analyses and reports (displayed as text in the conversation)
- Review code and suggest improvements (verbally)
- Explain flows, business logic, dependencies
- Compare branches, commits, differences
- Audit quality, security, performance

## Session start

When invoked, display:

```
READ-ONLY MODE ACTIVATED

I can read, search, and analyze the project.
I cannot create, edit, or delete any files.

How can I help?
```

If arguments were provided, start working on them immediately.
