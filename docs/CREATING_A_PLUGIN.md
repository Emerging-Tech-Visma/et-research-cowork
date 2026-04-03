# Creating a Claude Cowork Plugin

This guide explains how to build, package, and distribute a plugin for Claude Cowork following Anthropic's official patterns. Use this repo as a working reference — the `company-investigation` plugin here is built to this standard.

**Official reference repo:** [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins)

---

## What is a Cowork plugin?

A Cowork plugin is a folder of Markdown and JSON files that extends Claude's behavior in a specific domain. Plugins contain **skills** (on-demand workflows Claude follows when invoked), and optionally agents, hooks, MCP server connections, and commands.

No code, no build step, no infrastructure. Just text files.

---

## Plugin structure

Every plugin follows this layout:

```
plugin-name/
├── .claude-plugin/
│   └── plugin.json              # Required — plugin identity and version
├── skills/
│   └── skill-name/
│       ├── SKILL.md             # Required — skill definition and workflow
│       └── references/          # Optional but recommended
│           └── *.md             # Supporting detail files (keep SKILL.md lean)
├── templates/                   # Optional
│   └── *.html / *.md            # Output templates referenced by skills
├── agents/                      # Optional
│   └── agent-name.md            # Autonomous multi-step task definitions
├── hooks/                       # Optional
│   └── hooks.json               # Event-triggered automation
├── .mcp.json                    # Optional — external service connections
├── CONNECTORS.md                # Optional — tool-agnostic mappings
└── LICENSE
```

### What each component does

| Component | Purpose | When to use |
|---|---|---|
| `SKILL.md` | Defines a workflow Claude follows on-demand | Core of most plugins — always |
| `references/*.md` | Detail files loaded by SKILL.md | When SKILL.md would exceed ~3,000 words |
| `templates/` | Output templates (HTML, Markdown) | When the skill produces a formatted artifact |
| `agents/*.md` | Autonomous multi-step task definitions | When a task runs in the background without user turn-by-turn input |
| `hooks/hooks.json` | Automatic event-triggered behavior | When something should happen on every tool call, session start, etc. |
| `.mcp.json` | Connect external services (Slack, GitHub, Jira, etc.) | When the skill needs to read or write to external tools |
| `CONNECTORS.md` | Tool-agnostic category mappings | When your skill should work with multiple tools in the same category |

---

## plugin.json

Every plugin must have a `plugin.json` at `.claude-plugin/plugin.json`:

```json
{
  "name": "your-plugin-name",
  "version": "1.0.0",
  "description": "One-sentence description of what this plugin does.",
  "author": {
    "name": "YourOrg"
  }
}
```

**Rules:**
- `name` — kebab-case, lowercase, no spaces
- `version` — semantic versioning (`MAJOR.MINOR.PATCH`)
- Bump version on every meaningful change — Cowork uses this field to detect updates

---

## SKILL.md anatomy

A skill file has two parts: YAML frontmatter and the workflow body.

### Frontmatter

```yaml
---
name: your-skill-name
description: One-line description of when to use this skill and trigger phrases.
argument-hint: "<input>"
---
```

**Rules:**
- `description` must be a **single line** — multiline YAML (`>-` block scalars) causes Cowork to silently skip the skill
- Include trigger phrases in the description — Claude uses this to auto-invoke the skill
- `argument-hint` is optional but helps users know what input to provide

### Body

The body is instructions **for Claude**, not messages to the user. Use imperative language:

- "Fetch the URL and extract the company name." ✅
- "You should fetch the URL to extract the company name." ❌

**Keep SKILL.md under ~3,000 words.** Use the progressive disclosure pattern for detail:

```
## Step 2: Deep Research

Read `references/agent-prompts.md` for the full agent instructions...
```

Move verbose content into separate files in `references/`. SKILL.md stays lean — detail lives in references.

### Progressive disclosure pattern

```
skill-name/
├── SKILL.md                    ← lean: overview + step flow + pointers
└── references/
    ├── agent-prompts.md        ← verbose: full agent instructions
    ├── report-sections.md      ← verbose: all field specs
    └── html-template-guide.md ← verbose: output formatting rules
```

---

## Naming conventions

| Thing | Convention | Example |
|---|---|---|
| Plugin name | kebab-case, lowercase | `company-investigation` |
| Skill name | kebab-case, lowercase | `company-investigation` |
| Reference files | kebab-case, descriptive | `source-credibility.md` |
| Template files | kebab-case | `report.html` |

---

## Distribution paths

### Personal install via Claude Code CLI

```shell
/plugin marketplace add YourOrg/your-repo
/plugin install your-plugin-name@your-repo
/reload-plugins
```

### Organization distribution (Team/Enterprise — requires Owner role)

**GitHub sync (recommended):**
1. Make repo **private**
2. Claude Desktop → Organization settings → Plugins → Add plugins → **GitHub sync**
3. Connect the private repository — Cowork syncs automatically on every push

**Manual upload:**
1. Claude Desktop → Organization settings → Plugins → Add plugins → **Upload a file**
2. Upload a `.zip` of the plugin directory

> **Note:** Cowork's personal "Upload local plugin" dialog does NOT support skills from ZIPs — only the org admin upload path and GitHub marketplace sync load skills correctly.

---

## Versioning checklist

On every meaningful change, bump the version in **all three places**:

- [ ] `plugins/plugin-name/.claude-plugin/plugin.json` → `"version": "X.Y.Z"`
- [ ] `.claude-plugin/marketplace.json` → `"metadata": { "version": "X.Y.Z" }`
- [ ] `.claude-plugin/marketplace.json` → plugin entry `"version": "X.Y.Z"`
- [ ] `CHANGELOG.md` → add entry for the new version

All must match. Cowork compares the plugin entry version in `marketplace.json` against the installed version to detect available updates.

---

## Update detection gotcha

After a version bump and merge, Cowork won't detect the update until you **sync the marketplace**:

1. Cowork → Customize → find the marketplace → click **Sync**
2. Then the **Update** button on the plugin becomes active
3. Click Update → **restart Claude desktop** for the new version to load

---

## Further reading

- [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins) — 11 production plugins to study
- [cowork-plugin-management](https://github.com/anthropics/knowledge-work-plugins/tree/main/cowork-plugin-management) — Anthropic's meta-plugin for building plugins
- `plugins/company-investigation/` in this repo — complete working example
