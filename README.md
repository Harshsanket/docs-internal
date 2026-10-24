# docs-internal

Local-only guidance for AI coding agents working in a Git project. It organizes agent instructions, selected skills, custom instructions, and development records while keeping those materials separate from the application's version-controlled code.

This is a Markdown instruction template, not a Git plugin, installer, background service, or automatic security barrier. The agent must load and follow the rules through its supported configuration mechanism.

## What it does

The configuration starts with setup before implementation. It asks how skills should be selected, preserves user choices, and keeps internal work in a predictable folder. During development, it requires focused changes, evidence-based decisions, testing, and accurate progress records.

For Git, the rules require exclusion and tracking checks before commits or publication. They separate permission to edit, permission to commit, and permission to push. A request to change code does not automatically authorize publishing it.

This root README is an overview, not a replacement for the operating rules. Creating it does not authorize a commit or push. The detailed local policy remains in `docs-internal/AGENT.md`.

## Folder layout

```text
<project-root>/
|-- README.md                    # This overview
|-- .gitignore                   # Existing rules plus approved exclusions
|-- AGENTS.md                    # Local-only agent entrypoint
`-- docs-internal/               # Entire directory is local-only
    |-- README.md                # Internal file index and usage guide
    |-- AGENT.md                 # Setup, workflow, permissions, Git safeguards
    |-- CODING-PRINCIPLES.md      # Implementation and validation rules
    |-- INSTRUCTIONS.md          # Communication, evidence, and judgment
    |-- CUSTOM-INSTRUCTION      # Created only for supplied custom instructions
    |-- skills/                  # Selected and reviewed skill bundles
    `-- docs/
        |-- setup.md             # Confirmed choices and skill provenance
        |-- project-map.md       # Verified project structure and data flows
        |-- findings.md          # Evidence, questions, and risks
        |-- roadmap.md           # Planned, active, completed, and blocked work
        |-- decisions.md         # Append-only decision log
        `-- progress.md          # Append-only activity and validation log
```

The directory name is `docs-internal/`, without a leading dot. Internal skills belong in `docs-internal/skills/`; internal documentation belongs in `docs-internal/docs/`. Existing public project documentation is not moved or hidden.

## Setup and skill selection

On first use, the agent asks the user to select a mode. There is no default selection. It also confirms any unresolved project location, asks for optional custom instructions, and requests permission for narrowly scoped setup changes. A valid saved setup is reused rather than repeated.

| Mode | Behavior |
| --- | --- |
| Auto | Select the smallest useful set from verified codebase and current-task evidence. Reassess as work changes. Ask whenever a selection is unclear. |
| Guided | Propose a shortlist and wait for approval before adding or activating skills. |
| Manual | Use only skills explicitly selected by the user. |
| Off | Do not fetch, add, update, or activate optional external project skills. Preserve previously saved files. |

Candidate sources are `addyosmani/agent-skills`, `poteto/noodle`, and `mattpocock/skills`. A source is not an automatic trust or installation approval. Skills are reviewed before use; selecting a skill does not authorize running its scripts, installing a runtime, or changing global settings.

User-supplied instructions are saved in the extensionless file `docs-internal/CUSTOM-INSTRUCTION`. No placeholder is created when none are supplied. These instructions do not override the local-only safeguards or higher-priority host requirements.

## What it does for Git

### Keeps agent material local

The policy protects the root `AGENTS.md` and everything inside `docs-internal/`, including future files, downloaded skills, custom instructions, and internal records.

Agents must not stage, commit, push, upload, or include protected content in pull requests, shared patches, releases, deployment bundles, or shared archives. Renaming or copying the content does not make it public. General permission to push application code does not include permission to publish these materials.

### Requires ignore rules and separate tracking checks

After setup-write approval, merge these entries into the project-root `.gitignore`. Preserve existing rules; do not replace the file.

```gitignore
/AGENTS.md
/docs-internal/
```

Git ignore rules apply to untracked files. They do not remove files that are already tracked. Effective exclusions must be checked because other patterns can change the result. [G1]

The following are manual inspection commands, not an automatic pass/fail gate. Run them individually from the confirmed project root. A failed or unavailable check is a blocker, not a successful result.

**Check the index:**

```sh
git ls-files -- AGENTS.md docs-internal
```

A successful command must produce no paths. Any output means protected paths are in the index; stop the affected Git operation and request an approved recovery plan. [G2]

**Inspect the effective ignore rules:**

```sh
git check-ignore -v -- AGENTS.md docs-internal/ docs-internal/docs/progress.md docs-internal/skills/.protection-check docs-internal/CUSTOM-INSTRUCTION
```

Confirm an excluding rule for every listed path and check actual existing protected files too. A rule beginning with `!` is a negation, not proof of exclusion. A successful overall exit status does not prove that every path is protected. Tracked files are normally omitted, which is why the index check is separate. The `.protection-check` name is only a probe; it does not need to be created. [G3]

**Review staged changes:**

```sh
git diff --cached --name-status
```

This shows staged paths and change types, not the full contents. Review the staged content locally as well, including copied private text in otherwise public files. Do not paste private diffs into external tools. [G4]

These checks are a starting point. The complete workflow and read-only baseline guard are in `docs-internal/AGENT.md`.

### Stops unsafe publication

Before an authorized commit or publication, the agent must inspect protected paths, staged content, and actual package or deployment inputs. Before a push, it must also verify the intended remote and references and inspect the full outgoing history, not just the latest working tree.

If protected material is already tracked, staged, or previously exposed, the affected operation stops. The agent must preserve local files and ask for a specific recovery plan. It must not automatically untrack files, discard staged work, rewrite history, or force-push.

A push or other upload requires explicit approval for that operation or a clearly defined workflow that includes it. Permission to edit or commit is not permission to push.

## Limits: instructions are not enforcement

The template does not install hooks, modify Git automatically, execute checks on its own, or guarantee that every agent follows its instructions. Approved hooks can add safeguards, but they are not included or installed by this bundle.

Git exclusions do not govern every archive, build tool, backup, cloud-sync service, or AI provider. Those paths need separate review. A clean index does not prove that earlier commits or remote copies are free of protected material. Never store secrets in internal records merely because they are local-only.

This README does not grant permission to publish the private configuration or a configured archive. Keep the downloaded bundle outside the application repository while reviewing it; do not add the bundle itself to Git.

## Safe adoption

Review the template before applying it. Preserve an existing project README, `AGENTS.md`, `.gitignore`, and internal records. Do not blindly extract the archive over an existing project or replace its application documentation with this overview.

Use the agent host's supported instruction-loading mechanism to load the entrypoint and complete setup. Establish the approved Git protections before writing project-specific internal records or adding skills. Confirm which files were actually loaded; merely creating a directory does not prove that a host uses it.

This bundle contains templates, not an installed skill collection or a verified live-project configuration. The internal README describes the files; `AGENT.md` owns the detailed workflow and safeguards. This overview adds no new permissions or policy exceptions.

## Git references

These official references describe the Git commands above; they do not replace the project's stricter local-only policy.

- [G1] Git ignore patterns and tracked-file limitations: `https://git-scm.com/docs/gitignore`
- [G2] Git index inspection: `https://git-scm.com/docs/git-ls-files`
- [G3] Effective ignore rules, negations, and exit status: `https://git-scm.com/docs/git-check-ignore`
- [G4] Staged differences and name/status output: `https://git-scm.com/docs/git-diff`
