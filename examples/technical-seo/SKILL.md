---
name: technical-seo-audit
description: Audit a website for crawlability, indexability, metadata, structured data, performance and internal linking. Use when reviewing a site or page for technical SEO issues and improvement priorities.
---

# Technical SEO Audit

## When to use

Use this skill when the user asks for a technical SEO audit, page audit, indexability review, sitemap or robots.txt check, structured data validation, or prioritized technical SEO recommendations.

## Inputs required

- Website URL or local project path
- Audit scope, if the user has specified one
- Access credentials only when the user explicitly provides an approved authenticated workflow

## Workflow

1. Confirm the target URL, scope and whether the audit is read-only.
2. Inspect the authoritative source or live site before making recommendations.
3. Check HTTPS, redirects, robots.txt, XML sitemaps, canonical URLs, titles, descriptions, headings, indexability and structured data.
4. Review internal links, broken links, image alternatives and obvious performance signals.
5. Separate observed facts from assumptions and tool limitations.
6. Rank findings by impact, confidence and implementation effort.
7. Return evidence, affected URLs, recommended fixes and validation steps.

## Safety boundaries

- Do not change production files, DNS, Cloudflare, robots.txt or metadata without explicit approval.
- Do not submit URLs, build backlinks or publish content unless separately authorised.
- Do not expose credentials, private URLs or personal data.
- Do not describe a page as indexed without a source that verifies index status.

## Output requirements

Return:

- Scope and date checked
- Tools or sources used
- Passed checks
- Findings with evidence and severity
- Prioritized remediation plan
- Checks that were not possible and why
