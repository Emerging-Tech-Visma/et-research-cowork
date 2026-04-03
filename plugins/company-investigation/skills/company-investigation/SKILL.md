---
name: company-investigation
description: Deep company research with source credibility badges and a self-contained HTML report. Use when researching a company before a meeting, sales call, interview, or due diligence review. Trigger phrases include "investigate [URL]", "research [company]", "I have a meeting with [company]", "tell me about [company]", or any message containing a company URL.
argument-hint: "<company URL>"
---

## Overview

This skill performs a structured, multi-source investigation of a company before a meeting, sales call, interview, or due diligence review. Given a company URL, it fetches the company's website, dispatches four parallel research agents, then synthesises all findings into a single self-contained HTML report saved to the current working directory.

The report covers 10 sections, tags every claim with a source credibility badge, surfaces an AI Moat Score, and delivers ready-to-use talking points.

---

## Tools Used

- **WebFetch** — read the company URL and its subpages
- **WebSearch** — research competitors, news, funding, tech stack, and sentiment
- **Agent** — dispatch four parallel research agents
- **Write** — save agent findings to `/tmp/` and write the final HTML report
- **Read** — read reference files and agent output files

---

## Step 1: Quick Scan

When the user invokes `/investigate <url>`:

1. Use **WebFetch** to read the company URL provided by the user.
2. Extract: company name, tagline, what they do (1–2 sentences), key subpages found in navigation.
3. Present a brief summary (3–5 sentences: who they are, what they build, who they serve).
4. List the 10 report sections that will be covered:
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
5. Ask: "Want to adjust focus areas, add context, or skip any sections before I run the full investigation? (Or just say 'go' to proceed with all sections.)"
6. **STOP. Wait for the user's next message before doing anything else.**

### Step 1 error handling

- **URL unreachable:** Inform user, offer web-search-only mode, note in report header.
- **Empty/minimal content:** Note to user, use web search as primary source, continue.
- **Malformed URL:** Ask user for a valid URL before continuing.

---

## Step 2: Deep Research

After the user confirms, note `{{company_name}}` from Step 1. Read `references/agent-prompts.md` for the full instructions to pass to each agent. Then dispatch **4 parallel agents** simultaneously — do not wait for one before starting the next.

| Agent | Sections | Output file |
|---|---|---|
| Company Agent | 1–4 | `/tmp/investigation_company_agent.md` |
| Market Agent | 5 | `/tmp/investigation_market_agent.md` |
| Financial/News Agent | 6–8 | `/tmp/investigation_financial_news_agent.md` |
| AI Moat Agent | 9–10 | `/tmp/investigation_ai_moat_agent.md` |

Wait for all four agents to complete before proceeding to Step 3.

---

## Step 3: Synthesis & Report Generation

### 3.1 — Read all agent output files

Read each file in full. If a file is missing or empty, note which sections are affected — mark them "Research unavailable for this section" in the final report.

### 3.2 — Resolve conflicts

Compare findings for factual contradictions. For each conflict: retain both claims, prefix with `CONFLICT:` in bold, show both claims with sources.

### 3.3 — Source validation pass

Verify every claim carries a credibility tag (`[Verified]`, `[Reported]`, or `[Unconfirmed]`). Any claim missing a tag → assign `[Unconfirmed]`.

### 3.4 — Generate the HTML report

Read `references/html-template-guide.md` for complete HTML generation rules before writing. Read `templates/report.html` for the structural layout and placeholder conventions.

Generate a complete, self-contained HTML report replacing all `{{placeholder}}` variables with actual content. Include all 10 sections, Executive Summary, AI Moat Score widget, Talking Points, and Source Overview.

### 3.5 — Save the report

Filename pattern: `{company_name_lowercase_hyphenated}-investigation-{YYYY-MM-DD}.html`

Write to the **current working directory** (not `/tmp/`).

### 3.6 — Confirm completion

Tell the user: "Investigation complete. Report saved as `{filename}` in the current directory." Provide the full absolute file path.

### 3.7 — Open in browser (macOS)

Offer to open the file automatically: `open {filename}`

---

## Reference Files

| File | Purpose |
|---|---|
| `references/agent-prompts.md` | Full instructions to pass to each of the 4 research agents |
| `references/source-credibility.md` | Three-tier credibility framework and rules for tagging claims |
| `references/report-sections.md` | Definitions for all 10 sections, key questions, and output formats |
| `references/html-template-guide.md` | HTML generation rules, no-JS constraint, placeholder mapping |
| `templates/report.html` | Structural HTML template with `{{placeholder}}` variables and CSS |

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
| URL unreachable at Step 1 | Offer web-search-only mode; note in report header |
| URL returns empty/minimal content | Use web search as primary; continue normally |
| Company too obscure | Deliver what is available; flag low-coverage sections `[Unconfirmed]`; add notice at report top |
| Agent fails or times out | Mark affected sections "Research unavailable"; note in report header |
| Rate limiting during agent runs | Degrade gracefully; note affected sections; do not halt investigation |
| Conflicting facts between agents | Apply CONFLICT resolution from Step 3.2; never silently discard a claim |
| Template file missing | Use fallback inline HTML structure; warn user template was not found |
