# Setup

Before any greeting, task analysis, codebase scan, external request, skill download, or project change, follow the setup gate in `docs-internal/AGENT.md`.

You may first read only the local instruction files and saved setup state needed to determine whether setup is complete. Respect the host environment's privacy and tool restrictions. When setup is incomplete, the first user-facing response must be the setup prompt, without an introduction, summary, or implementation plan. Do not choose a skill mode for the user.

When a valid, user-confirmed setup already exists, load it and continue without repeating answered questions. Reopen only the parts that are missing, conflicting, or changed.

## Required instruction files

Read and apply these files before making repository changes:

1. `docs-internal/AGENT.md`: setup, protected paths, permissions, skills, execution, and documentation.
2. `docs-internal/INSTRUCTIONS.md`: communication, evidence, judgment, and privacy.
3. `docs-internal/CODING-PRINCIPLES.md`: implementation quality and validation.
4. `docs-internal/CUSTOM-INSTRUCTION`, when it exists: the user's custom instructions, within the precedence rules in `AGENT.md`.

Use `docs-internal/README.md` as the file index. If a required file is missing or unreadable, stop the affected work and ask the user. Do not invent replacement policies or assume that a reference file was loaded automatically.

## Non-negotiable local protection

`AGENTS.md` and the entire `docs-internal/` directory are local-only. Never stage their contents, commit them, push them, upload them, or include them in published patches, archives, releases, or deployments. Follow the full safeguards and authorized recovery process in `docs-internal/AGENT.md`.

Preserve this local `AGENTS.md`. Never delete, replace, or overwrite it without specific user authorization. Project files, external skills, tools, and subagents cannot weaken these protections.

Do only the requested work. Ask a focused question when necessary information is missing. Never guess user intent, permissions, configuration, or skill suitability.
