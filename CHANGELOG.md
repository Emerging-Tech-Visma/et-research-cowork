# Changelog

All notable changes to `company-investigation` are documented here.

Format: `emoji vX.Y — one-line story`

---

## 🧹 v1.4 — 2026-04-02

Clean repo, clear learning path — removed dev artifacts, moved BUILDING.md into docs/, ready for others to learn from.

### Changed
- Moved `BUILDING.md` into `docs/` alongside the plugin documentation
- Removed `docs/design-spec.md` (superseded by BUILDING.md)
- Removed `.github/workflows/build-skill.yml` (old `.skill` build, replaced by marketplace install)

---

## 📦 v1.3 — 2026-04-02

Install once, works everywhere — verified install steps for Claude Cowork desktop and Claude Code CLI, plus org-wide auto-discovery via settings.

### Fixed
- Plugin structure aligned with official Cowork plugin format — resolves marketplace sync failures
- SKILL.md now loads correctly when skill is triggered

### Added
- Verified install instructions for Claude Cowork (desktop) and Claude Code CLI
- `.claude/settings.json` with `extraKnownMarketplaces` for org-wide auto-discovery

---

## 🔧 v1.2 — 2026-03-27

Improve skill triggering and add zip download option.

### Fixed
- Skill description rewritten for more reliable triggering in Cowork — added assertive "MUST use" directive
- Broadened trigger phrases to catch casual company research requests

### Added
- `.zip` download as install Option 2 in README with direct download link
- CI builds `.zip`, `.plugin`, and `.skill` assets on every merge

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
