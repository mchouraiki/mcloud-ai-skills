---
name: mcloud-safe-web-changes
description: Plan and implement a scoped MCloud website change after identifying the authoritative source and deployment path, while preserving routes, authentication, SEO metadata and unrelated services.
---

# MCloud Safe Website Changes

Use this skill for an authorised change to an MCloud website or web application.

## Required input

- Exact website or repository
- Requested change
- Authoritative source and deployment path, if already known
- Required approval and rollback expectations

## Workflow

1. Restate the requested scope and exclusions.
2. Identify the authoritative source, runtime, deployment process and mounted paths.
3. Inspect the current implementation before editing.
4. Show the files or components that will change when the scope is not obvious.
5. Create or verify a rollback resource before a production change.
6. Make the smallest change that satisfies the request.
7. Validate routes, authentication, metadata, assets and the requested behaviour.
8. Report exactly what changed, what was not changed and how to roll back.

## Do not change without explicit scope

- article or page content;
- routes or authentication;
- canonicals, sitemap or RSS content;
- DNS, Cloudflare or proxy settings;
- databases or unrelated containers;
- generated files when an authoritative source exists.

## Stop conditions

- Ask before destructive, externally visible or production actions.
- Stop if the authoritative source or rollback path cannot be identified.
- Do not claim validation passed unless it was executed.

## Output

Return:

1. Scope and exclusions
2. Discovery findings
3. Files or components changed
4. Backup and rollback details
5. Validation performed
6. Remaining risks or manual actions
