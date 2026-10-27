<div align="center">
  <p>
    <img src="https://www.topy.ai/long_logo.svg" alt="TOPY AI CSO" width="420" />
  </p>
  <h1>TOPY AI CSO Skills</h1>
  <p><strong>19 skills that make your coding agent a small company's AI CSO: new CVEs and end-of-life dates for everything you run, no secrets in code, headers, TLS and safe scans of the domains you have verified, every skill and MCP server vetted before it is trusted, incident timelines and a weekly security report to the founder and the CEO — on the TOPY.AI CSO MCP server.</strong></p>
  <p>
    <a href="https://www.npmjs.com/package/@topy-ai/cso-skills"><img alt="npm" src="https://img.shields.io/npm/v/@topy-ai/cso-skills?style=for-the-badge&color=ff1212" /></a>
    <a href="https://github.com/TOPY-AI-LTD/TOPY-AI-CSO-Skills/blob/main/LICENSE"><img alt="MIT License" src="https://img.shields.io/badge/License-MIT-111827?style=for-the-badge" /></a>
    <a href="https://topy.ai/developers"><img alt="MCP" src="https://img.shields.io/badge/MCP-topy.ai%2Fmcp%2Fcso-0f172a?style=for-the-badge" /></a>
  </p>
</div>

---

The AI CSO is goal-first. It keeps five standing goals — **no open critical exposure** (anything on CISA KEV or critical
with a fix is fixed within days), **zero secrets in code**, **verified-only active checks**, **nothing trusted unvetted**
(every new skill, MCP server and package checked first) and **every incident with a timeline** — and every skill below
exists to move one of them.

- **Core** (`topy-ai-cso`): connect, first setup (inventory, domain verification, host consent), the CSO's goals, the daily watch.
- **Vulnerabilities**: are we affected by this CVE, dependencies and supply chain, end of life, vetting a package before install.
- **Code**: secrets (rotate first, then remove), unsafe code patterns, a STRIDE threat model and the OWASP ASVS checklist.
- **Web**: domain verification, headers and TLS, a safe scan of a verified site.
- **Agents**: vet a skill or MCP server before it is installed (the App Factory gate), and audit your own MCP server.
- **Response**: incident timelines, a fix plan with fix-risk tiers T1–T4, the weekly security report.

The safety model comes from Maggie Security and does not bend: the CSO **never changes a server, firewall or website**
(fix and protection plans are for a person to review and apply), **never scans a domain you have not verified**, reads a
server only after **you grant consent yourself in a terminal** (an agent cannot), leaves checks of sites you don't control
to a person (never a routine), never uses offensive techniques and **never prints a secret**. Changes take two calls — a
preview, then your yes.

## Install

```sh
npx @topy-ai/cso-skills install                  # this project, for the agents set up here
npx @topy-ai/cso-skills install -g --mcp         # your user, plus the MCP server
npx @topy-ai/cso-skills install --category vulnerabilities,web
npx @topy-ai/cso-skills list
```

Claude Code plugins: `/plugin marketplace add TOPY-AI-LTD/TOPY-AI-CSO-Skills`, then `/plugin install topy-ai-cso-all@topy-ai-cso`.
Codex: `codex plugin marketplace add TOPY-AI-LTD/TOPY-AI-CSO-Skills`. Pi: `pi install npm:@topy-ai/cso-skills`.
See the [installer README](packages/skills/README.md).

## Connect TOPY.AI

`https://topy.ai/mcp/cso` — OAuth with your TOPY.AI account (the same one as the AI CEO, CFO and COO). Only the accounts
that own the OneMan operation see its findings.

| Client | How |
|---|---|
| Claude, ChatGPT (web, desktop) | custom connector `https://topy.ai/mcp/cso` |
| Claude Code | `claude mcp add --transport http topy-cso https://topy.ai/mcp/cso` |
| Codex | `codex mcp add topy-cso --url https://topy.ai/mcp/cso` |
| Clients that only start a command | `npx -y @topy-ai/cso-mcp` after `npx @topy-ai/cso-mcp login` |
| Terminal and scripts | `npm i -g @topy-ai/cso-cli && cso-cli login` |

Server checks (`host-quick`, `host-audit`) and passive checks of sites you don't control (`public-check`) are not on
topy.ai: they need a person on OneMan, with host consent granted in a terminal.

## How the skills fit together

```
topy-cso-connect ─▶ topy-cso-setup (inventory · domain verify · consent) ─▶ topy-cso-goals
        │
   daily 06:17: topy-cso-daily-watch ─▶ topy-cso-cve-response ─▶ topy-cso-incident ─▶ topy-cso-fix-plan
        │                               topy-cso-dependencies · topy-cso-end-of-life
   weekly Mon 07:23: topy-cso-weekly-report ─▶ the founder (email) and the CEO
        │
   before code ships: topy-cso-secrets · topy-cso-code-scan · topy-cso-threat-model
   web (verified domains): topy-cso-domain-verify ─▶ topy-cso-web-checks ─▶ topy-cso-web-scan
   before you trust it: topy-cso-package-vet · topy-cso-vet-skill · topy-cso-mcp-audit
```

Try: *"Anything new I should worry about?"*, *"Are we affected by CVE-2026-…?"*, *"Did a key leak?"*,
*"Is this MCP server safe to install?"*, *"Send the weekly security report"*

## Packages

| Package | What it is |
|---|---|
| [`@topy-ai/cso-skills`](https://www.npmjs.com/package/@topy-ai/cso-skills) | This installer (Claude Code, Codex, Pi, Cursor, Gemini CLI, …) |
| [`@topy-ai/cso-mcp`](https://www.npmjs.com/package/@topy-ai/cso-mcp) | The CSO MCP server as a local stdio server (forwards to `https://topy.ai/mcp/cso`) |
| [`@topy-ai/cso-cli`](https://www.npmjs.com/package/@topy-ai/cso-cli) | The AI CSO on the command line |

## Repository structure

```
plugins/
  topy-ai-cso/                   core skills + .mcp.json (Claude Code) and mcp.json (Codex)
  topy-ai-cso-vulnerabilities/   topy-ai-cso-code/   topy-ai-cso-web/
  topy-ai-cso-agents/            topy-ai-cso-response/
  topy-ai-cso-all/               bundle that depends on all six
.claude-plugin/marketplace.json     Claude Code marketplace
.agents/plugins/marketplace.json    Codex marketplace
skills.json                         machine-readable catalogue
packages/skills/                    the @topy-ai/cso-skills installer
```

The skills are generated from a source catalogue kept next to TOPY.AI's MCP server; the build checks every tool a
skill names against the CSO server's tool list. Please open an issue rather than editing a `SKILL.md`.

## License

MIT © TOPY AI LTD. Privacy: [topy.ai/privacy](https://topy.ai/privacy).

## Skills

<!-- skills:start -->

**19 skills in 6 plugins**, plus the `topy-ai-cso-all` bundle. Generated from the source catalogue: please open an issue rather than editing a `SKILL.md`.

### AI CSO core (MCP) · `topy-ai-cso`

| Skill | Tier | What it does |
|---|---|---|
| [`topy-cso-connect`](plugins/topy-ai-cso/skills/topy-cso-connect/SKILL.md) | core | Connect the TOPY CSO MCP server and check what applies: the project's stack, verified domains, granted hosts, tools and feeds. |
| [`topy-cso-daily-watch`](plugins/topy-ai-cso/skills/topy-cso-daily-watch/SKILL.md) | core | Every morning: new CVEs, advisories and end-of-life dates for everything the company runs, matched to the stack — quiet unless something new needs a person. |
| [`topy-cso-goals`](plugins/topy-ai-cso/skills/topy-cso-goals/SKILL.md) | core | The AI CSO's standing goals and its status report for the CEO: open critical exposure, secrets in code, verified-only checks, vetted skills and MCP servers, incident timelines. |
| [`topy-cso-setup`](plugins/topy-ai-cso/skills/topy-cso-setup/SKILL.md) | core | First run for a new company or site: inventory the stack, verify each domain you own, and explain host consent — so every later check is allowed and complete. |

### Vulnerabilities & supply chain · `topy-ai-cso-vulnerabilities`

| Skill | Tier | What it does |
|---|---|---|
| [`topy-cso-cve-response`](plugins/topy-ai-cso-vulnerabilities/skills/topy-cso-cve-response/SKILL.md) | connected | A named CVE or advisory: are we affected, where, how urgent, and the response plan — with an incident timeline from start to close. |
| [`topy-cso-dependencies`](plugins/topy-ai-cso-vulnerabilities/skills/topy-cso-dependencies/SKILL.md) | connected | Known vulnerabilities in every lockfile ecosystem and in JavaScript copied into the site, prioritised, with the fixed versions. |
| [`topy-cso-end-of-life`](plugins/topy-ai-cso-vulnerabilities/skills/topy-cso-end-of-life/SKILL.md) | connected | Runtimes, databases, web servers and operating systems that stopped (or will soon stop) getting security fixes, and what to upgrade to. |
| [`topy-cso-package-vet`](plugins/topy-ai-cso-vulnerabilities/skills/topy-cso-package-vet/SKILL.md) | connected | Before adding a package: known vulnerabilities and malicious-package reports for that exact version, and a clear install / pin / don't install. |

### Code & secrets · `topy-ai-cso-code`

| Skill | Tier | What it does |
|---|---|---|
| [`topy-cso-code-scan`](plugins/topy-ai-cso-code/skills/topy-cso-code-scan/SKILL.md) | connected | Unsafe code patterns before they ship — injection, unsafe deserialisation, personal data in logs, weak crypto — with the safe pattern for each. |
| [`topy-cso-secrets`](plugins/topy-ai-cso-code/skills/topy-cso-secrets/SKILL.md) | connected | Keys, tokens and passwords in the code, its git history and the build output — and the rotate-first fix for each. |
| [`topy-cso-threat-model`](plugins/topy-ai-cso-code/skills/topy-cso-threat-model/SKILL.md) | connected | A STRIDE threat model of the system and an OWASP ASVS checklist filled from the findings — what could go wrong and how far we meet the standard. |

### Web surface · `topy-ai-cso-web`

| Skill | Tier | What it does |
|---|---|---|
| [`topy-cso-domain-verify`](plugins/topy-ai-cso-web/skills/topy-cso-domain-verify/SKILL.md) | connected | Prove the company controls a domain (DNS TXT record or a token file) before any active check — the CSO never scans a site that isn't verified. |
| [`topy-cso-web-checks`](plugins/topy-ai-cso-web/skills/topy-cso-web-checks/SKILL.md) | connected | Grade a verified site's HTTP security headers and cookies (A+ to F) and its TLS (protocols, certificate trust and expiry), with the exact fix for each. |
| [`topy-cso-web-scan`](plugins/topy-ai-cso-web/skills/topy-cso-web-scan/SKILL.md) | connected | A safe, rate-limited vulnerability scan (known flaws, exposed files, misconfigurations) of a site the company has verified — never exploitation. |

### Agent & MCP security · `topy-ai-cso-agents`

| Skill | Tier | What it does |
|---|---|---|
| [`topy-cso-mcp-audit`](plugins/topy-ai-cso-agents/skills/topy-cso-mcp-audit/SKILL.md) | connected | OWASP MCP checks on the company's own MCP tool registry: read-only hints, destructive tools behind confirmation, scopes, audit logging and hosts it may call. |
| [`topy-cso-vet-skill`](plugins/topy-ai-cso-agents/skills/topy-cso-vet-skill/SKILL.md) | connected | Before a skill, plugin or MCP server is installed or published: prompt-injection, data exfiltration, over-broad permissions and risky tools — the App Factory security gate. |

### Response & reporting · `topy-ai-cso-response`

| Skill | Tier | What it does |
|---|---|---|
| [`topy-cso-fix-plan`](plugins/topy-ai-cso-response/skills/topy-cso-fix-plan/SKILL.md) | connected | Turn the findings into a reviewed runbook — each action tagged T1 (batch-safe) to T4 (stage first) — that a person reviews and runs. The CSO never applies it. |
| [`topy-cso-incident`](plugins/topy-ai-cso-response/skills/topy-cso-incident/SKILL.md) | connected | Record a security incident or CVE response from start to close — what happened, every step and who did it — so nothing is lost and the report writes itself. |
| [`topy-cso-weekly-report`](plugins/topy-ai-cso-response/skills/topy-cso-weekly-report/SKILL.md) | connected | Every Monday: what is open by priority, what was fixed, what changed in the stack, and at most three actions — for the Founder by email and for the CEO. |

<!-- skills:end -->
