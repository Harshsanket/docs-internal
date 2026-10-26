# docs-internal

A drop-in, local-only folder that gives AI coding agents a fixed setup, a curated skill set, and one place to keep specs, plans, decisions, and handoffs. Nothing in it is committed to your project.

> This README explains the template. It is **not** copied into your project, and agents must never use it as your project's README.

## What you get

| Path | Purpose |
| --- | --- |
| `AGENT.md` | Setup gate, skill modes, folder rules, Git protection, project README format |
| `INSTRUCTIONS.md` | Communication, evidence, and judgment policy |
| `CODING-PRINCIPLES.md` | Implementation and validation policy |
| `setup.md` | Saved setup answers, so setup runs once |
| `handoff.md` | Current state for the next agent or session |
| `skills/` | Installed skills plus `INDEX.md` (source, commit SHA, why, use-when) |
| `specs/` | PRDs and specs |
| `plans/` | Roadmap and task plans |
| `decisions/` | One ADR per file |
| `map/` | Project map and domain glossary |
| `log/` | Append-only progress log and findings |

## Install

1. Copy the `docs-internal/` folder into your project root. Copy only that folder, not this README.
2. Tell your agent: `Read docs-internal/AGENT.md and run setup.`
3. Answer the setup prompt. Setup then:
   - adds `/AGENTS.md` and `/docs-internal/` to `.gitignore`
   - creates a root `AGENTS.md` pointer, so later sessions load the rules automatically
   - installs skills and saves your answers to `setup.md`

## Skill modes

| Mode | What happens |
| --- | --- |
| **Auto** | Installs the default set without asking. Adds other skills only when the codebase needs them. |
| **Guided** | Lists every skill from all three sources, with defaults pre-checked, plus a custom Git repo option. You pick. |
| **Manual** | Installs only the skills or repo URLs you name. |
| **Off** | Installs nothing. |

**Default set:** 24 skills in total.
- [Matt Pocock](https://github.com/mattpocock/skills) (5): `grill-with-docs`, `tdd`, `diagnosing-bugs`, `to-spec`, `improve-codebase-architecture`
- [Addy Osmani](https://github.com/addyosmani/agent-skills) (19): every skill except the six that overlap with Matt's skills (`test-driven-development`, `debugging-and-error-recovery`, `spec-driven-development`, `interview-me`, `documentation-and-adrs`, `idea-refine`)
- [poteto/noodle](https://github.com/poteto/noodle): available in Guided and Manual, and in Auto when the codebase shows a need

Skills are copied into `docs-internal/skills/` and pinned to a commit. Their scripts are never run. Any skill output that would normally go to the repo root, such as `GLOSSARY.md`, `docs/adr/`, or the issue tracker, is redirected into `docs-internal/`.

## Project README

At setup, the agent asks whether to create the project's README, restructure the existing one, or keep it as is. The generated README uses only verified project facts and follows this outline: Overview, Requirements, Getting Started, Configuration, How It Works, Deployment, Troubleshooting, Tests & Scripts, Security, Languages Used, License, About, Acknowledgments.

## Git protection

`AGENTS.md` and `docs-internal/` stay local. Before every commit or push, the agent checks that neither path is tracked or staged. The agent stages files by explicit path only, and never pushes without your approval. If protected files are already tracked, the agent stops and asks before doing anything.

## Limits

These files are instructions, not enforcement. They do not install hooks or control what your AI provider, build tools, or backup and sync services do with your files. Review them before you adopt them.

## License

See the license of each skill source. The template files are provided as-is.
