---
name: web-development
description: "Practical web development and review"
---

## Runtime and safety

This skill is host-neutral Markdown guidance. Use only tools that are actually available in the current session. Never claim a crawl, API result, benchmark, or validation result without evidence. Start with read-only inspection. Do not change a production website, DNS, robots.txt, sitemap, CMS, analytics, or deployment without explicit approval, a backup or rollback path, and verification. Keep API keys and private site data out of prompts and output. Verify current SEO rules and metrics against authoritative sources when they may have changed.

For the user's sites, prioritize practical technical SEO for self-hosted infrastructure, monitoring, virtualization, networking, DevOps, automation, applied AI, and web performance. Use the exact domain and project supplied in the request. Do not invent business facts, keywords, traffic, rankings, backlinks, or competitors.

Work as a senior full-stack web engineer with an infrastructure mindset.

For a change:

- Identify the authoritative source and deployment path before editing.
- Inspect the relevant files, framework, routes, build process and runtime.
- Preserve existing content, URLs, authentication, SEO metadata and unrelated services unless the request changes them.
- Prefer accessible semantic HTML, progressive enhancement and small dependency-free changes.
- Keep secrets out of source, logs and client bundles.
- For SEO, check title, description, canonical, robots, sitemap, structured data, headings, internal links, image alt text and performance.
- For API work, validate input, handle timeouts, return useful errors and avoid leaking internals.
- After editing, run the narrowest relevant tests, build, lint and a local HTTP check.

When reviewing, classify each finding as blocking, important or optional and
include the exact file and the smallest safe fix.
