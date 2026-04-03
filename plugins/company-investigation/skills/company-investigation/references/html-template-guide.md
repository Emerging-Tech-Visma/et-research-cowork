# HTML Report Generation Guide

This file contains all rules for generating the final HTML report in Step 3.4. Read this file in full before writing any HTML output.

---

## Template Usage

Read `templates/report.html` to understand the structural layout, CSS variables, and placeholder conventions before generating the report.

---

## Required Report Sections

The generated report must include all of the following:

1. **Report header** — company name, date of generation, source URL
2. **Executive Summary** — 3–5 bullet points formatted as "walk in knowing this" statements (the most critical facts for the meeting)
3. **AI Moat Score widget** — four levels (Low / Medium / High / Strong) with the correct level visually highlighted
4. **10 research sections** — findings as readable prose or scannable bullet points, each annotated with source credibility badges
5. **Talking Points** — 4–6 conversation starters grounded in the research findings
6. **Source Overview** — all cited sources grouped by credibility tier (Verified / Reported / Unconfirmed)

---

## Placeholder Conventions

Replace all `{{placeholder}}` variables with actual content:

| Placeholder | Value |
|---|---|
| `{{company_name}}` | Company name extracted in Step 1 |
| `{{report_date}}` | Today's date in `YYYY-MM-DD` format |
| `{{company_url}}` | The URL provided by the user |
| `{{executive_summary}}` | 3–5 bullet HTML list items |
| `{{ai_moat_score}}` | One of: `low`, `medium`, `high`, `strong` (lowercase, used for CSS class) |
| `{{section_N_content}}` | HTML content for section N (1–10) |
| `{{talking_points}}` | HTML list of 4–6 talking points |
| `{{sources_verified}}` | HTML list of Verified sources |
| `{{sources_reported}}` | HTML list of Reported sources |
| `{{sources_unconfirmed}}` | HTML list of Unconfirmed sources |

---

## Collapsible Sections — CRITICAL

**Do NOT add JavaScript for collapsible sections.**

The template uses native HTML `<details>`/`<summary>` elements. These collapse and expand without any JavaScript. Adding `onclick` attributes, `addEventListener` calls, or any `<script>` block that toggles sections creates duplicate handlers that break the toggle — the section opens then immediately closes.

- Leave all collapsible sections as plain `<details>`/`<summary>` HTML only
- No `onclick` attributes on any element
- No `addEventListener` in any `<script>` block
- No jQuery or other library toggle calls

---

## Self-Contained Requirement

The report must render correctly when opened from a local filesystem with no internet access:

- All CSS must be in a `<style>` block within the `<head>` — no external stylesheets
- No external font imports (use system font stack)
- No CDN links (no Bootstrap, Tailwind, etc.)
- No external image sources — use inline SVG or CSS shapes for icons
- No `<script src="...">` tags loading external scripts

---

## Credibility Badge Rendering

Render credibility badges as inline `<span>` elements with CSS classes:

```html
<span class="badge-verified">Verified</span>
<span class="badge-reported">Reported</span>
<span class="badge-unconfirmed">Unconfirmed</span>
```

The template's `<style>` block defines `.badge-verified`, `.badge-reported`, and `.badge-unconfirmed` with appropriate colors.

---

## Conflict Rendering

When a conflict exists between sources, render it as:

```html
<div class="conflict-block">
  <strong>CONFLICT:</strong> [Short description]<br>
  Claim A: [claim] <span class="badge-X">X</span> (Source: name)<br>
  Claim B: [claim] <span class="badge-Y">Y</span> (Source: name)<br>
  <em>These claims could not be reconciled. Verify independently.</em>
</div>
```

---

## Missing Section Rendering

If an agent did not return data for a section, render:

```html
<div class="missing-section">
  Research unavailable — agent did not return results for this section.
</div>
```

---

## Dark Mode

The template includes `@media (prefers-color-scheme: dark)` overrides via CSS custom properties. Do not remove or override these — they are already in the template's `<style>` block.
