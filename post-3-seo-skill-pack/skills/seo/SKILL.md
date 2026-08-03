---
name: seo
description: "Comprehensive SEO analysis for any website or business type. Full site audits, single-page analysis, technical SEO (crawlability, indexability, Core Web Vitals with INP), schema markup, content quality (E-E-A-T), image optimization, sitemap analysis, and GEO for AI Overviews/ChatGPT/Perplexity. Industry detection for SaaS, e-commerce, local, publishers, agencies. Triggers on: SEO, audit, schema, Core Web Vitals, sitemap, E-E-A-T, AI Overviews, GEO, technical SEO, content quality, page speed."
---

## Runtime and safety

This skill was imported from a Claude/claude-seo package. Treat its source-specific slash commands, `claude-seo` commands, Claude subagents, and named MCP tools as references, not executable instructions. Use only tools that are actually available in the current session. Never claim a crawl, API result, benchmark, or validation result without evidence. Start with read-only inspection. Do not change a production website, DNS, robots.txt, sitemap, CMS, analytics, or deployment without explicit approval, a backup or rollback path, and verification. Keep API keys and private site data out of prompts and output. Verify current SEO rules and metrics against authoritative sources when they may have changed.

For the user's sites, prioritize practical technical SEO for self-hosted infrastructure, monitoring, virtualization, networking, DevOps, automation, applied AI, and web performance. Use the exact domain and project supplied in the request. Do not invent business facts, keywords, traffic, rankings, backlinks, or competitors.

# SEO: Universal SEO Analysis Skill

**Invocation:** `/seo $1 $2` where `$1` is the command and `$2` is the URL or argument.

**Runtime:** Run bundled Python tools through `claude-seo run <script.py>`. Plugin
installs expose this command automatically. Repository users run
`./bin/claude-seo`; manual installers rewrite the command to the isolated
launcher path. Never invoke bundled scripts with a bare Python interpreter.

Comprehensive SEO analysis across all industries (SaaS, local services,
e-commerce, publishers, agencies). Orchestrates 24 sub-skills (21 core + 1 framework
integration + 2 extension mirrors) and 18 sub-agents. A separate optional Firecrawl
extension is also installable (see "Optional Extensions" below).

## Quick Reference

| Command | What it does |
|---------|-------------|
| `/seo audit <url>` | Full website audit with parallel subagent delegation |
| `/seo page <url>` | Deep single-page analysis |
| `/seo sitemap <url or generate>` | Analyze or generate XML sitemaps |
| `/seo schema <url>` | Detect, validate, and generate Schema.org markup |
| `/seo images <url or optimize>` | Image SEO: on-page audit, SERP analysis, file optimization |
| `/seo technical <url>` | Technical SEO audit (9 categories) |
| `/seo content <url>` | E-E-A-T and content quality analysis |
| `/seo content-brief <topic or url>` | Generate detailed SEO content brief with target keywords, outline, internal links |
| `/seo geo <url>` | AI Overviews / Generative Engine Optimization |
| `/seo plan <business-type>` | Strategic SEO planning |
| `/seo programmatic [url\|plan]` | Programmatic SEO analysis and planning |
| `/seo competitor-pages [url\|generate]` | Competitor comparison page generation |
| `/seo local <url>` | Local SEO analysis (GBP, citations, reviews, map pack) |
| `/seo maps [command] [args]` | Maps intelligence (geo-grid, GBP audit, reviews, competitors) |
| `/seo hreflang [url]` | Hreflang/i18n SEO audit and generation |
| `/seo google [command] [url]` | Google SEO APIs (GSC, PageSpeed, CrUX, Indexing, GA4) |
| `/seo backlinks <url>` | Backlink profile analysis (free: Moz, Bing, CC; premium: DataForSEO) |
| `/seo cluster <seed-keyword>` | SERP-based semantic clustering and content architecture |
| `/seo sxo <url>` | Search Experience Optimization: page-type analysis, user stories, personas |
| `/seo drift baseline <url>` | Capture SEO baseline for change monitoring |
| `/seo drift compare <url>` | Compare current state to stored baseline |
| `/seo drift history <url>` | Show drift history over time |
| `/seo ecommerce <url>` | E-commerce SEO: product schema, marketplace intelligence |
| `/seo firecrawl [command] <url>` | Full-site crawling and site mapping (extension) |
| `/seo dataforseo [command]` | Live SEO data via DataForSEO (extension) |
| `/seo image-gen [use-case] <description>` | AI image generation for SEO assets (extension) |
| `/seo flow [stage] [url\|topic]` | FLOW framework: evidence-led prompts for Find, Leverage, Optimize, Win, or Local stages |
| `/seo setup` | Explicitly create or refresh the isolated Python runtime and Chromium |
| `/seo doctor` | Check runtime readiness without changing the system |

## Runtime Setup

Run setup only when the user explicitly invokes `/seo setup` or explicitly asks
to repair dependencies. Execute `claude-seo setup`, report core and Chromium
status separately, and do not fall back to global or user package installation.
For diagnosis, execute `claude-seo doctor --json`; its output intentionally omits
absolute paths and environment values. If any `claude-seo run` command reports
that setup is required, suggest `/seo setup` and do not improvise a `pip install`.

## Orchestration Logic

When the user invokes `/seo audit`, delegate to subagents in parallel:
1. Detect business type (SaaS, local, ecommerce, publisher, agency, other)
2. Spawn subagents: seo-technical, seo-content, seo-schema, seo-sitemap, seo-performance, seo-visual, seo-geo
3. If Google API credentials detected (`claude-seo run google_auth.py --check`), also spawn seo-google agent
4. If local business detected, also spawn seo-local agent
5. If local business detected AND DataForSEO MCP available, also spawn seo-maps agent
6. If backlink APIs detected (`claude-seo run backlinks_auth.py --check`), also spawn seo-backlinks agent
7. If Firecrawl MCP available, use `firecrawl_map` to discover all site URLs before analysis
8. If content strategy signals detected (blog, pillar pages, topic clusters), also spawn seo-cluster agent
9. If e-commerce detected, also spawn seo-ecommerce agent
10. If drift baseline exists for this URL (`claude-seo run drift_history.py <url>`), also spawn seo-drift agent
11. Always include seo-sxo in full audits (search experience applies to all sites)
12. Collect results and generate unified report with SEO Health Score (0-100)
13. **Synthesize via the 10-principle framework** (see "Synthesis Methodology" below), walk PERCEIVE → ANALYZE → VALIDATE → ACT before bucketing findings into Critical / High / Medium / Low
14. Create prioritized action plan with dependency sequencing + falsifiability per recommendation
15. **Offer PDF report**: "Generate a professional PDF report? Use `/seo google report full`"

For individual commands, load the relevant sub-skill directly.
After any analysis command completes, offer to generate a PDF report via `scripts/google_report.py`.

## Synthesis Methodology

Audits are not just findings, they are findings synthesized into a coherent
strategy. claude-seo uses a 10-principle thinking framework grouped into four
phases: **PERCEIVE** (observe-external · observe-internal · listen),
**ANALYZE** (think · connect-lateral · connect-system), **VALIDATE** (feel ·
accept), **ACT** (create · grow).

Full audits (`/seo audit`, `/seo page`) walk every phase before emitting the
action plan. Narrower commands (`/seo schema`, `/seo images`, etc.) pass at
least THINK + ACCEPT before emitting (sound first principle, surfaced
falsifiability). The Critical / High / Medium / Low priority buckets are the
**output** of validation, not a substitute for it.

Full methodology + per-principle SEO mapping: `references/thinking-framework.md`.

Each emitted recommendation should carry:
- The first-principle observation it rests on (THINK)
- The dependency on / unblock relationship to other recommendations (CONNECT-system)
- An explicit "how would we know this failed?" check (ACCEPT)
- A leading indicator the user can monitor without re-running the audit (GROW)

## Industry Detection

Detect business type from homepage signals:
- **SaaS**: pricing page, /features, /integrations, /docs, "free trial", "sign up"
- **Local Service**: phone number, address, service area, "serving [city]", Google Maps embed --> auto-suggest `/seo local` for deeper analysis
- **E-commerce**: /products, /collections, /cart, "add to cart", product schema
- **Publisher**: /blog, /articles, /topics, article schema, author pages, publication dates
- **Agency**: /case-studies, /portfolio, /industries, "our work", client logos

## Quality Gates

Read `references/quality-gates.md` for thin content thresholds per page type.
Hard rules:
- WARNING at 30+ location pages (enforce 60%+ unique content)
- HARD STOP at 50+ location pages (require user justification)
- Never recommend HowTo schema (deprecated Sept 2023)
- FAQ schema: Google retired FAQ rich results for ALL sites on May 7, 2026 (no SERP feature anymore; supersedes the Aug 2023 gov/health restriction). Flag existing FAQPage at Info (not Critical); do not claim confirmed AI/LLM citation benefit; do not recommend removal; do not recommend new FAQPage for Google SERP benefit; use QAPage for genuine user Q&A
- All Core Web Vitals references use INP, never FID