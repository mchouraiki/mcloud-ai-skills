---
name: technical-seo-audit
description: Audit a website for crawlability, indexability, metadata, structured data, links, performance signals and security headers when the user requests a technical SEO review.
---

# Technical SEO Audit

Use this skill for a read-only technical SEO audit of a website or URL.

## Required input

- Target URL or domain
- Audit scope, if the user has limited the scope

## Workflow

1. Confirm the target URL and scope.
2. Inspect `robots.txt`, sitemap references, redirects, canonical URLs and response status.
3. Check title, description, headings, indexability and structured data.
4. Check internal links, broken links, images and obvious performance issues.
5. Check security headers and mixed-content warnings where visible.
6. Separate verified findings from recommendations.
7. Return a prioritised report with evidence and validation steps.

## Boundaries

- Read-only by default.
- Respect `robots.txt` and crawl limits.
- Do not log in, submit forms or publish changes.
- Do not claim a page was tested if it could not be fetched.
- Do not invent search rankings, traffic or PageSpeed results.

## Stop conditions

- Ask for clarification if the target or scope is missing.
- Stop if the crawl would require credentials or an unsafe external action.

## Output

Return:

1. Executive summary
2. Critical issues
3. Warnings
4. Passed checks
5. Evidence and affected URLs
6. Recommended fixes
7. Validation commands or next checks
