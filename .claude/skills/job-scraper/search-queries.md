# Search Queries for Job Scraper

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. None ship with AI Job Search: copy the ones for your market from [community-portals](https://github.com/ai-job-search-dev/community-portals) (e.g. `linkedin-search`, `freehire-search` under `portals/global/`), or build one with `/add-portal`. You do **not** need a matching `site:` line below for those CLIs to run.

The `site:` query templates in this file are the **WebSearch fallback** — for portals without a CLI, company career pages, or when a CLI fails.

**Language scope:** write every query category in every language listed in your CLAUDE.md Languages table (typically 1-2, sometimes more). A posting requiring a language you have *not* declared, as a job condition, is excluded before scoring; a posting requiring a *higher level* than you declared in a language you *do* work in is flagged for your own judgment, not excluded — see `04-job-evaluation.md`'s Language Gate, the single source of truth for this rule. Translate each category's keywords rather than machine-translating word-for-word (e.g. "Frontend Developer" -> "Desarrollador Frontend", not a literal word-for-word translation) if you work in more than one language.

## Search Sites

Primary (US job market):
- **linkedin.com/jobs** - LinkedIn job listings (filter: Dallas, Seattle, California)
- **indeed.com** - Indeed job board
- **glassdoor.com** - Glassdoor job listings (also useful for company reviews/salary research)
- **builtinseattle.com** / **builtin.com** - Built In network (Seattle and national tech job boards)

Secondary (company career pages via Google):
- Direct Google searches with `site:` filters for known target companies (none identified yet - add as they come up)

## Query Categories

Queries are grouped by priority. Write **each category in every language from your Languages table** (see Language scope above). Combine each query with location terms (Dallas, Seattle, or California) where the site supports it.

Each priority has two kinds of block. **Plain terms** blocks are what the portal CLIs consume: one term per line, one CLI call per term, no `OR`, no `site:` prefix, and no location (the CLI's location flag, or the city in `--query` where that portal's SKILL.md says so, carries it). Quote a multi-word phrase only if the portal's `Query syntax:` line says quoting is honoured. **WebSearch-only** blocks are Google syntax (`site:`, quotes, `OR`) for the fallback path and are never passed to a CLI.

**Organize by function, not job title.** The same underlying work carries different titles across companies and markets (a "Data Scientist" role at one employer may be posted as "Insights Analyst" or "Data Consultant" at another). Name each priority category after the function it covers, and list several plausible job titles as query variants within that category rather than betting an entire priority tier on one exact title string.

### Priority 1: Software Engineer (Full-Stack)

These match the strongest and most desired career direction - full-stack roles spanning React/frontend and backend (Java, serverless).

#### Plain terms (portal CLIs)

```
Software Engineer
Full Stack Engineer
Full Stack Developer
```

#### WebSearch-only (`site:` fallback)

```
site:linkedin.com/jobs "Software Engineer" Dallas
site:linkedin.com/jobs "Software Engineer" Seattle
site:linkedin.com/jobs "Software Engineer" California
site:indeed.com "Full Stack Engineer" Dallas OR Seattle OR California
```

### Priority 2: Backend / Cloud Engineer

These match domain expertise in AWS Lambda, serverless, and GraphQL.

#### Plain terms (portal CLIs)

```
Backend Engineer
Backend Software Engineer
Cloud Engineer
```

#### WebSearch-only (`site:` fallback)

```
site:linkedin.com/jobs "Backend Engineer" AWS Dallas OR Seattle OR California
site:indeed.com "Backend Software Engineer" GraphQL
site:linkedin.com/jobs "Cloud Engineer" AWS Lambda Seattle OR California
```

### Priority 3: Adjacent Roles

Adjacent roles to pivot into.

#### Plain terms (portal CLIs)

```
Software Developer
Application Developer
```

#### WebSearch-only (`site:` fallback)

```
site:linkedin.com/jobs "Software Developer" React Dallas OR Seattle OR California
site:indeed.com "Application Developer" JavaScript Python
```

### Priority 4: Broader Technical / Consulting

Wider net for general technical roles (Ford is currently a Technical Consultant at Pariveda Solutions).

#### Plain terms (portal CLIs)

```
Software Engineer
Technical Consultant
```

#### WebSearch-only (`site:` fallback)

```
site:linkedin.com/jobs "Technical Consultant" software Dallas OR Seattle OR California
site:indeed.com "Software Engineer" entry level OR "2 years experience"
```

## Location Filter

When evaluating results, check the job location against these tiers:
- **Dallas, TX** and surrounding areas - ideal (current base)
- **Seattle, WA** - ideal (open to relocation)
- **California** (any major tech hub - SF Bay Area, LA, San Diego) - ideal (open to relocation)
- Fully remote (US) - acceptable
- Any other location requiring relocation - flag with the user before proceeding, not yet discussed

## Language Filter

Your working languages and levels are in CLAUDE.md's Languages table. When filtering scraped results, apply `04-job-evaluation.md`'s Language Gate: a posting requiring a language you haven't declared at all is excluded; a posting requiring a higher level than you declared in a language you do work in is not excluded, flag it clearly instead (see `job-scraper/SKILL.md`'s Step 3 "Quick Fit Assessment" for how the flag surfaces in `/scrape` output). Postings simply *written* in a language you don't work in, that don't require it on the job, are fine.

## Date Filter

Only include jobs posted within the last 14 days, matching `/scrape` Step 1b.3: use a supported recency filter or filter the returned publication dates client-side. A future application deadline does not bypass this discovery window; `/rank` handles deadline expiry and urgency separately after discovery. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus. For example:
- "/scrape backend" -> Priority 2 queries + custom backend-specific queries
