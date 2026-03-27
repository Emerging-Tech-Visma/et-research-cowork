# company-investigation

> Pre-meeting company research — paste a URL, get a scannable HTML report.

A Claude Cowork skill that dispatches parallel AI research agents across 10 dimensions and delivers a self-contained HTML report with source credibility badges — ready before your next meeting.

---

## What you get

```
/investigate https://notion.so
```

```
┌─────────────────────────────────────────────────────┐
│  Notion                                             │
│  "The all-in-one workspace"          2026-03-26     │
├─────────────────────────────────────────────────────┤
│  Founded  │  HQ           │  Employees │  Funding   │
│  2013     │  San Francisco│  ~800      │  $343M     │
├─────────────────────────────────────────────────────┤
│  EXECUTIVE SUMMARY                                  │
│  • Valued at $10B (2021), PLG → enterprise push     │
│  • Notion AI at $10/member/mo — new revenue stream  │
│  • Main threat: Microsoft Loop bundled in M365      │
├─────────────────────────────────────────────────────┤
│  ▸ 1. Company Overview          [Verified]          │
│  ▸ 2. Product / Service         [Verified]          │
│  ▸ 3. Team / Leadership         [Reported]          │
│  ▸ 4. Business Model            [Verified]          │
│  ▸ 5. Market & Competitors      [Reported]          │
│  ▸ 6. Financials & Funding      [Verified]          │
│  ▸ 7. Tech Stack / Engineering  [Unconfirmed]       │
│  ▸ 8. News & Sentiment          [Reported]          │
│  ▸ 9. Red Flags / Risks         [Reported]          │
│  ▸ 10. AI Moat Analysis         [Reported]          │
├─────────────────────────────────────────────────────┤
│  AI MOAT SCORE:  Low  [ Medium ]  High  Strong      │
├─────────────────────────────────────────────────────┤
│  TALKING POINTS                                     │
│  1. "How is Notion AI attach rate tracking?"        │
│  2. "How are you handling the Loop bundling risk?"  │
│  3. "What % of revenue is now enterprise?"          │
├─────────────────────────────────────────────────────┤
│  SOURCES                                            │
│  [Verified]     notion.so, Crunchbase + Bloomberg   │
│  [Reported]     TechCrunch, G2, Glassdoor           │
│  [Unconfirmed]  LinkedIn estimates, Reddit signals  │
└─────────────────────────────────────────────────────┘
```

---

## How it works

```
User: /investigate https://company.com
         │
         ▼
┌─────────────────────┐
│   STEP 1: QUICK     │  WebFetch company URL
│   SCAN              │  Extract: name, tagline, subpages
│                     │  Show 10 sections → ask to adjust
└────────┬────────────┘
         │ user confirms "go"
         ▼
┌────────────────────────────────────────────────┐
│              STEP 2: DEEP RESEARCH             │
│  (4 agents run in parallel)                    │
│                                                │
│  ┌───────────────┐   ┌───────────────────────┐ │
│  │ Company Agent │   │    Market Agent       │ │
│  │ Sections 1–4  │   │    Section 5          │ │
│  │ (company URL  │   │    (G2, Capterra,     │ │
│  │  + subpages)  │   │     web search)       │ │
│  └───────┬───────┘   └──────────┬────────────┘ │
│          │                      │               │
│  ┌───────┴───────┐   ┌──────────┴────────────┐ │
│  │ Financial /   │   │    AI Moat Agent      │ │
│  │ News Agent    │   │    Sections 9–10      │ │
│  │ Sections 6–8  │   │    (job postings,     │ │
│  │ (Crunchbase,  │   │     GitHub, patents)  │ │
│  │  news, G2)    │   │                       │ │
│  └───────┬───────┘   └──────────┬────────────┘ │
│          └──────────┬───────────┘               │
└───────────────────────────────────────────────-─┘
                      │
                      ▼
         ┌────────────────────────┐
         │   STEP 3: SYNTHESIS    │
         │                        │
         │  1. Merge all findings │
         │  2. Resolve conflicts  │
         │  3. Tag credibility    │
         │  4. Generate HTML      │
         │  5. Save + open report │
         └────────────────────────┘
                      │
                      ▼
         notion-investigation-2026-03-26.html
```

---

## Source credibility

Every claim in the report is tagged:

```
┌────────────────┬─────────────────────────────────────────────┐
│ Badge          │ Criteria                                     │
├────────────────┼─────────────────────────────────────────────┤
│ [Verified]     │ Company's own URL, or 2+ independent sources │
│ [Reported]     │ Single reputable source (Reuters, G2, etc.)  │
│ [Unconfirmed]  │ Social media, forums, inferred/estimated     │
└────────────────┴─────────────────────────────────────────────┘
```

Conflicts between sources are flagged explicitly — never silently resolved.

---

## Install in Claude Cowork

Three ways to install — pick whichever suits you best.

### Option 1 — From GitHub (best for teams)

This is the recommended method. It keeps the skill in sync — when updates are published, just click Sync to get the latest version.

1. Open **Claude Cowork** and click **Customize** in the left sidebar
2. Under **Personal plugins**, click **+** → **Add marketplace**
3. Paste the repo URL:
   ```
   https://github.com/Emerging-Tech-Visma/et-research-cowork
   ```
4. Click **Sync** — the skill is now available to your account

> **First time?** Claude needs access to GitHub. Click **Install the Claude GitHub App** when prompted, grant access to the org/repo, then come back and click Sync again.

### Option 2 — Download the `.skill` file (quick one-click install)

Grab the ready-made skill file from the releases page and drag it into Cowork. No GitHub account needed.

1. Download [`company-investigation.skill`](https://github.com/Emerging-Tech-Visma/et-research-cowork/releases/latest/download/company-investigation.skill)
2. In Claude Cowork → **Customize** → **Personal plugins** → **+** → **Upload plugin**
3. Select the downloaded `.skill` file — done

### Option 3 — Source code zip (inspect or modify before installing)

For anyone who wants to review the code or make changes before installing.

1. Go to the [latest release](https://github.com/Emerging-Tech-Visma/et-research-cowork/releases/latest)
2. Under **Assets**, download **Source code (zip)**
3. Unzip and review or modify the skill files
4. In Claude Cowork → **Customize** → **Personal plugins** → **+** → **Upload plugin**
5. Select the folder or repackage as a `.plugin` file

### Updating the skill

If you installed via GitHub (Option 1), re-sync to get the latest version:

1. Claude Cowork → **Customize** → **Personal plugins**
2. Click the **company-investigation** plugin → **Sync**

If you installed via `.skill` file (Option 2), download the new release and re-upload it.

---

## Usage

### Slash command

```
/investigate https://linear.app
```

### Natural language (also works)

```
I have a meeting with Intercom tomorrow, can you help me prep?
Research Drata before my call with them
Due diligence on Notion — what do I need to know?
```

### Flow

```
You                          Claude Cowork
 │                                │
 │  /investigate https://...      │
 ├──────────────────────────────► │
 │                                │ fetches URL, extracts company info
 │  "Here's what I found:         │
 │   [company summary]            │
 │   Ready to run all 10          │
 │   sections? (say 'go')"        │
 ◄──────────────────────────────── │
 │                                │
 │  go                            │
 ├──────────────────────────────► │
 │                                │ 4 parallel agents research
 │                                │ (takes 3–10 minutes)
 │  "Investigation complete.      │
 │   Report saved as              │
 │   company-2026-03-26.html"     │
 ◄──────────────────────────────── │
 │                                │
 │  [opens in browser]            │
```

### Customising sections

After the Quick Scan, you can tell Claude to skip or focus:

```
Skip the Tech Stack section, I already know their stack.
Focus more on Red Flags and Financials.
Add extra context: they just acquired a competitor last month.
```

---

## Report sections

| # | Section | What it covers |
|---|---------|---------------|
| 1 | Company Overview | What they do, founding story, HQ, size |
| 2 | Product / Service | Offerings, pricing, target customer |
| 3 | Team / Leadership | Founders, C-suite, advisors, recent changes |
| 4 | Business Model | Revenue model, go-to-market, contract motion |
| 5 | Market & Competitors | Category, top 3–5 competitors, TAM, positioning |
| 6 | Financials & Funding | Rounds, investors, ARR signals, valuation |
| 7 | Tech Stack / Engineering | Stack, hiring signals, engineering culture |
| 8 | News & Sentiment | Press, customer/employee reviews (last 12mo) |
| 9 | Red Flags / Risks | Lawsuits, exec departures, controversies |
| 10 | AI Moat Analysis | AI defensibility: Low / Medium / High / Strong |

---

## Output

```
Output file:  {company_name}-investigation-{YYYY-MM-DD}.html
Location:     Current working directory
Format:       Self-contained HTML (no internet required to view)
Auto-opens:   Yes (macOS) — browser opens after generation
```

---

## Requirements

- Claude Cowork (any plan with skill support)
- No API keys or external accounts needed
- Works on any company with a public website

---

## License

MIT — see [LICENSE](LICENSE)

---

## Building your own Cowork skill — PRD Template

The design spec below is the exact document used to design this skill. Use it as a template when writing a PRD for your own Claude Cowork skill.

Full file: [`docs/design-spec.md`](docs/design-spec.md)

---

### Skill PRD template

```markdown
# {Skill Name} — Design Spec

**Date:** {YYYY-MM-DD}
**Repo:** `{org}/{repo}`
**Type:** Claude Cowork public skill (standalone, no workbench dependencies)
**Purpose:** {one-line description of what the skill does}

---

## 1. Skill Identity

| Field | Value |
|-------|-------|
| **Name** | `{skill-name}` |
| **Repo** | `github.com/{org}/{repo}` |
| **Invoke** | `/{command} <input>` |
| **Triggers** | "natural language phrase 1", "phrase 2", "phrase 3" |
| **Context** | fork (runs in isolated subagent) |

## 2. Repository Structure

{skill-name}/
├── SKILL.md                    # Skill definition + full instructions
├── references/
│   └── *.md                    # Supporting reference files for the skill
├── templates/
│   └── *.html / *.md           # Output templates
├── examples/
│   └── example-output.*        # Sample output for reference
├── LICENSE
└── README.md

Key constraint: List any hard constraints (no external deps, no API keys, etc.)

## 3. Flow

Describe the step-by-step flow the skill follows.

### Step 1: {Step name}

1. What the skill does first
2. What it extracts or asks
3. What it presents to the user

### Step 2: {Step name}

How it processes the user input and produces output.

## 4. {Core Framework / Logic}

Describe the core model, scoring system, or decision logic the skill uses.

| Category | Criteria | Output |
|----------|----------|--------|
| ... | ... | ... |

## 5. Output Design

**Goal:** What makes a good output for this skill?

### Layout

- What sections the output contains
- How it's structured for the user

### Styling / Format

- File format (HTML, Markdown, JSON, etc.)
- Self-contained? Offline-capable?

## 6. Scope & Boundaries

### In Scope

- What the skill handles

### Out of Scope

- What the skill explicitly does NOT handle

### Error Handling

- Known failure modes and how the skill responds

## 7. Output

**Path:** Where is the output saved?
**Filename:** `{pattern}-{YYYY-MM-DD}.{ext}`
**Opened automatically?** Yes / No
```
