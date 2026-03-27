# Source Credibility Framework

This document is the authoritative reference for how all research agents in the `company-investigation` skill assess, label, and surface source credibility. Every claim written into a report MUST carry a credibility tier badge and a source citation. Agents must follow these rules mechanically — no silent upgrades, no silent omissions.

---

## 3-Tier Framework

### [Verified] — Green Badge

A claim is **Verified** when it meets ONE of the following conditions:

1. The information comes directly from the **company's own URL** (official website, official press release, official investor relations page, official product docs). The company is the primary source of record for facts about itself.
2. **Two or more independent external sources** agree on the same specific claim (same number, same fact, same event). The sources must be independent — a news article quoting a press release does not count as a second independent source.

Use the badge exactly as: `[Verified]`

### [Reported] — Yellow Badge

A claim is **Reported** when it comes from a **single reputable source** and no contradicting source exists.

Reputable sources include:

- **Major news outlets:** Reuters, Bloomberg, TechCrunch, The Wall Street Journal (WSJ), Financial Times (FT), Forbes, Wired, VentureBeat
- **Major review platforms:** G2, Capterra, Trustpilot, Glassdoor
- **Analyst firms:** Gartner, Forrester, IDC
- **Government or regulatory filings:** SEC filings, Companies House (UK), court records, patent filings, official regulatory databases

A single article from a reputable outlet = `[Reported]`. If a second reputable outlet independently confirms the same fact, upgrade to `[Verified]`.

Use the badge exactly as: `[Reported]`

### [Unconfirmed] — Grey Badge

A claim is **Unconfirmed** when it comes from any of the following:

- Social media posts (X/Twitter, LinkedIn posts by individuals, Facebook)
- Reddit threads, Hacker News comments, forum posts
- Anonymous reviews (e.g., anonymous Glassdoor review with no corroboration)
- Blog posts from non-major outlets (company blogs, personal blogs, Medium posts)
- Inferred or extrapolated figures (e.g., "estimated ARR based on headcount")
- A single source that cannot be classified as reputable under the criteria above
- Any claim where the original source is unclear or cannot be traced

Use the badge exactly as: `[Unconfirmed]`

---

## Source Classification Rules

Apply these rules per source type. Rules are deterministic — do not apply judgment to override them.

| Source Type | Default Tier | Upgrade Condition |
|---|---|---|
| Company's own website / press releases / official blog | `[Verified]` | Already at top tier |
| Company investor relations page / SEC/regulatory filings | `[Verified]` | Already at top tier |
| Two or more independent external sources agreeing | `[Verified]` | N/A — this IS the upgrade condition |
| Reuters, Bloomberg, WSJ, FT, TechCrunch, Forbes, Wired, VentureBeat, Financial Times | `[Reported]` | Upgrade to `[Verified]` if a second independent source confirms |
| G2, Capterra, Trustpilot (platform-level summaries or named reviews) | `[Reported]` | Upgrade to `[Verified]` if corroborated by a second independent source |
| Glassdoor (platform-level summaries) | `[Reported]` | Same as above |
| Gartner, Forrester, IDC analyst reports | `[Reported]` | Upgrade if second independent analyst or news source confirms |
| Government filings, court records, patent databases | `[Reported]` minimum; `[Verified]` if it is the company's own filing | Based on source |
| LinkedIn company page (official) | `[Reported]` | Treat as official company-controlled channel; upgrade to `[Verified]` if it mirrors company website |
| LinkedIn individual profiles, job postings | `[Unconfirmed]` | Upgrade to `[Reported]` if corroborated by a named news article or company press release |
| X/Twitter (any account, including company official) | `[Unconfirmed]` | Upgrade only if corroborated by company website or reputable press |
| Reddit, Hacker News, forums | `[Unconfirmed]` | No upgrade path — must find a reputable source separately |
| Blog posts (non-major outlets, personal blogs, Medium) | `[Unconfirmed]` | Upgrade to `[Reported]` only if the blog post cites a primary source you can verify independently |
| Anonymous review (no named reviewer, no date) | `[Unconfirmed]` | No upgrade path |
| Inferred/extrapolated figures (e.g., ARR estimate from headcount) | `[Unconfirmed]` | No upgrade — must label as estimate; see Financial Figure Rules |
| Crunchbase, PitchBook (public data) | `[Reported]` | Upgrade to `[Verified]` if company press release or two news sources confirm |

---

## Conflict Resolution Rules

When two agents or two sources disagree on a fact, follow these rules exactly:

1. **Do not silently pick one claim over the other.** Never choose the "more likely" claim and present it as fact.
2. **Flag the conflict explicitly** in the report using this format:

```
CONFLICT: [Short description of conflicting fact]
- Claim A: [Exact claim] [Tier] (Source: name, URL)
- Claim B: [Exact claim] [Tier] (Source: name, URL)
Note: These claims could not be reconciled. Reader should verify independently.
```

3. If one source is `[Verified]` and the other is `[Unconfirmed]`, the `[Verified]` source takes precedence — but the conflict must still be noted if the discrepancy is material (e.g., a large difference in a funding figure).
4. If both sources are the same tier, flag both without preference.
5. If a claim cannot be verified at all, mark it `[Unconfirmed]` — never present it as established fact.

---

## Financial Figure Rules

Financial figures (revenue, ARR, valuation, funding amount, employee count when used as a financial signal) carry extra requirements because they are frequently misquoted, outdated, or inferred.

- **Never state a financial figure without a source citation.** No exceptions.
- If the figure comes from the company's own press release, investor relations page, or official filing → `[Verified]`
- If the figure comes from a reputable press outlet (Reuters, Bloomberg, WSJ, TechCrunch, etc.) → `[Reported]`
- If the figure comes from Crunchbase or PitchBook (public, un-cited entries) → `[Reported]`
- If the figure is **inferred** (e.g., "estimated $20M ARR based on 200 employees at typical SaaS ARR per employee ratios") → `[Unconfirmed]`; must explicitly label as "estimate" or "inferred"
- If a figure is outdated (older than 24 months), note the date of the source alongside the tier
- If multiple sources report different figures for the same metric, apply Conflict Resolution rules above

Format for financial figures in the report:

```
Revenue: ~$50M ARR [Reported] (Source: TechCrunch, https://..., 2024-09)
Funding: $120M total [Verified] (Source: Company press release, https://...; confirmed by Bloomberg, https://...)
Valuation: ~$500M [Unconfirmed] (Source: Inferred from funding round size; no public confirmation)
```

---

## Report Display Format

### Inline Citation Format

Every claim in the report body must follow this format:

```
Claim text [Tier] (Source: source name, URL)
```

Examples:

```
The company was founded in 2018 [Verified] (Source: company website, https://acme.com/about)
Total funding stands at $45M [Reported] (Source: Crunchbase, https://crunchbase.com/...)
The CEO previously worked at Stripe [Unconfirmed] (Source: LinkedIn post, https://linkedin.com/...)
```

If a claim has multiple supporting sources (making it `[Verified]`), list both:

```
The company has 300 employees [Verified] (Source: LinkedIn company page, https://...; confirmed by TechCrunch, https://...)
```

### Source Overview Section

Every report must end with a **Sources** section, structured as follows:

```
## Sources

### [Verified] Sources
- Source name — URL — date accessed/published
- ...

### [Reported] Sources
- Source name — URL — date accessed/published
- ...

### [Unconfirmed] Sources
- Source name — URL — date accessed/published
- ...
```

Group all sources used by tier. Include the date of the source where known. If no date is available, note "date unknown."

---

## Quick Reference Checklist for Agents

Before writing any claim into a report, answer these questions:

1. Do I have a source for this claim? If no → do not include the claim.
2. Is the source the company's own URL? If yes → `[Verified]`.
3. Do I have two or more independent sources confirming this? If yes → `[Verified]`.
4. Is the source a single reputable outlet (see list above)? If yes → `[Reported]`.
5. Is the source social media, Reddit, a blog, or anonymous? If yes → `[Unconfirmed]`.
6. Is the claim a financial figure? Apply Financial Figure Rules — never omit citation.
7. Is there a conflicting claim from another source or agent? Apply Conflict Resolution Rules — flag explicitly, never silently pick.
