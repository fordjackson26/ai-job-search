# Search Queries for Job Scraper

## Search Sites

Primary (US job market):
- **linkedin.com/jobs** - LinkedIn job listings (filter: Dallas, Seattle, California)
- **indeed.com** - Indeed job board
- **glassdoor.com** - Glassdoor job listings (also useful for company reviews/salary research)
- **builtinseattle.com** / **builtin.com** - Built In network (Seattle and national tech job boards)

Secondary (company career pages via Google):
- Direct Google searches with `site:` filters for known target companies (none identified yet - add as they come up)

## Query Categories

Queries are grouped by priority. Each query should be combined with location terms (Dallas, Seattle, or California) where the site supports it.

### Priority 1: Software Engineer (Full-Stack)

These match the strongest and most desired career direction - full-stack roles spanning React/frontend and backend (Java, serverless).

```
site:linkedin.com/jobs "Software Engineer" Dallas
site:linkedin.com/jobs "Software Engineer" Seattle
site:linkedin.com/jobs "Software Engineer" California
site:indeed.com "Full Stack Engineer" Dallas OR Seattle OR California
```

### Priority 2: Backend / Cloud Engineer

These match domain expertise in AWS Lambda, serverless, and GraphQL.

```
site:linkedin.com/jobs "Backend Engineer" AWS Dallas OR Seattle OR California
site:indeed.com "Backend Software Engineer" GraphQL
site:linkedin.com/jobs "Cloud Engineer" AWS Lambda Seattle OR California
```

### Priority 3: Adjacent Roles

Adjacent roles to pivot into.

```
site:linkedin.com/jobs "Software Developer" React Dallas OR Seattle OR California
site:indeed.com "Application Developer" JavaScript Python
```

### Priority 4: Broader Technical / Consulting

Wider net for general technical roles (Ford is currently a Technical Consultant at Pariveda Solutions).

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

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus. For example:
- "/scrape backend" -> Priority 2 queries + custom backend-specific queries
