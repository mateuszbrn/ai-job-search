# Search Queries for Job Scraper

<!-- SETUP: Customize these queries based on your skills, target roles, and location -->

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. Shipped country-agnostic CLIs include `linkedin-search` and `freehire-search`; Danish demos and any skill you add with `/add-portal` are included the same way. You do **not** need a matching `site:` line below for those CLIs to run.

The `site:` query templates in this file are the **WebSearch fallback** — for portals without a CLI, company career pages, or when a CLI fails.

**Language scope:** write every query category in every language listed in your CLAUDE.md Languages table (typically 1-2, sometimes more). A posting requiring a language you have *not* declared, as a job condition, is excluded before scoring; a posting requiring a *higher level* than you declared in a language you *do* work in is flagged for your own judgment, not excluded — see `04-job-evaluation.md`'s Language Gate, the single source of truth for this rule. Translate each category's keywords rather than machine-translating word-for-word (e.g. "Frontend Developer" -> "Desarrollador Frontend", not a literal word-for-word translation) if you work in more than one language.

## Search Sites

Primary (your market's job boards - scaffold one with `/add-portal`):
- **pracuj.pl** - Poland's largest general job board (no CLI yet - run `/add-portal` to scaffold one; used as a WebSearch `site:` fallback until then)
- **linkedin.com/jobs** - LinkedIn job listings (filter: Poland / Kraków); also covered by `linkedin-search` CLI
- **nofluffjobs.com** - niche board for tech/IT roles (optional; also candidate for `/add-portal`)
- **justjoin.it** - another major Polish tech job board (optional; also candidate for `/add-portal`)

Secondary (company career pages via Google):
- Direct Google searches with `site:` filters for known target companies

## Query Categories

Queries are grouped by priority. Write **each category in every language from your Languages table** (see Language scope above). Combine each query with your location terms (e.g. your city, region, or metro area) where the site supports it.

**Organize by function, not job title.** The same underlying work carries different titles across companies and markets (a "Data Scientist" role at one employer may be posted as "Insights Analyst" or "Data Consultant" at another). Name each priority category after the function it covers, and list several plausible job titles as query variants within that category rather than betting an entire priority tier on one exact title string.

### Priority 1: Fund Administration / Financial Operations

These match your strongest and most desired career direction (current role type).

```
site:pracuj.pl "Fund Accountant" Kraków
site:pracuj.pl "Fund Administrator" Kraków
site:pracuj.pl "Financial Operations Analyst" Kraków
site:pracuj.pl "Fund Expense Analyst" Kraków
site:linkedin.com/jobs "Fund Accountant" Poland
site:linkedin.com/jobs "Fund Administrator" Poland
```

### Priority 2: Data / Reporting / Process Automation

Adjacent to your current work - built on Excel/VBA/Python automation experience.

```
site:pracuj.pl "Data Analyst" Kraków
site:pracuj.pl "Reporting Analyst" Kraków
site:pracuj.pl "Process Automation Analyst" Kraków
site:pracuj.pl "Junior Business Analyst" Kraków
site:linkedin.com/jobs "Data Analyst" Poland Excel VBA
```

### Priority 3: AI / Automation (pivot direction)

Roles to grow into as the current AI/automation learning plan progresses.

```
site:nofluffjobs.com "AI Implementation" Kraków
site:justjoin.it "Junior AI" OR "Automation Engineer" Kraków
site:linkedin.com/jobs "Prompt Engineer" Poland
site:linkedin.com/jobs "Junior Machine Learning Engineer" Poland
```

### Priority 4: Broader Technology (wide net)

Entry-level technology roles - candidate is willing to learn on the job.

```
site:nofluffjobs.com "IT Support Specialist" Kraków
site:justjoin.it "Junior Software Developer" Kraków
site:linkedin.com/jobs "Graduate Programme" technology Poland
```

**Key skill search terms (combine with the above as needed):** Excel, VBA, Python, fund accounting, process automation, AI

## Location Filter

When evaluating results, verify the job location matches the candidate's constraints:
- **Kraków and surrounding areas** - hybrid or fully on-site, always acceptable
- **Anywhere in Poland** - acceptable if remote
- **Anywhere worldwide** - acceptable only if remote or willing to relocate, AND compensation reaches 20,000+ PLN net equivalent
- No borderline/too-far commute tiers apply (no daily-commute-from-home constraint stated)

## Language Filter

Your working languages and levels are in CLAUDE.md's Languages table. When filtering scraped results, apply `04-job-evaluation.md`'s Language Gate: a posting requiring a language you haven't declared at all is excluded; a posting requiring a higher level than you declared in a language you do work in is not excluded, flag it clearly instead (see `job-scraper/SKILL.md`'s Step 3 "Quick Fit Assessment" for how the flag surfaces in `/scrape` output). Postings simply *written* in a language you don't work in, that don't require it on the job, are fine.

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus. For example:
- "/scrape [focus_area]" -> relevant category queries + custom focus-specific queries
