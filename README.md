# et-research-cowork

Company investigation skill for Claude Cowork. Paste a company URL, get a scannable HTML report for pre-meeting prep.

## What it does

1. **Quick scan** — reads the company URL, confirms what you're looking at
2. **Deep research** — dispatches parallel agents across 4 research dimensions
3. **HTML report** — delivers a polished, scannable report with source credibility badges

## Report Sections

| Section | Coverage |
|---------|----------|
| Company Overview | What they do, founding story, HQ, size |
| Product/Service Analysis | Offerings, pricing, positioning |
| Team/Leadership | Founders, key executives, backgrounds |
| Business Model | Revenue streams, how they make money |
| Market & Competitors | Market size, key competitors, differentiation |
| Financials & Funding | Funding rounds, revenue, valuation |
| Tech Stack / Engineering | Technologies used, hiring signals |
| News & Sentiment | Recent press, reviews, reputation |
| Red Flags / Risks | Lawsuits, controversies, churn signals |
| AI Moat Analysis | AI defensibility, AI adoption, competitive moat |

## Source Credibility

Every claim is tagged with a credibility tier:

- **Verified** — company-sourced or 2+ independent sources agree
- **Reported** — single reputable source (major news, G2, Capterra, etc.)
- **Unconfirmed** — single uncertain source or inferred

## Usage

```
/investigate <company-url>
```

## License

MIT
