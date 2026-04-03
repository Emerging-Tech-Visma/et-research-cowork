# Agent Prompts Reference

This file contains the full instructions to pass to each of the four parallel research agents in Step 2. Read the relevant agent section before dispatching. All agents must also read `references/source-credibility.md` and `references/report-sections.md` before writing their findings.

---

## Agent 1 — Company Agent

**Goal:** Research the company directly from its own website and public profiles.

**Sections covered:** 1 — Company Overview, 2 — Product/Service Analysis, 3 — Team/Leadership, 4 — Business Model

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

## Agent 2 — Market Agent

**Goal:** Research the competitive landscape and market positioning.

**Sections covered:** 5 — Market & Competitors

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

## Agent 3 — Financial/News Agent

**Goal:** Research funding, financials, press coverage, and risk signals.

**Sections covered:** 6 — Financials & Funding, 7 — News & Sentiment, 8 — Red Flags / Risks

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

## Agent 4 — AI Moat Agent

**Goal:** Assess AI usage, tech stack signals, and engineering presence.

**Sections covered:** 9 — Tech Stack / Engineering, 10 — AI Moat Analysis

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
