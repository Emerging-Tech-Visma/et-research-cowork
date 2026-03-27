# Company Investigation Skill — Design Spec

**Date:** 2026-03-26
**Repo:** `Emerging-Tech-Visma/et-company-investigation`
**Type:** Claude Cowork public skill (standalone, no workbench dependencies)
**Purpose:** Pre-meeting company research — paste a URL, get a scannable HTML report

---

## 1. Skill Identity

| Field | Value |
|-------|-------|
| **Name** | `company-investigation` |
| **Repo** | `github.com/Emerging-Tech-Visma/et-company-investigation` |
| **Invoke** | `/investigate <url>` |
| **Tier** | 1 |
| **Triggers** | "investigate company", "company research", "research company", "due diligence", "pre-meeting prep" |
| **Context** | fork (runs in isolated subagent) |

## 2. Repository Structure

```
et-company-investigation/
├── SKILL.md                    # Skill definition + full instructions
├── references/
│   ├── report-sections.md      # Section definitions & agent prompts
│   └── source-credibility.md   # Source validation rules & tier definitions
├── templates/
│   └── report.html             # Self-contained HTML report template
├── examples/
│   └── example-report.html     # Sample output for reference
├── LICENSE                     # Open source license
└── README.md                   # Public docs for Claude Cowork users
```

**Key constraint:** Fully self-contained. No external tool dependencies. Claude uses built-in tools only (WebFetch, WebSearch, Write, Read, Agent).

## 3. Two-Step Flow

### Step 1: Quick Scan

When user runs `/investigate <url>`:

1. **Read the company URL** via WebFetch/Jina
2. **Extract:** company name, tagline, what they do, key pages found
3. **Present summary** to user with the 10 default report sections:
   1. Company Overview
   2. Product/Service Analysis
   3. Team/Leadership
   4. Business Model
   5. Market & Competitors
   6. Financials & Funding
   7. Tech Stack / Engineering
   8. News & Sentiment
   9. Red Flags / Risks
   10. AI Moat Analysis
4. **Ask user:** "Want to adjust focus areas, add context, or skip any sections before I run the full investigation?"

### Step 2: Deep Research (Parallel Agents)

Dispatch **4 parallel agents**, each writes findings to a temp file in `/tmp/investigation_*.md`:

| Agent | Focus | Primary Sources |
|-------|-------|----------------|
| **Company Agent** | Overview, product, team, business model | Company URL + subpages (trusted source) |
| **Market Agent** | Competitors, market size, positioning | Web search, industry reports, G2, Capterra |
| **Financial/News Agent** | Funding, revenue, press, sentiment, red flags | Crunchbase, news outlets, web search |
| **AI Moat Agent** | AI defensibility, AI adoption, tech signals | Web search, job postings, tech blogs |

After all agents complete:

1. **Synthesize** — merge findings, deduplicate, resolve conflicts
2. **Source validation pass** — tag each claim with credibility tier
3. **Generate HTML** — render into the self-contained report template
4. **Open in browser** for user review

## 4. Source Credibility Framework

Every claim in the report gets a credibility tag:

| Tier | Label | Criteria | Display |
|------|-------|----------|---------|
| **Verified** | Company-sourced OR 2+ independent sources agree | Green badge |
| **Reported** | Single reputable source | Yellow badge |
| **Unconfirmed** | Single source, uncertain reliability, or inferred | Grey badge with note |

### Source Classification Rules

- **Company's own URL** → always Verified (user-defined trusted source)
- **2+ independent external sources agreeing** → Verified
- **Major news outlets** (Reuters, Bloomberg, TechCrunch, Financial Times, WSJ, etc.) → Reported minimum
- **Major review platforms** (G2, Capterra, Trustpilot) → Reported minimum
- **Social media, forums, anonymous sources** → Unconfirmed unless corroborated
- **Financial figures** → must have source citation, never stated without attribution
- **Agent disagreement** → flag the conflict explicitly in the report rather than picking one side

### Report Display

- Each section shows sources as footnotes with credibility badge inline
- "Source Overview" section at the bottom lists all sources grouped by tier

## 5. HTML Report Design

**Design goal:** Scannable pre-meeting prep — not a wall of text.

### Layout

- **Executive Summary** — top of report, 3-5 bullet points ("walk into the meeting knowing this")
- **Key Stats Sidebar** — founding year, HQ, employee count, funding, revenue (if known)
- **10 Collapsible Sections** — each with heading, 2-4 key findings, source badges
- **AI Moat Score** — visual indicator (Low / Medium / High / Strong) with reasoning
- **Talking Points** — auto-generated conversation starters for meeting prep
- **Source Overview** — all sources grouped by credibility tier

### Styling

- Self-contained CSS, no external dependencies
- Dark/light mode via `prefers-color-scheme`
- Print-friendly (collapses sections, hides non-essential)
- Mobile responsive
- No external fonts or CDN links — fully offline-capable

## 6. Scope & Boundaries

### In Scope

- Single company investigation per invocation
- Public information only (no API keys required beyond Claude's built-in tools)
- English-language sources (primary), with note if company is non-English
- Works with any company that has a website URL

### Out of Scope

- Comparing multiple companies
- Paid data sources (Bloomberg Terminal, PitchBook, etc.)
- Ongoing monitoring / alerts
- Private company financials beyond what's publicly reported

### Error Handling

- **URL unreachable** → inform user, offer to proceed with web search only
- **Company too obscure** (few sources) → deliver what's available, flag low-coverage sections as Unconfirmed
- **Rate limiting on web search** → degrade gracefully, note which sections are incomplete

## 7. Output

**Path:** Current working directory by default. The skill asks the user where to save if unclear. For workbench users: `~/Documents/Output/{company_name}/final/`

**Filename:** `{company_name}-investigation-{YYYY-MM-DD}.html`

**Opened automatically** in browser after generation for quick review.
