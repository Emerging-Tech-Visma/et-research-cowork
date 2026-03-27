---
name: company-investigation
description: >
  Pre-meeting company research — paste a company URL or name and get a scannable HTML report
  with source credibility badges across 10 research dimensions.
  Use when: investigate company, investigate URL, look up company, research company,
  check out company, company background, who is this company, tell me about company,
  I have a meeting with, before my call with, due diligence on, find out about company,
  company profile, company overview, analyze company, dig into company.
  Also handles: update skill, check for skill updates, update investigation skill, update this skill.
  Trigger on any URL followed by an investigation intent, or any company name with research context.
compatibility: Works in both Cowork and Claude Code environments.
version: 1.0.0
---

## Overview

This skill performs a structured, multi-source investigation of a company before a meeting, sales call, interview, or due diligence review. Given a company URL, it fetches the company's website, dispatches parallel research agents across four domains (company profile, market landscape, financials/news, and AI/tech), then synthesises all findings into a single self-contained HTML report saved to the current working directory.

The report covers 10 sections, tags every claim with a source credibility badge, surfaces an AI Moat Score, and delivers ready-to-use talking points so you can walk into any meeting fully prepared.

---

## Tools Used

- **WebFetch** — read the company URL and its subpages (About, Team, Pricing, Blog, etc.)
- **WebSearch** — research competitors, news, funding, tech stack, and sentiment
- **Agent** — dispatch four parallel research agents to maximise coverage and speed
- **Write** — save intermediate agent findings to `/tmp/` and write the final HTML report to the current working directory
- **Read** — read reference files (`references/source-credibility.md`, `references/report-sections.md`) and agent output files from `/tmp/`

---

## Step 1: Quick Scan

When the user invokes `/investigate <url>`:

1. Use **WebFetch** to read the company URL provided by the user.
2. From the fetched content, extract:
   - Company name
   - Tagline or value proposition (verbatim if available)
   - What they do in 1–2 plain-English sentences
   - Any key subpages found in the navigation (e.g. About, Team, Pricing, Careers, Blog, Docs)
3. Present a brief summary to the user (3–5 sentences covering who they are, what they build, and who they serve).
4. List the 10 report sections that will be covered in the full investigation:
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
5. Ask the user: "Want to adjust focus areas, add context, or skip any sections before I run the full investigation? (Or just say 'go' to proceed with all sections.)"
6. **Wait for user response before proceeding to Step 2.** Do not begin research until the user replies.

### Error handling for Step 1

- **URL unreachable or returns an HTTP error:** Inform the user, then offer to proceed using web search only (skip WebFetch for the company URL; rely entirely on WebSearch). Note "Web-search-only mode" in the final report header.
- **URL returns empty or minimal content (e.g. a holding page or login wall):** Note this to the user, state that you will use web search as the primary source for the company's own content, and proceed as normal.
- **Malformed or missing URL:** Ask the user to provide a valid URL before continuing.

---

## Step 2: Deep Research

After the user confirms (says "go" or provides adjustments), note the company name extracted in Step 1 as `{{company_name}}`. Then dispatch **4 parallel agents**. Each agent writes its findings to a dedicated temp file in `/tmp/`. Do not wait for one agent to finish before starting the next — dispatch all four simultaneously.

---

### Agent 1 — Company Agent

**Goal:** Research the company directly from its own website and public profiles.

**Sections covered:** Company Overview, Product/Service Analysis, Team/Leadership, Business Model

**Output file:** `/tmp/investigation_company_agent.md`

**Instructions to pass to the agent:**

> You are a company research agent. Your task is to investigate `{{company_name}}` using its own website and public profiles.
>
> 1. Use WebFetch to read the company's primary URL and any subpages available (About, Team, Product, Pricing, Blog, Docs, Careers).
> 2. Answer the key research questions for sections 1–4 as defined in `references/report-sections.md`. Read that file first.
> 3. For every factual claim you record, append a credibility tag: `[Verified]`, `[Reported]`, or `[Unconfirmed]`, following the definitions in `references/source-credibility.md`. Read that file before you begin writing findings.
> 4. Structure your output as Markdown with one H2 heading per section (## 1. Company Overview, ## 2. Product/Service Analysis, ## 3. Team/Leadership, ## 4. Business Model).
> 5. Under each section, list findings as bullet points. Each bullet must end with its credibility tag and a parenthetical source citation, e.g. `[Verified](company website — About page)`.
> 6. Write your complete findings to `/tmp/investigation_company_agent.md`.

---

### Agent 2 — Market Agent

**Goal:** Research the competitive landscape and market positioning.

**Sections covered:** Market & Competitors

**Output file:** `/tmp/investigation_market_agent.md`

**Instructions to pass to the agent:**

> You are a market research agent. Your task is to map the competitive landscape for `{{company_name}}`.
>
> 1. Use WebSearch to research: direct competitors, adjacent competitors, estimated market size, category name (how analysts label this space), and how `{{company_name}}` is positioned relative to alternatives.
> 2. Check G2 or Capterra category pages for competitor listings, analyst or industry reports, and competitor websites and marketing copy.
> 3. Answer the key research questions for section 5 as defined in `references/report-sections.md`. Read that file first.
> 4. For every factual claim, append a credibility tag (`[Verified]`, `[Reported]`, or `[Unconfirmed]`) and a source citation, following `references/source-credibility.md`. Read that file before writing findings.
> 5. Structure your output as Markdown: ## 5. Market & Competitors, with bullet-point findings.
> 6. Write your complete findings to `/tmp/investigation_market_agent.md`.

---

### Agent 3 — Financial/News Agent

**Goal:** Research funding, financials, press coverage, and risk signals.

**Sections covered:** Financials & Funding, News & Sentiment, Red Flags / Risks

**Output file:** `/tmp/investigation_financial_news_agent.md`

**Instructions to pass to the agent:**

> You are a financial and news research agent. Your task is to surface funding history, media coverage, and risk signals for `{{company_name}}`.
>
> 1. Use WebSearch to find: Crunchbase or PitchBook profile, recent funding rounds (last 3 years), estimated revenue or ARR if publicly reported, key investors, and any IPO or acquisition news.
> 2. Search for news articles from the last 12 months. Look for: product launches, leadership changes, layoffs, lawsuits, regulatory issues, customer complaints, and positive press.
> 3. Search Glassdoor or Blind for employee sentiment signals (rating, key themes in reviews).
> 4. Identify any red flags: negative patterns in press, leadership instability, funding gaps, customer churn signals, or ethical controversies.
> 5. Answer the key research questions for sections 6, 7, and 8 as defined in `references/report-sections.md`. Read that file first.
> 6. **Never state a financial figure without citing its source.** If a figure is estimated, label it as an estimate.
> 7. For every factual claim, append a credibility tag (`[Verified]`, `[Reported]`, or `[Unconfirmed]`) and a source citation, following `references/source-credibility.md`. Read that file before writing findings.
> 8. Structure your output as Markdown with: ## 6. Financials & Funding, ## 7. News & Sentiment, ## 8. Red Flags / Risks.
> 9. Write your complete findings to `/tmp/investigation_financial_news_agent.md`.

---

### Agent 4 — AI Moat Agent

**Goal:** Assess AI usage, tech stack signals, and engineering presence.

**Sections covered:** Tech Stack / Engineering, AI Moat Analysis

**Output file:** `/tmp/investigation_ai_moat_agent.md`

**Instructions to pass to the agent:**

> You are a technology and AI research agent. Your task is to assess the tech stack and AI defensibility of `{{company_name}}`.
>
> 1. Use WebSearch to find tech stack signals: job postings (look for programming languages, frameworks, cloud providers, and data infrastructure tools mentioned), engineering blog posts, GitHub organisation presence (public repos, activity level, stars), and BuiltWith or similar data if available.
> 2. Assess AI and ML adoption: Does the company describe proprietary AI/ML capabilities? Are they using AI as a feature wrapper (low moat) or building core models/data assets (high moat)? Look for patents, research papers, unique datasets, or AI-specific job titles (ML Engineer, Research Scientist).
> 3. Rate the company's AI moat as one of: **Low** / **Medium** / **High** / **Strong**. Provide 2–4 specific evidence points supporting your rating.
> 4. Answer the key research questions for sections 9 and 10 as defined in `references/report-sections.md`. Read that file first.
> 5. For every factual claim, append a credibility tag (`[Verified]`, `[Reported]`, or `[Unconfirmed]`) and a source citation, following `references/source-credibility.md`. Read that file before writing findings.
> 6. Structure your output as Markdown with: ## 9. Tech Stack / Engineering, ## 10. AI Moat Analysis.
> 7. Write your complete findings to `/tmp/investigation_ai_moat_agent.md`.

---

**After dispatching all four agents, wait for all of them to complete before proceeding to Step 3.**

---

## Step 3: Synthesis & Report Generation

Once all four agents have written their output files, proceed as follows.

### 3.1 — Read all agent output files

Read each of the following files in full:
- `/tmp/investigation_company_agent.md`
- `/tmp/investigation_market_agent.md`
- `/tmp/investigation_financial_news_agent.md`
- `/tmp/investigation_ai_moat_agent.md`

If any file is missing or empty (because an agent failed or timed out), note which sections are affected. Those sections will be marked "Research unavailable for this section" in the final report.

### 3.2 — Resolve conflicts

Compare the four files for any factual contradictions (e.g. two agents cite different founding years, headcounts, or funding totals). For each conflict found:
- Retain both claims in the report.
- Prefix the affected bullet with `CONFLICT:` in bold.
- Show both claims with their respective sources so the reader can judge.

### 3.3 — Source validation pass

Before writing the report, verify that every claim in the combined findings carries a credibility tag (`[Verified]`, `[Reported]`, or `[Unconfirmed]`). Any claim missing a tag should be assigned `[Unconfirmed]` by default.

### 3.4 — Generate the HTML report

Read the template file at `templates/report.html` to understand the structural layout, CSS variables, and placeholder conventions.

Generate a **complete, self-contained HTML report** based on that template. The report must:

1. **Replace all `{{placeholder}}` variables** with actual content derived from the agent findings and the company name/date.
2. **Include all 10 sections** with findings written as readable prose or scannable bullet points, each annotated with source credibility badges.
3. **Include an Executive Summary** at the top (3–5 bullet points formatted as "walk in knowing this" statements — the most critical facts a person needs before the meeting).
4. **Include an AI Moat Score** widget showing the four levels (Low / Medium / High / Strong) with the correct level visually highlighted based on Agent 4's assessment.
5. **Include a Talking Points section** with 4–6 conversation starters the user can bring into the meeting, grounded in the research findings.
6. **Include a Source Overview** section at the bottom, listing all cited sources grouped by credibility tier (Tier 1: Primary, Tier 2: Secondary, Tier 3: Inferred) as defined in `references/source-credibility.md`.
7. **Be completely self-contained** — all CSS must be inlined or in a `<style>` block within the file. No external stylesheets, fonts, or scripts. No CDN links. The file must render correctly when opened from a local filesystem with no internet access.
8. **Mark any sections with missing agent data** clearly: use a banner or callout reading "Research unavailable — agent did not return results for this section."
9. **Mark any conflicts** using the `CONFLICT:` label, showing both claims.
10. **Include the report generation date** (today's date: use the date at time of execution) and the source URL in the report header.

### 3.5 — Save the report

Determine the output filename using this pattern:
- Take the company name, convert to lowercase, replace spaces and special characters with hyphens.
- Format: `{company_name_lowercase_hyphenated}-investigation-{YYYY-MM-DD}.html`
- Example: `acme-corp-investigation-2026-03-26.html`

Write the complete HTML file to the **current working directory** (not `/tmp/`).

### 3.6 — Confirm completion

Tell the user:

> "Investigation complete. Report saved as `{filename}` in the current directory. Open it in your browser to view the full report."

Then provide the full absolute file path so the user can open it directly.

### 3.7 — Open in browser (optional)

If running on macOS, offer to open the file automatically:
```
open {filename}
```
Ask the user if they want it opened, or simply inform them of the path and let them open it.

---

## Reference Files

The following files are part of this skill's supporting resources. Agents must read these files before writing their findings.

| File | Purpose |
|---|---|
| `references/source-credibility.md` | Defines the three credibility tiers and the rules for tagging claims as `[Verified]`, `[Reported]`, or `[Unconfirmed]` |
| `references/report-sections.md` | Defines each of the 10 report sections, the key questions each section must answer, and the agent responsible |
| `templates/report.html` | The structural HTML template with `{{placeholder}}` variables, CSS, and layout for the final report |

---

## Output Spec

| Property | Value |
|---|---|
| Filename | `{company_name_lowercase_hyphenated}-investigation-{YYYY-MM-DD}.html` |
| Location | Current working directory |
| Format | Self-contained HTML (no external dependencies) |
| Encoding | UTF-8 |
| Auto-open | Offered after save on macOS; file path always shown |

---

## Error Handling

| Condition | Response |
|---|---|
| URL unreachable at Step 1 | Inform user; offer web-search-only mode; note "Web-search-only mode — company website unavailable" in the report header |
| URL returns empty/minimal content | Note to user; use web search as primary company source; continue normally |
| Company too obscure (very few sources found) | Deliver what is available; flag low-coverage sections with `[Unconfirmed]`; add a notice at the top of the report: "Limited public information available — coverage may be incomplete" |
| An agent fails or times out | Skip that agent's sections in the report; mark each affected section with "Research unavailable — agent did not return results for this section"; note the gap in the report header |
| Rate limiting on web search during agent runs | Degrade gracefully; note affected sections as having incomplete research; do not halt the entire investigation |
| Conflicting facts between agents | Apply the CONFLICT resolution process defined in Step 3.2; never silently discard either claim |
| Template file missing | Generate the report using a fallback inline structure (plain but readable HTML) and warn the user that the template was not found |

---

## Updating This Skill

When the user asks to **update this skill**, **check for updates**, or **update the investigation skill**, run the following flow instead of the investigation flow.

### Update Check

1. Use **WebFetch** to fetch the latest release from the GitHub API:
   ```
   https://api.github.com/repos/Emerging-Tech-Visma/et-research-cowork/releases/latest
   ```
2. Parse the response and extract:
   - `tag_name` — the latest version (e.g. `v1.2.0`)
   - `name` — release title
   - `body` — release notes / changelog
   - `assets[].browser_download_url` — direct download link for the `.skill` file (look for an asset ending in `.skill`)
3. Compare the latest tag against the current skill version (`1.0.0`).

### If an update is available

Tell the user:

> "A new version of the company-investigation skill is available: **{tag_name}**
>
> **What's new:**
> {release body, trimmed to key bullet points}
>
> **To update in Claude Cowork:**
> 1. Download the new skill file: `{browser_download_url}`
> 2. Open Claude Cowork → **Settings → Skills**
> 3. Find **company-investigation** and click **Update** (or **Remove**, then re-add)
> 4. Import the downloaded `.skill` file — or paste the repo URL to re-install from source:
>    `https://github.com/Emerging-Tech-Visma/et-research-cowork`"

### If already on the latest version

Tell the user:

> "You're already on the latest version of company-investigation (`{current_version}`). No update needed."

### If the GitHub API is unreachable

Tell the user:

> "Could not reach GitHub to check for updates. You can check manually at:
> https://github.com/Emerging-Tech-Visma/et-research-cowork/releases/latest"
