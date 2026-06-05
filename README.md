# my-daily-agent

A shareable standalone opencode workspace configuration for a daily development agent.

## Included

- `.opencode/agents/my-daily-agent.md` — standalone daily agent definition
- `.opencode/opencode.jsonc` — shareable daily workflow template
- `.opencode/opencode.json` — minimal local default-agent config
- `.opencode/commands/` — daily-oriented command workflow files
- `rules-cn.md` — Chinese interaction and safety rules referenced by the config

## What this repository is

This repository is a **template** version of a personal daily opencode setup.
It keeps the daily workflow structure, MCP layout, commands, and rules, while replacing machine-specific values with environment-variable placeholders.

## Before use

You should set or adapt the following environment variables on your own machine:

- `OPENCODE_FILESYSTEM_ROOT`
- `GITHUB_PAT`
- `BRAVE_API_KEY`
- `OBSIDIAN_API_KEY`
- `OBSIDIAN_BASE_URL`
- `CHROMA_DB_PATH`
- `ANYSEARCH_API_KEY`
- `KB_PYTHON`
- `KB_MCP_SERVER`
- `KB_ROOT`
- `KB_CONFIG`

## Notes

- Secrets are **not** included in this repository.
- Some local MCP servers depend on tools you install separately.
- The included config is a shareable template, not a guarantee that every MCP works out of the box on another machine.
- The local knowledge base integration has been generalized to `kb` instead of project-specific `SecKB` / `CVEKB` naming.

## Usage

Open this folder as an opencode workspace:

`C:\Users\Administrator\Desktop\Agent\my-daily-agent`

The workspace-local config defaults to the `my-daily-agent` agent.
