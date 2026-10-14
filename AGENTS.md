# AGENTS.md

This file is the repository-level Codex adapter. Shared project knowledge
belongs in `docs/`; this file should point to that knowledge rather than
duplicate it.

## Sources of truth

Use the documentation relevant to the task:

- Architecture: `docs/architecture.md`
- Product requirements: `docs/requirements/lastenheft-v1.0.md`
- Conventions: `docs/conventions.md`
- Testing and validation: `docs/testing.md`
- AI-assisted development: `docs/ai-usage.md`
- Architecture decisions: `docs/decisions/`

Treat those documents as authoritative for their respective concerns.

The product requirements document defines the intended product scope
and acceptance criteria. Always check its approval status before
using it as an implementation baseline.

Draft requirements may be analyzed and reviewed, but must not be
treated as approved authorization for implementation.

Do not independently approve requirements, change the approved scope,
or weaken security and quality gates. Escalate material conflicts or
missing approvals to the Product Owner.

## Working principles

- Understand the relevant context before making significant changes.
- Follow the documented architecture and project conventions.
- Keep changes focused and prefer existing patterns.
- Preserve existing behavior unless the task explicitly changes it.
- State important assumptions when information is incomplete.
- Update authoritative documentation when behavior, interfaces, architecture,
  or workflows change.

## Scope and change discipline

Do not perform unrelated refactoring, formatting, dependency changes, file
moves, API changes, configuration changes, or architectural changes.

Before editing, identify the affected components, relevant documentation,
tests, compatibility impact, and risks. Make the smallest coherent change
that satisfies the task.

Do not create, modify, or delete external data, credentials, infrastructure,
or production systems merely because a tool is available. Read and write
operations require separate authorization. Prefer read-only or reversible
approaches for external systems.

Never expose or commit passwords, API keys, access tokens, private keys,
cookies, confidential connection strings, or other secrets.

## Testing and validation

Follow `docs/testing.md`. Choose validation appropriate to the scope and
risk of the change.

Do not claim that a test, build, command, integration, or defect fix
succeeded unless the relevant validation was actually executed and its
result is known. Report unexecuted validation, remaining uncertainty, and
environment failures separately from implementation failures.

When something fails, inspect the cause before changing behavior. Do not
weaken valid tests, suppress errors, or apply speculative fixes repeatedly.

## Uncertainty and risky changes

Distinguish verified facts, documented decisions, assumptions, and unknowns.
Surface material uncertainty before irreversible or high-impact changes.

For destructive, irreversible, security-sensitive, production-affecting, or
externally visible operations: identify the impact, verify prerequisites,
confirm authorization, and prefer a dry run or reversible alternative.

## Codex-specific extensions

Codex-specific configuration belongs in `.codex/`.

- `.codex/config.toml` contains project-level Codex configuration.
- `.codex/hooks.json` is reserved for explicitly configured lifecycle hooks.
- `.codex/agents/` contains neutral TOML templates and concrete custom-agent
  files. Register a concrete role in `.codex/config.toml` under
  `[agents.<name>]` and point `config_file` to the file under `agents/`.
- Repository skills belong in `.agents/skills/<skill-name>/SKILL.md`.
  Use a skill for a focused, reusable workflow; keep shared project
  knowledge in `docs/`.

The `.example` suffix is used for Claude Code examples that must be copied
or renamed to their expected active filename before discovery. Do not treat
an example as an active project capability.

## Completion reporting

When reporting work, distinguish:

- Changed: what was modified.
- Validated: what was actually checked.
- Not validated: what could not be checked and why.
- Remaining issues: known risks, limitations, or follow-up work.

Do not imply greater confidence than the evidence supports.
