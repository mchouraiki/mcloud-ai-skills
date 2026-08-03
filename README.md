# How to Create Reusable AI Skills with `SKILL.md`

This repository contains the practical files for the MCloud Solutions guide:

**How to Create Reusable AI Skills with `SKILL.md`**

The guide is written mainly for people using ChatGPT and Codex to perform repeated technical work. It also explains how the same instruction structure can be adapted for OpenCode, local LLM wrappers and other compatible AI agents.

## What this gives you

An ordinary prompt tells the AI what you want once. A reusable skill documents how the work should be performed every time.

Adding these files gives you:

- less repetition when starting a technical task;
- more consistent results between conversations and projects;
- clear rules for what the AI must inspect before editing;
- explicit safety boundaries for production systems, secrets and destructive actions;
- repeatable output requirements, testing steps and validation checks;
- a versioned workflow that can be improved instead of rebuilt from memory;
- a package that can be shared with a team or reused with compatible AI tools.

This is an instruction layer. It is not model training, permanent memory or a replacement for reviewing the AI's work.

## ChatGPT and Codex use

The primary use case is to add the files to a ChatGPT or Codex workflow as project guidance, reference material or a reusable skill package, depending on the ChatGPT surface and account features available to you.

The practical pattern is:

1. Keep `core-guidance.md` as the common rules for how the AI should work.
2. Add a task-specific `SKILL.md` when you need a defined workflow, such as technical SEO or web development.
3. Give the AI the relevant project files and ask it to use the guidance before making changes.
4. Review the proposed plan and approve production changes separately.
5. Keep the package under version control so changes to the workflow are visible.

`SKILL.md` is the standard individual skill filename. Automatic discovery, file locations and permission handling vary between ChatGPT, Codex, OpenCode and local LLM wrappers. The structure is portable, but copying the file does not automatically install it in every tool.

## Repository contents

| Path | Purpose |
| --- | --- |
| [`article/`](article/) | Full website article source |
| [`templates/core-guidance.md`](templates/core-guidance.md) | Generic shared guidance template |
| [`examples/technical-seo/SKILL.md`](examples/technical-seo/SKILL.md) | Complete task-specific example |
| [`docs/compatibility.md`](docs/compatibility.md) | ChatGPT, Codex, OpenCode and local LLM notes |
| [`docs/sources.md`](docs/sources.md) | Sources and attribution |
| [`downloads/`](downloads/) | Clean downloadable archive |

## Download

[Download the reusable `SKILL.md` and core guidance package](downloads/mcloud-ai-skills-skill-md-core-guidance.zip)

The archive contains the article, generic template, example skill, compatibility notes, sources, license and changelog. It contains only public documentation and reusable examples.

## The three-guide series

This guide is the foundation for the series:

1. **How to Create Reusable AI Skills with `SKILL.md`**
2. **Using AI Skills for Safer Web Development**
3. **Using AI Skills for Technical SEO, Content and Website Audits**

The second and third guides will be published as separate packages. They are not included here.

## Website

Read the complete guide on MCloud Solutions:

https://mcloudsolutions.net/guides/create-reusable-ai-skill-skill-md-core-guidance/

The website article is the main explanation. This repository contains the reusable files and download package that support it.

## License and attribution

The documentation and templates are released under the license in [`LICENSE`](LICENSE). See [`docs/sources.md`](docs/sources.md) for attribution and source information.
