# 🔥 CopilotForge

> **Set up GitHub Copilot properly for any project — in one command.**

Without configuration, Copilot doesn't know your stack, your conventions, or your team's patterns. CopilotForge fixes that: it analyzes your codebase, finds the right instructions, agents, and skills for your stack, and installs them.

[![GitHub Copilot](https://img.shields.io/badge/GitHub%20Copilot-Agent%20Mode-blue?logo=github)](https://docs.github.com/en/copilot)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## What it does

Copilot works best when it understands your project. That means having:

- **`copilot-instructions.md`** — teaches Copilot your naming conventions, error handling patterns, testing approach, and architecture
- **Instructions** — stack-specific best practices (TypeScript strict mode, React patterns, pytest conventions…)
- **Agents & skills** — reusable workflows (code review, conventional commits, test generation…)
- **Prompts** — quick commands tailored to your workflow

CopilotForge discovers and installs all of these. It ships a **curated asset index** (no runtime fetching) pre-vetted from [github/awesome-copilot](https://github.com/github/awesome-copilot), the MCP Registry, and community repos.

---

## Commands

### `/forge` — Full setup for your project

Scans your project, scores your current Copilot setup, shows what's missing, and installs what you choose.

```
🔬 Analyzing your project...
   TypeScript | React | Vitest | GitHub Actions | Docker

📊 Current Copilot score: 2/10 (F)

🔍 Found 8 relevant assets:

  # │ Type        │ Name                      │ Trust
  1 │ instruction │ typescript-strict          │ ✅
  2 │ instruction │ react-patterns             │ ✅
  3 │ instruction │ vitest-testing             │ ✅
  4 │ agent       │ code-reviewer              │ ✅
  5 │ skill       │ conventional-commit        │ ✅
  6 │ mcp-server  │ github-mcp-server          │ ✅
  7 │ prompt      │ create-test                │ ✅
  8 │ instruction │ docker-best-practices      │ ✅

Which ones to install? (all / numbers / none)
> all

✅ 8 assets installed. Score: 9/10 (A)
```

After each install, `/forge` shows a before/after score comparison and asks if you want to continue improving. Stops automatically at 8+ or when nothing new is found.

### `/discover` — Find assets by description

Search the curated index by describing what you want, without scanning your project.

```
/discover EntraID authentication
/discover container deployment with Kubernetes
/discover React testing patterns
```

Works great when you know what you need but not which asset provides it.

### Generate instructions

The highest-impact single action. Scans your codebase and generates a `copilot-instructions.md` tailored to your project:

| Detects | Examples |
|---------|---------|
| Naming conventions | camelCase vars, kebab-case files, PascalCase types |
| Error handling | try-catch vs Result types, custom error classes |
| Import style | Named vs default, file extensions, sorted imports |
| Testing patterns | Framework, describe-it vs flat, mocking approach |
| Architecture | Layer-based vs feature-based, directory structure |
| Code style | Semicolons, quotes, indentation |

```
Generate instructions for this project
```

---

## Setup

**Step 1 — Clone and build (one time)**

```bash
git clone https://github.com/g-mercuri/copilot-forge.git ~/copilot-forge
cd ~/copilot-forge/mcp-server && npm install && npm run build
```

**Step 2 — Register as a global MCP server in VS Code**

`Ctrl+Shift+P` → **"MCP: Edit User Configuration"** → add:

```json
{
  "servers": {
    "copilot-forge": {
      "type": "stdio",
      "command": "node",
      "args": ["/absolute/path/to/copilot-forge/mcp-server/dist/index.js"]
    }
  }
}
```

**Step 3 — Open any project and run in Copilot Chat (Agent Mode)**

```
/forge
```

---

## Scoring

CopilotForge scores your Copilot setup from 0 to 10 and gives a letter grade. Use it to understand gaps and track progress.

| Category | Points |
|----------|--------|
| copilot-instructions.md | 0–2 |
| Coding standards | 0–1 |
| Error handling | 0–1 |
| Testing practices | 0–1 |
| Language instructions | 0–1 |
| Security/governance | 0–1 |
| Prompts | 0–1 |
| Agents/skills | 0–1 |
| Commit conventions | 0–1 |

---

## Enterprise: Org Standards

`apply_org_standards` pushes org-wide Copilot standards from your org's `.github` repo to any project. If no source is configured, it generates sensible defaults from detected codebase patterns.

---

## Security

Every asset in the index carries a trust badge:

| Badge | Level | Sources |
|-------|-------|---------|
| ✅ Verified | High | `github/awesome-copilot`, `microsoft/*` |
| ⚠️ Community | Medium | GitHub repos with reasonable activity |

All installs are preview-by-default. Additional protections: URL allowlist, SSRF blocking, content scanning, path traversal prevention, audit log at `~/.copilot-forge/audit.jsonl`.

---

## Reference

### MCP Tools

| Tool | Description |
|------|-------------|
| `discover_assets` | Analyze project stack + keyword search → ranked asset recommendations |
| `generate_instructions` | Scan codebase → generate `copilot-instructions.md` |
| `install_asset` | Safe batch installer with preview → confirm flow |
| `score_setup` | Score Copilot setup quality (0–10) with gaps and quick wins |
| `analyze_project` | Deep project scan (languages, frameworks, dependencies) |
| `apply_org_standards` | Apply org-wide standards from a `.github` repo |

### Covered stacks

TypeScript, JavaScript, Python, Go, Rust, Java, Kotlin, C#/.NET, Ruby, PHP, Swift, React, Next.js, Vue, Angular, Svelte, Django, FastAPI, Spring Boot, ASP.NET, Rails, Laravel, Docker, Kubernetes, Terraform, GitHub Actions, AWS, Azure, GCP, Vitest, Jest, pytest, and more.

### File structure

```
.github/
├── agents/copilot-forge.agent.md
├── prompts/
│   ├── forge.prompt.md        # /forge command
│   └── discover.prompt.md     # /discover command
└── skills/
    ├── agent-governance/
    └── conventional-commit/

mcp-server/src/
├── data/asset-index.ts          # Curated asset catalog
├── tools/                       # One file per MCP tool
├── security/                    # URL validation, content scanning, audit
├── core/                        # Scoring engine, git operations
└── analyzers/                   # Code pattern detection
```

---

## Development

```bash
cd mcp-server
npm run build    # tsc → dist/
npm run test     # vitest
npm run lint     # eslint
```

---

## Contributing

- 🐛 **Bugs** — Open an issue
- 💡 **New assets** — Suggest additions to the curated index
- 🔧 **PRs** — Improve tools, add curated assets, fix bugs
- 📖 **Docs** — Clearer instructions, more examples

Please open an issue before submitting large changes.

---

## License

[MIT License](LICENSE)

---

<p align="center">
  <strong>🔥 CopilotForge</strong> — One command to set up Copilot for any project<br>
  Built with ❤️ for the GitHub Copilot community
</p>

