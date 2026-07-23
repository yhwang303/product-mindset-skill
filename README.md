# Product Mindset Skill

[English](README.md) | [简体中文](README.zh-CN.md)

Product Mindset is an Agent Skill that turns productization experience into behavioral guardrails for AI coding agents. It helps an agent build something that real users can understand, adopt, trust, and operate—not merely a demo that works on the developer's machine.

The skill is intentionally risk-adjusted. A free community utility should not be forced through pricing, customer-support, and enterprise-lifecycle work. A long-running internal system or regulated commercial product should not be allowed to skip reliability, security, recovery, and compliance checks.

## What it changes

When relevant, the skill requires the agent to:

- explicitly define the product level before starting a new product;
- separate user evidence from assumptions;
- compare the product with competitors, general AI, manual workflows, and doing nothing;
- inspect the first-use journey and remove unnecessary friction;
- apply release requirements in proportion to actual exposure and failure impact;
- verify real user paths instead of declaring completion from code inspection;
- surface only decisions, blockers, research deliverables, and release-gate results instead of producing ritual product commentary.

This is a behavioral guardrail, not a security sandbox. For hard enforcement, combine it with tests, hooks, CI gates, permissions, and external stateful tooling.

## Product levels

You must explicitly define or confirm the level for a new product before implementation begins.

| Level | Use it for | Typical expectations |
| --- | --- | --- |
| **T0 — Exploration prototype** | Testing a technical, interaction, or demand hypothesis; no usability promise | Hypothesis, validation method, stop condition; do not call it productized |
| **T1 — Shared utility** | Free/open-source tools, small public utilities, low-risk vibe-coded projects | Core value, shortest path, install docs, recovery, data boundary, limitations, basic verification |
| **T2 — Sustained-use product** | Internal multi-user systems, long-running public services, real accounts or data | T1 plus metrics, permissions, reliability, monitoring, backup, rollback, support, upgrade and migration |
| **T3 — Commercial or critical product** | Paid products, SLAs, sensitive data, critical business, regulated domains | T2 plus compliance, threat modeling, audit, capacity, incident response, formal support and lifecycle |

Profit is not required for productization. Risk requirements still apply to free software when it handles credentials, private data, payments, health information, or irreversible operations.

## Start with an explicit product-definition prompt

Do not begin a new project with only “build me an app.” Make the level decision visible in the prompt.

If you already know the level:

```text
Use the product-mindset skill for this project.

Product definition:
- Target user:
- Problem and usage scenario:
- Current alternative:
- Product level: T0 / T1 / T2 / T3
- Why this level:
- Explicit non-goals:

Before coding, check whether the selected level matches the actual exposure and failure impact.
Then apply the corresponding productization requirements throughout implementation.
```

If you are unsure:

```text
Use the product-mindset skill.

Before writing code:
1. Help me define the target user, real problem, current alternative, expected users, data sensitivity, operating duration, and failure impact.
2. Recommend T0, T1, T2, or T3 with a short reason.
3. Ask me to explicitly confirm the level.

Do not start implementation until I confirm the product level.

My product idea is: ...
```

For later work, state the confirmed level briefly:

```text
Continue this product as T2. Add team invitations without increasing onboarding friction or weakening permission boundaries.
```

## Installation

Claude Code discovers a skill from `~/.claude/skills/<skill-name>/SKILL.md` for personal use or `.claude/skills/<skill-name>/SKILL.md` for one project. This follows Anthropic's [official Agent Skills documentation](https://docs.anthropic.com/en/docs/claude-code/skills).

### Option A: Claude Code plugin marketplace (recommended, all platforms)

Run these commands inside Claude Code:

```text
/plugin marketplace add yhwang303/product-mindset-skill
/plugin install product-mindset@product-mindset-skills
/reload-plugins
```

This repository follows Anthropic's [plugin marketplace format](https://code.claude.com/docs/en/plugin-marketplaces). Future updates can be obtained through the marketplace/plugin update flow.

### Option B: Personal installation on macOS or Linux

```bash
mkdir -p ~/.claude/skills/product-mindset
curl -L \
  https://raw.githubusercontent.com/yhwang303/product-mindset-skill/main/skills/product-mindset/SKILL.md \
  -o ~/.claude/skills/product-mindset/SKILL.md
```

For Cursor:

```bash
mkdir -p ~/.cursor/skills/product-mindset
curl -L \
  https://raw.githubusercontent.com/yhwang303/product-mindset-skill/main/skills/product-mindset/SKILL.md \
  -o ~/.cursor/skills/product-mindset/SKILL.md
```

### Option C: Personal installation on Windows PowerShell

Claude Code:

```powershell
$dir = Join-Path $HOME ".claude\skills\product-mindset"
New-Item -ItemType Directory -Force $dir | Out-Null
Invoke-WebRequest `
  "https://raw.githubusercontent.com/yhwang303/product-mindset-skill/main/skills/product-mindset/SKILL.md" `
  -OutFile (Join-Path $dir "SKILL.md")
```

Cursor:

```powershell
$dir = Join-Path $HOME ".cursor\skills\product-mindset"
New-Item -ItemType Directory -Force $dir | Out-Null
Invoke-WebRequest `
  "https://raw.githubusercontent.com/yhwang303/product-mindset-skill/main/skills/product-mindset/SKILL.md" `
  -OutFile (Join-Path $dir "SKILL.md")
```

### Option D: Install only for one project

macOS/Linux:

```bash
mkdir -p .claude/skills/product-mindset
curl -L \
  https://raw.githubusercontent.com/yhwang303/product-mindset-skill/main/skills/product-mindset/SKILL.md \
  -o .claude/skills/product-mindset/SKILL.md
```

Windows PowerShell:

```powershell
$dir = ".claude\skills\product-mindset"
New-Item -ItemType Directory -Force $dir | Out-Null
Invoke-WebRequest `
  "https://raw.githubusercontent.com/yhwang303/product-mindset-skill/main/skills/product-mindset/SKILL.md" `
  -OutFile (Join-Path $dir "SKILL.md")
```

Commit the project-scoped skill if everyone working in the repository should use the same guardrails.

### Option E: Ask an agent to install it

Paste this into an agent that can access the filesystem and GitHub:

```text
Install the Product Mindset Agent Skill from:
https://github.com/yhwang303/product-mindset-skill

Before changing files:
1. Read skills/product-mindset/SKILL.md and confirm that it contains no scripts or executable hooks.
2. Install it as a personal skill at ~/.claude/skills/product-mindset/SKILL.md.
3. If a file already exists there, back it up instead of overwriting it silently.
4. Verify the YAML frontmatter after copying.
5. Report the installed path and show me the explicit T0–T3 product-definition prompt.
```

Replace the destination with `~/.cursor/skills/product-mindset/SKILL.md` for Cursor, or `.claude/skills/product-mindset/SKILL.md` for project-only installation.

## Verify the installation

Ask:

```text
Use product-mindset. Explain T0–T3 in one sentence each, then ask me to explicitly define the level of my product before we write code.
```

If the skill is not found, confirm the directory name is `product-mindset`, the file is named exactly `SKILL.md`, and the YAML frontmatter begins and ends with `---`. Claude Code may need a restart if the top-level skills directory did not exist when the session started.

## Update or remove

For a manual installation, rerun the installation command to update.

To remove a personal Claude Code installation:

```bash
rm -rf ~/.claude/skills/product-mindset
```

Windows PowerShell:

```powershell
Remove-Item -Recurse -Force (Join-Path $HOME ".claude\skills\product-mindset")
```

Review the path before deleting. Project and Cursor installations use the corresponding paths shown above.

## Repository layout

```text
.
├── .claude-plugin/
│   └── marketplace.json
├── skills/
│   └── product-mindset/
│       └── SKILL.md
├── README.md
├── README.zh-CN.md
└── LICENSE
```

## Contributing

Issues and pull requests are welcome. Changes should preserve the core design:

- proportional requirements instead of one enterprise checklist for every project;
- evidence over agent self-assessment;
- explicit product-level confirmation for new products;
- minimal visible commentary during ordinary implementation;
- safety and data-protection blockers cannot be waived by selecting a lower level.

## License

MIT
