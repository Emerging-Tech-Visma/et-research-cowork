# How we built company-investigation

It started with a familiar feeling: opening a calendar invite 15 minutes before a call, seeing a company name you barely recognise, and frantically Googling while trying to look like you knew who they were all along.

We've all been there. A quick LinkedIn crawl. A TechCrunch search. Maybe a Crunchbase tab if you're organised. Five minutes later you have seven browser tabs, three conflicting funding figures, and no idea which one to trust. You walk into the meeting with fragments — not a picture.

That frustration became the design brief: one command, one report, walk in ready.

---

## Trust nothing, label everything

The first thing we decided was that we wouldn't just pull facts from the web and present them as truth. That's the obvious thing to build, and it's the wrong thing to build.

Company information on the internet is a mess. A TechCrunch article from 2022 still ranks above a press release from last month. LinkedIn headcount numbers are notoriously inflated. Anonymous Glassdoor reviews sit next to verified funding announcements with no indication of which one you should actually believe.

So we built a credibility framework first — before a single line of skill logic was written. Every claim in the report gets tagged:

```
[Verified]     — Company's own URL, or 2+ independent sources agree
[Reported]     — Single reputable source (Reuters, G2, Bloomberg, etc.)
[Unconfirmed]  — Social media, forums, inferred, or estimated
```

And critically: when two sources disagree, the report flags the conflict explicitly rather than silently picking one side. A `CONFLICT:` block shows both claims with their sources and lets you decide. Appearing confident when the data is actually ambiguous is worse than useful.

---

## Why 4 agents, not 1

The naive version of this skill is a single agent that searches the web and writes a report. We built that version mentally and immediately saw the problem: research domains don't transfer cleanly to sequential execution.

By the time a single agent finishes researching the company's product, it's already used up context that could have been spent on financials. By the time it gets to competitors, it's half-remembering what it found about the founding team. The output is shallow on everything because it's trying to do everything.

The solution was obvious once we framed it as a team problem. Four specialists, working in parallel:

- **Company Agent** — reads the company's own website and public profiles. Sections 1–4: who they are, what they sell, who runs it, how they make money.
- **Market Agent** — searches G2, Capterra, analyst reports. One job: map the competitive landscape.
- **Financial/News Agent** — Crunchbase, press, Glassdoor. Funding history, recent news, red flags.
- **AI Moat Agent** — job postings, GitHub, engineering blogs. Is AI actually defensible here, or just a feature wrapper?

Each writes findings to a temp file independently. A synthesis pass merges everything, resolves conflicts, and generates the final report. The tradeoff is real: the skill takes 3–10 minutes versus 2 minutes for a basic web search. We tested both. The quality difference is not subtle.

---

## The report had to work offline

There was a constraint we set early: the HTML report cannot depend on the internet to render. No CDN links. No external fonts. No remote stylesheets.

The reason is practical. You generate the report at your desk, then you walk into a meeting room with questionable WiFi. Or you forward it to a colleague who opens it on a plane. Or you print it. If the report is a beautiful skeleton because `cdn.tailwind.css` didn't load, it's useless at the moment it matters most.

So everything is inlined. The CSS is in a `<style>` block. The fonts fall back to system stacks. Collapsible sections use native `<details>`/`<summary>` elements — no JavaScript required for the basic toggle. Dark mode comes from a `prefers-color-scheme` media query. Print styles force all sections open and hide the chrome.

The template is ~800 lines of vanilla HTML/CSS. It renders identically in Chrome, Safari, Firefox, and a PDF printer.

---

## What testing taught us

We ran three live investigations before shipping: Linear, Drata, and Intercom.

The Linear run confirmed the core flow worked. The Drata run revealed something embarrassing: we had labelled it a "sparse coverage" test case — a company that would stress-test how the skill handles limited public data. Drata turned out to be a G2 Leader for 15 consecutive quarters with a $2B valuation and a $250M acquisition in 2025. Not sparse. The skill handled it fine; our test design had been lazy.

The Intercom run tested something more interesting: whether the skill would trigger from natural language without the `/investigate` command. The prompt was *"I have a big meeting with Intercom tomorrow, can you help me prep?"* The skill matched it correctly — no slash command needed. That made the whole thing feel like it was actually designed for humans.

Overall pass rate against our structured assertions: **94.4% with the skill, 27.8% without**. The gap is almost entirely in the things that matter — credibility labels, structured sections, AI Moat Score, source attribution.

---

## What it doesn't do yet

v1.0 is deliberately narrow. It researches one company per invocation. It uses only public information — no Bloomberg Terminal, no PitchBook API, no paid data sources. It doesn't monitor companies over time or alert you when something changes.

Those aren't oversights. They're the next version. The foundation — the credibility framework, the parallel agent architecture, the self-contained output — is built to extend. Comparison reports across multiple companies, integration with internal CRM data, scheduled digests before recurring meetings. The skeleton is there.

---

For now, it does one thing well: you paste a URL, and you walk in ready.
