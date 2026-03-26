# Report Sections Reference

This document defines all 10 sections of a `company-investigation` report. Each section specifies the responsible agent, the primary sources to consult, the key questions the agent must answer, and the output format. Agents must work through every question and note unanswered questions explicitly — they must not omit a section or skip questions silently.

All credibility tiering follows `/references/source-credibility.md`.

---

## Agent Roster

| Agent | Sections Owned |
|---|---|
| Company Agent | 1 — Company Overview, 2 — Product/Service Analysis, 3 — Team/Leadership, 4 — Business Model |
| Market Agent | 5 — Market & Competitors, and positioning signals from competitor comparison data |
| Financial/News Agent | 6 — Financials & Funding, 7 — News & Sentiment, 8 — Red Flags / Risks |
| AI Moat Agent | 9 — Tech Stack / Engineering, 10 — AI Moat Analysis |

---

## Section 1: Company Overview

**Report heading:** `## 1. Company Overview`
**Responsible agent:** Company Agent
**Output file:** `/tmp/investigation_company_agent.md` (Section 1 block)

### Primary Sources
- Company website (homepage, About page, Mission/Values page)
- LinkedIn company page
- Official press releases (founding announcement, milestone announcements)
- Crunchbase or PitchBook company profile (for founding date, HQ)

### Key Questions (agent must address all 4)
1. What exactly does this company do — describe the core business in 2 sentences?
2. When was it founded and by whom (founder names)?
3. Where is the company headquartered (city, country)?
4. How many employees does the company have (current best estimate)?

### Output Format

```markdown
# Company Overview
**Confidence:** [overall section confidence — use the lowest tier present]
**Sources consulted:** [list each source name and URL]

## Key Findings
- [Claim] [Tier] (Source: name, URL)
- [Claim] [Tier] (Source: name, URL)
...

## Unanswered Questions
- [Any of the 4 key questions the agent could not answer, with a note on why]
```

---

## Section 2: Product/Service Analysis

**Report heading:** `## 2. Product/Service Analysis`
**Responsible agent:** Company Agent
**Output file:** `/tmp/investigation_company_agent.md` (Section 2 block)

### Primary Sources
- Company product/solutions pages
- Company pricing page (if public)
- G2 product profile and reviews
- Capterra product profile and reviews
- Product demos or video walkthroughs (YouTube, company website)
- App store listings (if applicable)

### Key Questions (agent must address all 4)
1. What are the company's main products or services — list each with a one-line description?
2. Is pricing publicly available — if so, what are the tiers and approximate price points?
3. Who is the target customer — SMB, mid-market, enterprise, or consumer? Are there named verticals?
4. What are the top-cited product strengths based on customer reviews (G2, Capterra)?

### Output Format

```markdown
# Product/Service Analysis
**Confidence:** [overall section confidence]
**Sources consulted:** [list]

## Key Findings
- [Claim] [Tier] (Source: name, URL)
...

## Unanswered Questions
- [Unanswered questions]
```

---

## Section 3: Team / Leadership

**Report heading:** `## 3. Team / Leadership`
**Responsible agent:** Company Agent
**Output file:** `/tmp/investigation_company_agent.md` (Section 3 block)

### Primary Sources
- Company About / Team page
- LinkedIn profiles of founders and C-suite (individual profiles)
- Official press releases announcing hires or departures
- Crunchbase people section
- News articles mentioning leadership changes

### Key Questions (agent must address all 4)
1. Who are the founders — names, roles at founding, and professional background prior to this company?
2. Who currently leads the company (CEO, CTO, CPO, CFO, or equivalent titles) — names and brief backgrounds?
3. Are there notable advisors or board members — names and their relevant credentials?
4. Have there been any recent executive changes (hires, departures, role changes) in the last 18 months?

### Output Format

```markdown
# Team / Leadership
**Confidence:** [overall section confidence]
**Sources consulted:** [list]

## Key Findings
- [Claim] [Tier] (Source: name, URL)
...

## Unanswered Questions
- [Unanswered questions]
```

---

## Section 4: Business Model

**Report heading:** `## 4. Business Model`
**Responsible agent:** Company Agent
**Output file:** `/tmp/investigation_company_agent.md` (Section 4 block)

### Primary Sources
- Company website (pricing, sales/contact pages, partner pages)
- Press interviews and founder interviews (TechCrunch, podcast transcripts, etc.)
- Job postings (reveal go-to-market motion, e.g., "Account Executive — Enterprise" vs "growth marketing")
- Customer reviews on G2/Capterra (reveal procurement motion, contract length clues)
- LinkedIn posts or interviews from sales/GTM leadership

### Key Questions (agent must address all 3)
1. What is the primary revenue model — SaaS subscription, usage-based/consumption, marketplace/take-rate, services, licensing, freemium, or a combination?
2. How does the company acquire customers — product-led growth (PLG/self-serve), sales-led (inbound or outbound), channel/partner-led, or a hybrid?
3. What is the typical contract motion — self-serve/credit card, SMB velocity sales, mid-market AE-led, or enterprise multi-stakeholder deal?

### Output Format

```markdown
# Business Model
**Confidence:** [overall section confidence]
**Sources consulted:** [list]

## Key Findings
- [Claim] [Tier] (Source: name, URL)
...

## Unanswered Questions
- [Unanswered questions]
```

---

## Section 5: Market & Competitors

**Report heading:** `## 5. Market & Competitors`
**Responsible agent:** Market Agent
**Output file:** `/tmp/investigation_market_agent.md` (Section 5 block)

### Primary Sources
- Web search for market category definition and sizing (Gartner, Forrester, IDC reports)
- G2 category pages (lists competitors and category positioning)
- Capterra "Alternatives to [Company]" pages
- Competitor company websites
- Analyst reports and market maps (publicly available)
- News articles about the market category

### Key Questions (agent must address all 4)
1. What market category or sub-category does this company operate in — use the industry's own terminology where possible?
2. Who are the top 3–5 direct competitors — names, one-line descriptions, and approximate size/stage if known?
3. How does the company differentiate itself from competitors — based on product positioning, pricing, target segment, or technology claims?
4. What is the approximate total addressable market (TAM) size — cite the source and date of any market sizing figure?

### Positioning Signals Note

The Market Agent also captures any positioning language competitors use against this company (e.g., "alternative to X" landing pages, competitive comparison pages). These signals should be noted as findings with `[Unconfirmed]` or `[Reported]` tier based on source.

### Output Format

```markdown
# Market & Competitors
**Confidence:** [overall section confidence]
**Sources consulted:** [list]

## Key Findings
- [Claim] [Tier] (Source: name, URL)
...

## Competitor Table
| Competitor | Description | Stage/Size | Key Differentiator |
|---|---|---|---|
| [Name] | [1 line] | [Tier] (Source) | [1 line] |

## Positioning Signals
- [Competitor X positions against this company as: ...] [Tier] (Source: name, URL)

## Unanswered Questions
- [Unanswered questions]
```

---

## Section 6: Financials & Funding

**Report heading:** `## 6. Financials & Funding`
**Responsible agent:** Financial/News Agent
**Output file:** `/tmp/investigation_financial_news_agent.md` (Section 6 block)

### Primary Sources
- Crunchbase company profile (funding rounds, investors)
- PitchBook public data (if accessible)
- Company press releases announcing funding rounds
- News articles (TechCrunch, Bloomberg, Reuters, Forbes) covering funding rounds
- SEC filings or regulatory filings (for public companies or required disclosures)
- Founder/CEO interviews mentioning ARR or growth milestones

### Key Questions (agent must address all 4)
1. What is the total funding raised to date — dollar amount, number of rounds, and from which notable investors?
2. What is the most recent funding round — amount, date, round stage (Seed/Series A/B/C/etc.), and lead investor?
3. Are there any public revenue figures or ARR signals — exact figures with source, or credible estimates with explicit labeling as estimates?
4. What is the approximate valuation — at last round or current estimate — and what is the source?

All financial figures must follow the Financial Figure Rules in `/references/source-credibility.md` without exception.

### Output Format

```markdown
# Financials & Funding
**Confidence:** [overall section confidence]
**Sources consulted:** [list]

## Key Findings
- [Claim] [Tier] (Source: name, URL)
...

## Funding Summary
| Round | Amount | Date | Lead Investor | Tier | Source |
|---|---|---|---|---|---|
| [e.g., Series B] | [$XXM] | [YYYY-MM] | [Name] | [Tier] | [Source] |

## Unanswered Questions
- [Unanswered questions]
```

---

## Section 7: News & Sentiment

**Report heading:** `## 7. News & Sentiment`
**Responsible agent:** Financial/News Agent
**Output file:** `/tmp/investigation_financial_news_agent.md` (Section 7 block)

### Primary Sources
- Google News search (company name, last 12 months)
- TechCrunch, Bloomberg, Reuters, Forbes, Wired, VentureBeat articles (last 12 months)
- G2 review summaries (most recent reviews, positive and negative themes)
- Capterra review summaries
- Glassdoor company reviews (overall rating, top themes)
- Analyst coverage (Gartner Peer Insights, Forrester Wave mentions)

### Key Questions (agent must address all 4)
1. What are the most significant news stories about this company in the last 12 months — summarize each with date and source?
2. What do customers say — what are the top 2–3 positive themes and top 2–3 negative themes from review platforms?
3. What do employees say on Glassdoor — overall rating, top praise themes, top criticism themes?
4. Has the company received notable analyst coverage (Gartner Magic Quadrant, Forrester Wave, IDC MarketScape) — and what was the positioning?

### Output Format

```markdown
# News & Sentiment
**Confidence:** [overall section confidence]
**Sources consulted:** [list]

## Key Findings
- [Claim] [Tier] (Source: name, URL)
...

## Customer Sentiment Summary
- Positive themes: [theme 1], [theme 2], [theme 3] [Tier] (Source: G2/Capterra)
- Negative themes: [theme 1], [theme 2], [theme 3] [Tier] (Source: G2/Capterra)
- Overall G2 rating: [X.X/5] [Reported] (Source: G2, URL)
- Overall Glassdoor rating: [X.X/5] [Reported] (Source: Glassdoor, URL)

## Unanswered Questions
- [Unanswered questions]
```

---

## Section 8: Red Flags / Risks

**Report heading:** `## 8. Red Flags / Risks`
**Responsible agent:** Financial/News Agent
**Output file:** `/tmp/investigation_financial_news_agent.md` (Section 8 block)

### Primary Sources
- Google News (company name + "lawsuit", "controversy", "breach", "layoffs", "fraud")
- Public court records (PACER for US, Companies House for UK)
- Glassdoor reviews (patterns of negative employee feedback, management red flags)
- Reddit and Hacker News (treat as `[Unconfirmed]` — flag sentiment patterns only, do not assert facts)
- G2/Capterra (patterns of churn-indicating reviews: "switching away", "cancelled", "disappointed")
- Regulatory databases (FTC, SEC enforcement actions)

### Key Questions (agent must address all 4)
1. Is there any pending or recently resolved litigation — describe the nature, parties, and current status?
2. Have there been any executive departures (C-suite or VP level) in the last 18 months — who left, when, and was a reason given?
3. Are there any product controversies, data breaches, security incidents, or regulatory investigations on record?
4. Are there patterns in customer reviews or community discussions suggesting high churn, product instability, or support failures?

### Output Format

```markdown
# Red Flags / Risks
**Confidence:** [overall section confidence]
**Sources consulted:** [list]

## Key Findings
- [Claim] [Tier] (Source: name, URL)
...

## Risk Summary
| Risk Type | Description | Severity | Tier | Source |
|---|---|---|---|---|
| [Litigation / Executive Departure / Product / Sentiment] | [1-line description] | [Low/Medium/High] | [Tier] | [Source] |

## Unanswered Questions
- [Unanswered questions]
```

If no red flags are found after a thorough search, the agent must state: "No red flags identified after searching [list of sources]. This absence of evidence is not evidence of absence — independent verification is recommended."

---

## Section 9: Tech Stack / Engineering

**Report heading:** `## 9. Tech Stack / Engineering`
**Responsible agent:** AI Moat Agent
**Output file:** `/tmp/investigation_ai_moat_agent.md` (Section 9 block)

### Primary Sources
- BuiltWith.com (infer front-end, analytics, hosting stack from public data)
- Job postings on the company careers page, LinkedIn Jobs, and Indeed (reveal required technologies)
- GitHub (if the company has an open-source presence — check for public repos)
- Company engineering blog (look for posts about infrastructure, architecture, tooling)
- Stackshare.io (if the company has a listed profile)
- Press articles about engineering or infrastructure decisions

### Key Questions (agent must address all 4)
1. What is the approximate tech stack — front-end, back-end, data/ML infrastructure, cloud provider — based on available signals?
2. Are they actively hiring engineers, and in what specialties (front-end, back-end, ML/AI, data, security, platform)?
3. Do they have an engineering blog, open-source repositories, or public technical content that signals engineering culture?
4. Is there evidence of proprietary technical differentiation — notable patents, unique infrastructure choices, or published research?

### Output Format

```markdown
# Tech Stack / Engineering
**Confidence:** [overall section confidence]
**Sources consulted:** [list]

## Key Findings
- [Claim] [Tier] (Source: name, URL)
...

## Inferred Tech Stack
| Layer | Technology | Confidence | Source |
|---|---|---|---|
| Front-end | [e.g., React] | [Tier] | [BuiltWith / job posting] |
| Back-end | [e.g., Python/Django] | [Tier] | [job posting] |
| Cloud | [e.g., AWS] | [Tier] | [engineering blog] |
| ML/AI | [e.g., PyTorch, HuggingFace] | [Tier] | [job posting] |

## Unanswered Questions
- [Unanswered questions]
```

---

## Section 10: AI Moat Analysis

**Report heading:** `## 10. AI Moat Analysis`
**Responsible agent:** AI Moat Agent
**Output file:** `/tmp/investigation_ai_moat_agent.md` (Section 10 block)

### Primary Sources
- Company product pages and feature descriptions (for AI capability claims)
- Job postings for AI/ML/data science roles (signal investment in AI)
- Press and news articles mentioning AI, machine learning, or proprietary models
- Company blog posts or white papers on AI/ML methodology
- Patent databases (USPTO, EPO) for ML/AI-related filings
- Web search for academic papers or research output by company staff

### Key Questions (agent must address all 4)
1. Does the company use AI in its core product — is AI central to the product value proposition, or a supplementary feature?
2. Is the company training proprietary models (custom data, fine-tuned models, or foundational research), or using off-the-shelf AI APIs (OpenAI, Anthropic, Google, AWS AI services) with minimal differentiation?
3. How many current open job postings are for AI/ML/data science roles, and what level of seniority/specialization do they require?
4. What is the AI defensibility score — assessed as **Low / Medium / High / Strong** — with a written rationale?

### AI Defensibility Scoring Rubric

Use this rubric to assign the defensibility score. Apply judgment based on evidence gathered; cite the evidence for each point.

| Score | Criteria |
|---|---|
| **Strong** | Company trains proprietary models on unique/proprietary data, has published AI research, has ML patents, and AI is the primary product differentiator |
| **High** | Company fine-tunes models on proprietary data or has built significant ML infrastructure; AI is central to product and not easily replicated by competitors using off-the-shelf APIs |
| **Medium** | Company uses AI prominently in the product but primarily via third-party APIs or models; some workflow or data differentiation exists but switching to a competitor's AI layer would be feasible |
| **Low** | AI is a feature layer on top of an otherwise non-AI product; company uses off-the-shelf APIs with minimal customization; any competitor could replicate the AI capability quickly |

### Output Format

```markdown
# AI Moat Analysis
**Confidence:** [overall section confidence]
**Sources consulted:** [list]

## Key Findings
- [Claim] [Tier] (Source: name, URL)
...

## AI Moat Assessment
**Score:** [Low / Medium / High / Strong]
**Rationale:** [2-4 sentences explaining the score based on evidence]

| Signal | Evidence | Tier | Source |
|---|---|---|---|
| Proprietary model training | [Yes/No/Unclear] | [Tier] | [Source] |
| Unique training data | [Yes/No/Unclear] | [Tier] | [Source] |
| AI/ML hiring volume | [X open roles] | [Tier] | [Source] |
| Published AI research | [Yes/No] | [Tier] | [Source] |
| AI patents | [Yes/No] | [Tier] | [Source] |
| Core vs. feature AI | [Core/Feature/Supplementary] | [Tier] | [Source] |

## Unanswered Questions
- [Unanswered questions]
```

---

## Agent Output File Structure

Each agent writes all of its sections into a single Markdown file at the path specified below. Sections must be written in order with a horizontal rule (`---`) between them.

| Agent | Output File |
|---|---|
| Company Agent | `/tmp/investigation_company_agent.md` |
| Market Agent | `/tmp/investigation_market_agent.md` |
| Financial/News Agent | `/tmp/investigation_financial_news_agent.md` |
| AI Moat Agent | `/tmp/investigation_ai_moat_agent.md` |

### Standard Section Block Template

Every section written by every agent must follow this exact structure:

```markdown
# {Section Name}
**Confidence:** [Verified / Reported / Unconfirmed — use the lowest tier present in findings]
**Sources consulted:**
- Source name — URL — date accessed or date of publication

## Key Findings
- Finding 1 [Tier] (Source: name, URL)
- Finding 2 [Tier] (Source: name, URL)
- Finding 3 [Tier] (Source: name, URL)
...

## Unanswered Questions
- Question text — reason it could not be answered (e.g., "no public data found", "behind paywall", "conflicting sources")
```

### Rules for Writing Output Files

1. Do not skip a section because it seems irrelevant — write the section and note what was found or not found.
2. Do not omit the "Unanswered Questions" block — if all questions were answered, write "None."
3. Use the exact tier badge syntax: `[Verified]`, `[Reported]`, `[Unconfirmed]`.
4. If a conflict between sources is found, apply the Conflict Resolution rules from `/references/source-credibility.md` and embed the `CONFLICT:` block directly in the Key Findings section.
5. The overall section **Confidence** rating is always the lowest tier that appears in that section's findings. If any finding is `[Unconfirmed]`, the section confidence is `[Unconfirmed]`.
