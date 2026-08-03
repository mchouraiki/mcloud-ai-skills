# Compatibility and installation notes

This package is designed primarily for ChatGPT and Codex-style technical workflows.

## ChatGPT and Codex

Use `core-guidance.md` as shared project guidance and use a task-specific `SKILL.md` when the task requires a defined process. Depending on the ChatGPT or Codex surface, the files may be added as project instructions, uploaded reference files or installed into a supported skills directory.

The exact discovery and permission model is controlled by the host product. Always confirm that the AI has loaded the relevant files before relying on them.

## Other tools

The same Markdown structure can be adapted for OpenCode and local LLM wrappers, but the folder location, automatic discovery, tool permissions and invocation command may be different.

The file format is portable. The installation process is not automatically identical.
