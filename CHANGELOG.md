# Changelog

All notable changes to `company-investigation` are documented here.

Format: `emoji vX.Y — one-line story`

---

## 🔧 v1.1 — 2026-03-27

Fix plugin installation from GitHub and add CI/CD for `.skill` packaging.

### Fixed
- Plugin structure now matches official Anthropic layout — resolves "Plugin not found" error when installing from GitHub
- Download link in README now triggers direct `.skill` file download

### Added
- GitHub Actions workflow to auto-build and upload `.skill` file on every merge to main
- Clean release notes (no changelog preamble)

---

## 🚀 v1.0 — 2026-03-26

Walk into any meeting fully briefed — paste a URL, get a 10-section HTML report with source credibility badges in minutes.

### What's included
- Two-step flow: Quick Scan → parallel deep research
- 4 parallel agents: Company, Market, Financial/News, AI Moat
- 10 structured report sections with collapsible HTML layout
- Source credibility framework: Verified / Reported / Unconfirmed
- AI Moat Score (Low / Medium / High / Strong)
- Auto-generated talking points for meeting prep
- Self-contained HTML output — no internet needed to view
- Natural language trigger — no `/investigate` command required
- Graceful error handling: URL unreachable, obscure companies, rate limiting
