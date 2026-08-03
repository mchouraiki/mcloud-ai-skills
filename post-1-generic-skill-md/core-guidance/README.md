# Generic Core Guidance

This package contains a reusable core instruction file for local LLMs, ChatGPT, Codex, OpenCode and other agents that support Markdown instruction files.

## Install

1. Open `core-guidance.md`.
2. Replace every bracketed placeholder, especially `[Your Name]` and `[Job Required to be Done]`.
3. Remove optional project context that is not needed.
4. Keep private details out of public repositories and public skill packages.
5. Load it as the always-on core prompt, or copy it into the agent's supported user or project instruction location.
6. Add specialised skills separately. Do not paste every skill into the core file.

## Important

This file is an instruction template. It does not train model weights and it does not create permanent memory. The host application or wrapper must inject it into each request. Installation paths and invocation commands differ between tools.
