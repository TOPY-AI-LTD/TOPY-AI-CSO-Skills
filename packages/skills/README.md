# @topy-ai/cso-skills

The [TOPY.AI](https://topy.ai) AI CSO skills for **Claude Code, Codex, Pi, Cursor, Gemini CLI, OpenCode, GitHub Copilot, Windsurf** and other coding agents: 19 skills that look after a small company's security the way a senior CSO would — new CVEs and end-of-life dates for everything it runs, no secrets in code, active checks only on domains you have verified, every skill and MCP server vetted before it is trusted, incidents with a timeline, and a weekly security report to the founder and the CEO — powered by the TOPY.AI CSO MCP server.

```sh
npx @topy-ai/cso-skills install                  # this project, for the agents set up here
npx @topy-ai/cso-skills install -g               # your user: every project
npx @topy-ai/cso-skills install -g -a codex,pi   # pick the agents
npx @topy-ai/cso-skills install --mcp            # also add the CSO MCP server to .mcp.json (Claude Code)
```

Pi users can also install it as a Pi package: `pi install npm:@topy-ai/cso-skills`.

## Agents

| Agent | Skills | MCP server |
|---|---|---|
| **Claude Code** | `npx @topy-ai/cso-skills install -a claude`, or the plugin marketplace | `install --mcp` writes `.mcp.json`, or the `topy-ai-cso` plugin |
| **Codex** | `npx @topy-ai/cso-skills install -a codex`, or `codex plugin marketplace add TOPY-AI-LTD/TOPY-AI-CSO-Skills` | `codex mcp add topy-cso --url https://topy.ai/mcp/cso` |
| **Pi** | `pi install npm:@topy-ai/cso-skills` | `npx -y @topy-ai/cso-mcp` |
| **Cursor, Gemini CLI, OpenCode, Copilot, Windsurf and others** | `npx @topy-ai/cso-skills install -a <agent>` | Remote URL `https://topy.ai/mcp/cso` |
| **Claude.ai, Claude Desktop, ChatGPT** | Upload a skill folder as a zip | Custom connector `https://topy.ai/mcp/cso` |

`npx @topy-ai/cso-skills agents` prints the supported agents and marks the ones found on your machine. The install record lives in `<project>/.topy-ai/cso-skills-install.json`, or `~/.config/topy/cso-skills-install.json` for the user scope (`TOPY_HOME`). Commit the project's skill folders and `.topy-ai/` to share the skills with your team.

## Choose skills

```sh
npx @topy-ai/cso-skills list                                              # every skill, by category
npx @topy-ai/cso-skills install --category vulnerabilities,web           # categories (or plugin names like topy-ai-cso-vulnerabilities)
npx @topy-ai/cso-skills install topy-cso-secrets topy-cso-weekly-report       # single skills
```

Categories: `core` (connect, setup, goals, daily watch — always installed), `vulnerabilities`, `code`, `web`, `agents`, `response`.

## The MCP server

`https://topy.ai/mcp/cso` — the same TOPY.AI account and sign-in (OAuth) as the AI CEO, CFO and COO; only the accounts that own the OneMan operation see its findings. For scheduled agents, an API key as `TOPY_API_KEY`.

```sh
npx @topy-ai/cso-skills mcp -g     # prints the commands for Claude Code, Codex, Gemini CLI, Cursor and Pi
```

## Update and remove

```sh
npx @topy-ai/cso-skills@latest update                      # this project (-g for your user)
npx @topy-ai/cso-skills remove topy-cso-threat-model       # or --all
npx @topy-ai/cso-skills doctor
```

Files you edited are kept on update and remove unless you pass `--force`. Every command accepts `--dry-run`. The CEO, CFO, COO and CSO skill packages install side by side; each keeps its own record.

## Without the installer

```sh
git clone --depth 1 https://github.com/TOPY-AI-LTD/TOPY-AI-CSO-Skills.git
mkdir -p ~/.agents/skills
cp -R TOPY-AI-CSO-Skills/plugins/*/skills/* ~/.agents/skills/
```

Or `npx skills add TOPY-AI-LTD/TOPY-AI-CSO-Skills -a <agent>`. Claude Code plugins: `/plugin marketplace add TOPY-AI-LTD/TOPY-AI-CSO-Skills`, then `/plugin install topy-ai-cso-all@topy-ai-cso`.

Source, skills index and changelog: [TOPY-AI-LTD/TOPY-AI-CSO-Skills](https://github.com/TOPY-AI-LTD/TOPY-AI-CSO-Skills).
