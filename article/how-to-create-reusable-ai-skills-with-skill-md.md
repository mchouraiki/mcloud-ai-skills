# How to Create Reusable AI Skills with SKILL.md

> Original article: [MCloud Solutions](https://mcloudsolutions.net/guides/how-i-create-reusable-ai-skills-with-skill-md/)

AI becomes much more useful when it understands how you want recurring work done.

If every website audit, code review or infrastructure task starts with the same long prompt, the process is not reusable yet. The better approach is to turn that working method into a small, versioned package that an AI agent can discover and load when needed.

That package is an AI skill.

The key file is called `SKILL.md`.

## What is an AI skill?

An AI skill is a folder containing instructions for a repeatable task. The folder normally includes:

```text
my-skill/
├── SKILL.md
├── scripts/       optional deterministic tools
├── references/    optional supporting documentation
└── assets/        optional templates and files
```

`SKILL.md` is the required entry point. It tells the agent what the skill does, when it should be used and how the workflow should be performed.

The important distinction is that a skill is not just a saved prompt. A good skill defines a complete working method, including its boundaries, checks, expected output and conditions where the agent must stop and ask questions.

## Why the filename matters

The standard filename is `SKILL.md`, with capital letters exactly as shown.

The file is normally placed inside a folder named after the skill:

```text
technical-seo/
└── SKILL.md
```

The folder name should be short, lowercase and hyphenated. The metadata inside the file should contain at least `name` and `description`:

```markdown
---
name: technical-seo
description: Audit crawlability, indexability, metadata, schema and performance. Use when reviewing a website for technical SEO problems.
---
```

The open Agent Skills specification defines `name` and `description` as required metadata. The name is limited to lowercase letters, numbers and hyphens, with a maximum length of 64 characters. The description must explain both the capability and the situations where it should be used.

## Core guidance versus task skills

I keep two different types of instructions separate.

### Core guidance

The shared file, for example `core-guidance.md`, contains personal or project-wide behaviour:

- Use short, clear explanations
- Preserve existing routes and metadata
- Inspect before editing
- Ask before destructive actions
- Validate changes before reporting success
- Keep secrets out of logs and chat
- Respect the author's voice and formatting preferences

This guidance applies broadly. It does not need to describe how to perform one specific job.

### Task skill

A task skill contains the workflow for one type of work:

- Technical SEO auditing
- Web development and deployment
- Zabbix troubleshooting
- Database performance analysis
- Network configuration backup
- PDF generation and verification

The task skill should be narrow enough that the agent can recognise when it applies. If one file attempts to control every possible task, it becomes difficult to discover, maintain and test.

The practical model is:

```text
Core guidance: how the agent should work
Task skill: how to perform this type of work
Project rules: how this repository or website is structured
```

## How the model discovers a skill

The agent usually sees the skill's metadata first, especially its name and description. The full body is loaded only when the skill is considered relevant.

This is called progressive loading or progressive disclosure. It keeps the initial context smaller and lets the agent load detailed instructions only when they are useful.

This makes the description one of the most important parts of the skill. A vague description may never trigger. An over-broad description may trigger for unrelated tasks.

Weak description:

```yaml
description: Helps with websites.
```

Better description:

```yaml
description: Review and improve HTML, CSS, JavaScript, PHP and React websites while preserving routes, SEO metadata and deployment structure. Use when editing an existing website or validating a web change.
```

The description should answer two questions:

1. What does this skill do?
2. When should the agent use it?

## What belongs in SKILL.md?

Keep the main file focused on the workflow. A useful structure is:

```markdown
# Skill title

## When to use
...

## Inputs required
...

## Workflow
1. Inspect...
2. Plan...
3. Change...
4. Test...

## Safety boundaries
...

## Output requirements
...

## Supporting files
- Read references/checklist.md when...
- Run scripts/validate.py when...
```

The agent already knows how to reason, write code and explain results. The skill should add the task-specific knowledge it would otherwise have to rediscover every time.

Do not fill the file with general motivational text, repeated model instructions or a large reference manual that is never needed.

## References, scripts and assets

Use supporting folders when the information or logic is too detailed for the main workflow.

### References

Use `references/` for material the agent may need to read:

- API notes
- Database schemas
- Editorial standards
- Vendor-specific commands
- A security checklist
- Examples of accepted output

Link to each reference directly from `SKILL.md` and explain when to read it. Avoid deeply nested chains of references.

### Scripts

Use `scripts/` for deterministic work that should be executed consistently:

- Validate JSON or YAML
- Check links
- Render a document
- Calculate a checksum
- Compare configuration files
- Generate a report

Do not add a script merely because the agent can run code. Add one when it improves repeatability, safety or accuracy.

### Assets

Use `assets/` for files that should be copied or used in the result:

- A website starter template
- A report template
- A logo
- A configuration example
- A document style file

Keep assets separate from references so the agent knows which files are instructions and which files are output material.

## Local LLM usage

The same design works with a local model, but the loading mechanism depends on the application around the model.

A local model does not automatically understand a folder just because it contains `SKILL.md`. Your wrapper, editor integration or agent runtime must discover the skill, select it and include its contents in the request.

A practical local setup is:

```text
User request
    ↓
Skill matcher
    ↓
Load SKILL.md
    ↓
Load only required references
    ↓
Run scripts when needed
    ↓
Return result and validation evidence
```

For a local Qwen or similar model, start with a simple implementation:

1. Scan known skill directories.
2. Read the frontmatter from each `SKILL.md`.
3. Match the request against the descriptions.
4. Inject the selected skill into the system or developer context.
5. Let the model decide whether to load a referenced file.
6. Keep scripts available as executable tools rather than pasting every script into context.

This is also where a memory system should remain separate. Memory stores facts about the user or previous work. A skill stores the procedure for performing a task. Combining them into one large prompt makes both harder to control.

## Download the template and example

The accompanying package includes a generic `core-guidance.md` template and a complete technical SEO example skill:

https://github.com/mchouraiki/mcloud-ai-skills

Use the files as a starting point, then adapt the boundaries, validation steps and project rules to your own environment. Review the license and attribution requirements before redistributing modified material.

## What comes next

This is the first article in a three-part series. The next articles cover safer web development workflows and a practical SEO skill pack for technical SEO, content and website audits.

## ChatGPT, Codex and OpenCode compatibility

The Agent Skills format is designed to be portable, but the discovery locations and tool permissions still belong to each application.

ChatGPT and Codex use skills as reusable workflows and load the detailed `SKILL.md` instructions when the skill is relevant.

Codex also supports broader project guidance such as `AGENTS.md`. That is useful for repository-specific commands and conventions. A task skill should remain a skill instead of becoming a huge `AGENTS.md` file.

OpenCode supports native Agent Skills and searches configured project or global skill directories. It also supports compatible `.claude/skills/` and `.agents/skills/` locations, depending on the configuration and version in use.

The portable part is the folder structure and `SKILL.md` format. The application-specific parts are:

- Where the folder is stored
- How the skill is discovered
- Which tools the agent can call
- Whether scripts need explicit permission
- How project rules override or combine with global guidance

Do not assume that copying a skill into a directory automatically gives the agent permission to execute every script inside it.

## A generic SKILL.md template

Start small and adapt the template to one workflow:

```markdown
---
name: replace-with-lowercase-name
description: Describe what this skill does and when the agent should use it.
---

# Workflow title

## Use this skill when

- The request involves...
- The user asks for...

## Do not use this skill when

- The request is only...
- Another specialist workflow is more appropriate.

## Inputs required

- Identify the project, files or URL.
- Ask for missing information before making changes.

## Workflow

1. Inspect the authoritative source.
2. Identify constraints and risks.
3. Explain the proposed change.
4. Make the smallest safe change.
5. Run focused validation.
6. Report what changed and what remains.

## Safety boundaries

- Do not expose secrets.
- Do not modify unrelated files.
- Do not delete data without confirmation.
- Stop when the target or authority is ambiguous.

## Supporting files

- Read `references/checklist.md` when the detailed checklist is needed.
- Run `scripts/validate.py` after changing structured files.

## Output

Return a concise summary, changed files, validation results and any follow-up action.
```

## How to create a skill

The best starting point is not a blank file. Start with a real task that you have already completed successfully.

Write down:

- The exact request that started the work
- The files or systems inspected
- The decisions that mattered
- The checks that prevented mistakes
- The final output expected by the user

Then turn the repeated process into a workflow.

Keep environment-specific details in references or configuration. Keep dangerous operations explicit. Define what the agent must inspect before editing and what evidence is required before it can say the task is complete.

For example, a web-development skill should not merely say "fix the website." It should say how to find the authoritative source, how to preserve routes and SEO metadata, which tests to run and when deployment requires confirmation.

## How to test a skill

Test the skill with at least five types of request:

1. A direct request that should activate it
2. An indirect request with the same intent
3. An incomplete request that should cause a question
4. An unrelated request that should not activate it
5. A risky request where the skill should stop or require confirmation

Review both activation and output quality. A skill can fail before the workflow starts if its description is poor. It can also activate correctly but produce unsafe results if the body lacks boundaries or validation steps.

Version skills in Git. Keep a small changelog in commit messages or release notes, and test again after changing the description because discovery behaviour can change even when the workflow body does not.

## Copyright and licensing

A skill may include original instructions, code, documentation, templates and references. You still need to check the rights for anything copied from another project.

Before publishing a skill:

- Read the source repository's license
- Preserve copyright and attribution notices
- Do not copy proprietary documentation into a public package
- Mark modified files clearly when required
- Keep third-party code under its original license
- Add your own license for original material
- Link to the original project when attribution is required

If you build on another project's workflow, explain what was reused and what you changed. Attribution is not a substitute for permission when the license does not allow redistribution.

## The practical rule

Put permanent working principles in shared core guidance. Put one repeatable workflow in each task skill. Put detailed references, deterministic scripts and reusable files beside `SKILL.md`.

That structure is small enough to maintain, clear enough to test and portable enough to use across modern AI coding and agent tools.

The next two posts apply the same model to practical work:

- [Using AI Skills for Safer Web Development](https://mcloudsolutions.net/guides/ai-skill-safer-web-development/)
- [Using AI Skills for Technical SEO, Content and Website Audits](https://mcloudsolutions.net/guides/ai-skills-technical-seo-content-website-audits/)

Download the generic core guidance template and use it as the starting point for your own workflow library.

## Sources and further reading

- [OpenAI: Build skills](https://developers.openai.com/codex/build-skills)
- [OpenAI: Skills in the API](https://developers.openai.com/api/docs/guides/tools-skills)
- [Agent Skills specification](https://agentskills.io/specification)
- [OpenCode: Agent Skills](https://opencode.ai/docs/skills/)
- [OpenCode: Rules and project guidance](https://opencode.ai/docs/rules/)
