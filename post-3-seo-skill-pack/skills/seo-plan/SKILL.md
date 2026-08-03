---
name: seo-plan
description: "Strategic SEO planning for new or existing websites. Industry-specific templates, competitive analysis, content strategy, and implementation roadmap. Use when user says \"SEO plan\", \"SEO strategy\", \"SEO planning\", \"content strategy\", \"keyword strategy\", \"content calendar\", \"site architecture\", or \"SEO roadmap\"."
---

## Runtime and safety

This skill was imported from a Claude/claude-seo package. Treat its source-specific slash commands, `claude-seo` commands, Claude subagents, and named MCP tools as references, not executable instructions. Use only tools that are actually available in the current session. Never claim a crawl, API result, benchmark, or validation result without evidence. Start with read-only inspection. Do not change a production website, DNS, robots.txt, sitemap, CMS, analytics, or deployment without explicit approval, a backup or rollback path, and verification. Keep API keys and private site data out of prompts and output. Verify current SEO rules and metrics against authoritative sources when they may have changed.

For the user's sites, prioritize practical technical SEO for self-hosted infrastructure, monitoring, virtualization, networking, DevOps, automation, applied AI, and web performance. Use the exact domain and project supplied in the request. Do not invent business facts, keywords, traffic, rankings, backlinks, or competitors.

# Strategic SEO Planning

## Process

### 1. Discovery
- Business type, target audience, competitors, goals
- Current site assessment (if exists)
- Budget and timeline constraints
- Key performance indicators (KPIs)

### 2. Competitive Analysis
- Identify top 5 competitors
- Analyze their content strategy, schema usage, technical setup
- Identify keyword gaps and content opportunities
- Assess their E-E-A-T signals
- Estimate their domain authority

### 3. Architecture Design
- Load industry template from `assets/` directory
- Design URL hierarchy and content pillars
- Plan internal linking strategy
- Sitemap structure with quality gates applied
- Information architecture for user journeys

### 4. Content Strategy
- Content gaps vs competitors
- Page types and estimated counts
- Blog/resource topics and publishing cadence
- E-E-A-T building plan (author bios, credentials, experience signals)
- Content calendar with priorities

### 5. Technical Foundation
- Hosting and performance requirements
- Schema markup plan per page type
- Core Web Vitals baseline targets
- AI search readiness requirements
- Mobile-first considerations

### 6. Implementation Roadmap (4 phases)

#### Phase 1: Foundation (weeks 1-4)
- Technical setup and infrastructure
- Core pages (home, about, contact, main services)
- Essential schema implementation
- Analytics and tracking setup

#### Phase 2: Expansion (weeks 5-12)
- Content creation for primary pages
- Blog launch with initial posts
- Internal linking structure
- Local SEO setup (if applicable)

#### Phase 3: Scale (weeks 13-24)
- Advanced content development
- Link building and outreach
- GEO optimization
- Performance optimization

#### Phase 4: Authority (months 7-12)
- Thought leadership content
- PR and media mentions
- Advanced schema implementation
- Continuous optimization

## Industry Templates

Load from `assets/` directory:
- `saas.md`: SaaS/software companies
- `local-service.md`: Local service businesses
- `ecommerce.md`: E-commerce stores
- `publisher.md`: Content publishers/media
- `agency.md`: Agencies and consultancies
- `generic.md`: General business template

## Output

### Deliverables
- `SEO-STRATEGY.md`: Complete strategic plan
- `COMPETITOR-ANALYSIS.md`: Competitive insights
- `CONTENT-CALENDAR.md`: Content roadmap
- `IMPLEMENTATION-ROADMAP.md`: Phased action plan
- `SITE-STRUCTURE.md`: URL hierarchy and architecture

### KPI Targets
| Metric | Baseline | 3 Month | 6 Month | 12 Month |
|--------|----------|---------|---------|----------|
| Organic Traffic | ... | ... | ... | ... |
| Keyword Rankings | ... | ... | ... | ... |
| Domain Authority | ... | ... | ... | ... |
| Indexed Pages | ... | ... | ... | ... |
| Core Web Vitals | ... | ... | ... | ... |

### Success Criteria
- Clear, measurable goals per phase
- Resource requirements defined
- Dependencies identified
- Risk mitigation strategies

## DataForSEO Integration (Optional)

If DataForSEO MCP tools are available, use `dataforseo_labs_google_competitors_domain` and `dataforseo_labs_google_domain_intersection` for real competitive intelligence, `dataforseo_labs_bulk_traffic_estimation` for traffic estimates, `kw_data_google_ads_search_volume` and `dataforseo_labs_bulk_keyword_difficulty` for keyword research, and `business_data_business_listings_search` for local business data.

## Error Handling

| Scenario | Action |
|----------|--------|
| Unrecognized business type | Fall back to `generic.md` template. Inform user that no industry-specific template was found and proceed with the general business template. |
| No website URL provided | Proceed with new-site planning mode. Skip current site assessment and competitive gap analysis that require a live URL. |
| Industry template not found | Check `assets/` directory for available templates. If the requested template file is missing, use `generic.md` and note the missing template in output. |
