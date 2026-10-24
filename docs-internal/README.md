# docs-internal

Private, local-only guidance for coding agents and assistants. This collection separates communication rules, coding rules, workflow rules, user custom instructions, skill bundles, and project records without duplicating the complete policy in every file.

## Start with setup

Load the root `AGENTS.md` through the agent tool's supported instruction mechanism. The first agent interaction must follow the setup prompt at the top of `AGENT.md`, with no greeting, plan, codebase scan, or installation before it. A previously completed, valid setup is reused rather than repeated.

Setup asks the user to choose Auto, Guided, Manual, or Off for external project skills. It also resolves the project root when unclear, collects optional custom instructions, and obtains narrowly scoped setup-write permission. There is no automatic default mode.

Auto selects a minimal, useful set using real codebase and current-task evidence. It asks rather than guessing when suitability, compatibility, permissions, or user intent is unclear. Guided waits for approval of a shortlist. Manual uses user-selected skills. Off disables optional external project skills without deleting saved files.

## Files

| File or directory | Responsibility |
| --- | --- |
| Project-root `AGENTS.md` | Local entrypoint: start setup and load this collection |
| `AGENT.md` | Authoritative setup, local-only protection, Git permissions, skill management, documentation, retry limits, and handoff |
| `INSTRUCTIONS.md` | Communication, accuracy, evidence, historical context, judgment, and privacy |
| `CODING-PRINCIPLES.md` | Implementation scope, quality, testing, debugging, and technical decisions |
| `CUSTOM-INSTRUCTION` | Exact user-supplied instructions; create only when supplied; no extension |
| `skills/` | Selected, reviewed external skill bundles and their necessary resources |
| `docs/` | All internal project records, including setup state and skill provenance |

## Intended layout

```text
<project-root>/
|-- AGENTS.md
`-- docs-internal/
    |-- README.md
    |-- AGENT.md
    |-- CODING-PRINCIPLES.md
    |-- INSTRUCTIONS.md
    |-- CUSTOM-INSTRUCTION        # Conditional; not a fabricated placeholder
    |-- skills/                   # Initially empty
    `-- docs/
        |-- setup.md
        |-- project-map.md
        |-- findings.md
        |-- roadmap.md
        |-- decisions.md
        `-- progress.md
```

The internal folder is `docs-internal/`, without a leading dot. Its `skills/` and `docs/` children are not project-root siblings. Public application documentation is outside this collection and must not be renamed or hidden by this setup.

## Mandatory local-only policy

The root `AGENTS.md` and all of `docs-internal/` must remain local-only. Never commit, push, upload, publish, or include their contents in shared outputs or deployment artifacts. General authorization to push code does not permit sharing these files. Copies under different names remain protected.

Before writing internal project material, establish the root `.gitignore` exclusions and independent index checks specified in `AGENT.md`. Preserve existing ignore rules. Do not replace the project's `.gitignore` with a sample file.

If protected files are already tracked or exposed, stop the affected operation and follow the explicit-approval recovery procedure. Do not automatically remove files, discard staged work, or rewrite history. Preserve an existing root `AGENTS.md`; request approval for its proposed edits.

Local-only is an operational requirement, not a promise that Git ignore rules, prompts, or hooks can control every tool, archive, synchronization service, or provider. Verify actual processing and publication paths as required by `AGENT.md`.

## Skills and custom instructions

The candidate sources are `addyosmani/agent-skills`, `poteto/noodle`, and `mattpocock/skills`. Their full addresses and the review procedure are in `AGENT.md`. Discover relevant entries from current repository contents; do not assume every source has an identical layout or that its installation command is safe for this project.

Source permission is not permission to install all skills, run third-party scripts, install an orchestration runtime, modify global configuration, or publish data. Skill files stay under `skills/`; their evidence and source revisions stay in `docs/setup.md`.

Do not create `CUSTOM-INSTRUCTION` until the user provides custom instructions. When provided, save them faithfully and apply them within the safeguards and precedence rules. Do not silently substitute a `.md` filename or invent preferences.

## Template status and safe use

This deliverable is an instruction template, not a configured project or an installed skill collection. The records under `docs/` intentionally contain no invented repository facts, approvals, test results, decisions, or activity entries. The `skills/` directory starts empty. Custom instructions must be supplied by the user.

Review downloaded templates in a separate local location first. Do not blindly extract or copy them over an existing project. When adopting them, preserve existing files, obtain permission for any edits, and merge required exclusions before introducing protected material into the project. Do not stage the template package or distribute a configured copy.

These Markdown files are reference instructions, not a universal executable configuration format. Verify that the host actually loads the entrypoint and referenced rules. If it cannot load skills from the required folder, ask about manual-reference use rather than copying files into another directory.

## Maintenance

Keep each rule in its owning file. `AGENT.md` is the single detailed authority for setup and local-only protections; the root entrypoint intentionally repeats only a brief safety reminder. Keep custom instructions separate from general rules.

Update living records in place. Append, rather than rewrite, decisions and progress. Review rules for concrete, testable outcomes and conflicting requirements. Policy changes are not authorization to move existing files or modify application code.
