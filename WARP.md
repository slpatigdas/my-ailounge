# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## What this repo is
This repository is primarily a **Markdown-based “agent library”** used with **Gemini CLI** (management/planning) and **opencode CLI** (structured agent execution). The core deliverables here are:
- Agent definitions and governance docs in `agents/`
- Global agent behavior rules in `AGENTS.md`
- opencode agent configuration in `.opencode/agent/*.md`

There is currently **no application build/lint/test pipeline at the repo root** (no root `package.json`, `pyproject.toml`, etc.). Most changes are edits to Markdown files.

## About Warp (warp.dev)
Warp is an **Agentic Development Environment**: a modern terminal/editor that can run commands *and* operate via natural-language prompts.

Key Warp concepts that matter when working in this repo:
- **Warp AI**: Warp auto-detects whether you’re typing a command or a prompt, and can enter richer code-generation flows when it detects a coding task.
- **Agents / multi-agent workflows**: you can run multiple agents in parallel; they will notify you when they need input.
- **Warp Drive**: shared notebooks/workflows/environment variables; Warp may use this as context for AI-assisted work.

Docs: https://docs.warp.dev/

## Common commands
### Repo navigation / quick orientation
```powershell
# list top-level structure
Get-ChildItem -Force -Name

# inspect an agent folder
Get-ChildItem -Force -Name agents\jira
```

### opencode CLI plugin deps (local)
The `.opencode/` folder is a small Node/Bun workspace used to pin `@opencode-ai/plugin`.

```powershell
# install/update .opencode dependencies
Push-Location .opencode
bun install
Pop-Location
```

Notes:
- `.opencode/package.json` has only dependencies (no scripts), so there are **no repo-provided** `bun test` / `bun lint` commands.

## High-level architecture
### 1) Global agent governance
- `README.md` explains the repo’s intent and tool/model usage split (Gemini for management/coordinating; ChatGPT/Anthropic for coding/reviews).
- `AGENTS.md` defines cross-cutting rules for all agents (deterministic when possible, declare intent, prefer read over write, Python-first execution, human-in-the-loop).

When unsure which behavior constraints apply, read `AGENTS.md` first.

### 2) Agent modules in `agents/`
Each integration lives under `agents/<name>/` and is expected to contain:
- `README.md`: integration pointers/links
- `AGENTS.md`: integration-specific rules and operating constraints
- `TODO.md`: the agent’s working queue (usually the “source of truth” list the agent maintains)

Example:
- `agents/jira/TODO.md` is the current Jira ticket queue.

### 3) opencode agent configuration in `.opencode/agent/`
Files under `.opencode/agent/*.md` are **opencode agent definitions** (YAML frontmatter + prompt body). They typically:
- Specify runtime settings (model, temperature, enabled tools)
- Point to the authoritative working files under `agents/*` (e.g., which `TODO.md` to maintain)

In this repo, `.opencode/agent/jira-alignment.md` describes how the Jira agent should curate `agents/jira/TODO.md` and what Jira project constraints to apply.

## Repo-specific “gotchas” (worth checking before edits)
- `README.md` mentions a `tools/` directory, but it is not currently present in the repo.
- `agents/jira/AGENTS.md` references `.opencode/agent/jira-manager.md` and `agents/jira-manager/TODO.md`, but the repo currently contains `.opencode/agent/jira-alignment.md` and `agents/jira/TODO.md`. If you are wiring up automation, reconcile these paths/names first.
