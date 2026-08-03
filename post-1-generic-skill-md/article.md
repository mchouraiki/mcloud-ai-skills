---
title: "How I Create Reusable AI Skills with SKILL.md"
author: "Moustafa Chouraiki"
category: "AI and Automation"
published: "2026-08-03"
description: "A practical guide to turning repeatable technical work into reusable AI skills with SKILL.md, core guidance and simple validation."
slug: "guides/how-to-create-reusable-ai-skills-with-skill-md"
---

# How I Create Reusable AI Skills with `SKILL.md`

I kept seeing the same problem in AI-assisted work.

The assistant could produce a good answer, but only after I repeated the same instructions every time. Inspect the real source first. Do not change production without approval. Do not touch authentication or SEO metadata. Tell me exactly what was checked.

That is not a reliable workflow. It is a prompt that has to be rebuilt from memory on every request.

The better approach is to document the workflow once and load it when the task needs it.

That is what a reusable AI skill does.

## What is a `SKILL.md` file?

`SKILL.md` is a Markdown instruction file for one repeatable job.

It tells an assistant:

- when the workflow applies;
- what input it needs;
- which steps to follow;
- what it must not assume;
- when it must stop and ask for approval;
- what the final response must contain;
- how the result must be validated.

The format is simple on purpose. It is readable by people, easy to review in Git, and usable by different AI tools that support Markdown instructions.

The important point is that the file describes a process. It does not train the model.

## The structure I use

```text
my-skill/
  SKILL.md
  references/
  scripts/
  assets/
```

Only `SKILL.md` is required. The other folders are useful when they contain something the workflow actually needs.

| Folder | Purpose |
|---|---|
| `SKILL.md` | The workflow, boundaries and output format |
| `references/` | Standards, schemas, policies and detailed background |
| `scripts/` | Deterministic checks and repeatable calculations |
| `assets/` | Templates, examples and reusable files |

I keep the main file focused. If it turns into a large technical manual, the assistant has to load too much context before it can do the actual work.

## A real example

Here is the kind of skill I use before making a technical change:

```md
---
name: safe-technical-change
description: Inspect and plan a scoped technical change when the user requests a website, application or infrastructure change.
---

# Safe Technical Change

Use this skill before changing a website, application or infrastructure component.

## Required input

- Exact target
- Requested change
- Known environment and deployment path
- Required approval and rollback expectations

## Workflow

1. Restate the requested scope and exclusions.
2. Identify the authoritative source and deployment path.
3. Inspect the current implementation before editing.
4. Identify the smallest safe change.
5. Ask for approval before destructive, production or externally visible actions.
6. Make the change only after the scope and rollback path are clear.
7. Validate the requested behaviour and report exactly what changed.

## Do not assume

- Do not assume a generated file is the authoritative source.
- Do not assume a service, route or API is safe to change.
- Do not assume a backup or test exists because somebody mentioned it.
- Do not claim validation passed if it was not run.

## Stop conditions

- Ask for clarification if the target, scope or deployment path is missing.
- Stop if the rollback path cannot be identified.
- Stop before production changes when approval is not clear.

## Output

Return:

1. Scope and exclusions
2. Discovery findings
3. Proposed change
4. Approval or rollback requirement
5. Files or components changed
6. Validation performed
7. Remaining risk
```

This is more useful than a vague instruction such as "fix this website". The assistant knows what to inspect, what it cannot assume and what the final report should contain.

The package accompanying this article includes this generic example, reusable core guidance and a practical MCloud example for safe technical changes.

## Keep common rules separate

The specialist skill should not contain every rule that applies to every task.

I keep common behaviour in a separate core guidance file. That file can contain rules such as:

- inspect before changing anything;
- separate facts from assumptions;
- protect credentials and private data;
- ask before destructive or production actions;
- preserve unrelated systems and configuration;
- provide complete commands and validation steps;
- never claim a test passed if it was not run.

The task skill then adds only the specialist workflow.

This separation matters. If I change the approval rule, I should not have to edit ten different skills. If I update one specialist workflow, I should not accidentally change the rules for infrastructure work.

## How I use this in MCloud work

The same structure works across the type of work I do.

For a website change, the skill can require the assistant to identify the authoritative source and deployment path before editing. That prevents the common mistake of changing generated files while the real source is somewhere else.

For an infrastructure investigation, the skill can require read-only discovery first, evidence collection, a proposed change, approval, implementation and validation.

The same pattern works for any focused audit, where the skill can require read-only discovery, clear evidence and a distinction between a confirmed issue and a recommendation.

The tools are different, but the discipline is the same: understand the environment before touching it.

## Skills are not memory

A skill defines how a task should be performed. It does not remember previous conversations.

If the assistant needs stable facts, keep them separately:

```text
profile.md       Stable user and project facts
style.md         Preferred writing and response style
memory.db        Approved summaries and decisions
SKILL.md         The task workflow
```

Do not place passwords, API keys, private tokens, customer data or confidential infrastructure details in a reusable skill.

Load only the relevant memory and the relevant skill. Sending the entire history with every request wastes context and makes irrelevant answers more likely.

## Skills are not scripts

Use the skill to describe decisions and workflow boundaries. Use scripts for work that should be deterministic.

For example, a skill can tell the assistant to check a sitemap. A script can parse the XML, count URLs and report invalid entries consistently.

That gives you a useful division:

```text
SKILL.md       judgment, order of work and safety boundaries
scripts/       repeatable checks
references/    supporting knowledge
assets/        templates and examples
```

The assistant should still report what it actually ran. A script existing in the folder does not mean the check was performed.

## Using the same skill with different tools

The Markdown structure can travel between local LLM wrappers, ChatGPT, Codex, OpenCode and other coding agents. The installation path and invocation command cannot be assumed to be identical.

For a local `llama.cpp` setup, the wrapper must load the core guidance, select the relevant skill and inject both into the request sent to the model server.

Codex and other agents may discover skills from their own supported directories or use explicit invocation. Follow the current documentation for that host.

The portable part is the content and structure. The host-specific part is where the file is installed, how it is selected and which tools the assistant can actually use.

## Test a new skill before trusting it

I would test at least these five cases:

1. A direct request that should activate the skill.
2. An indirect request describing the same job.
3. An incomplete request that should produce a clarification question.
4. A request outside the skill scope that should not activate it.
5. A dangerous or unsupported request that should stop or ask for approval.

Also check that the output contains evidence, validation steps and no invented results.

## What a skill cannot do

A `SKILL.md` file cannot provide credentials, install tools, bypass permissions or guarantee that the assistant will make a correct decision.

It improves consistency. It gives the assistant a documented workflow and clear boundaries. The actual result still depends on the model, the available tools, the quality of the input and the validation performed afterwards.

That is why I treat skills as operational documentation, not magic prompts.

## Before publishing or installing

Check that:

- the name is specific and unique;
- the description explains when the skill should trigger;
- required inputs are clear;
- unsupported assumptions are listed;
- stop and approval conditions are defined;
- validation is included;
- private information is excluded;
- the license and attribution are clear;
- the skill has been tested against direct, indirect, incomplete and unsafe requests.

## Download and related guides

Download the generic core guidance and examples here:

[Download the Post 1 files from GitHub](https://github.com/mchouraiki/mcloud-ai-skills/tree/main/post-1-generic-skill-md)

The next two posts apply the same thinking to real technical work:

- [Web development skill guide](https://mcloudsolutions.net/guides/ai-skill-safer-web-development/)
- [SEO skills guide](https://mcloudsolutions.net/guides/ai-skills-technical-seo-content-website-audits/)

## Sources

- [OpenAI: Build skills](https://developers.openai.com/plugins/build/skills/)
- [Agent Skills specification](https://agentskills.io/specification)

The package also includes a `SOURCES.md` file with attribution and licensing notes.
