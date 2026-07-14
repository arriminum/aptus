# CLAUDE.md

This file guides Claude Code in this repository. The full rules for working on Aptus CSS — what to read first, which files are editable, build and validation commands, scope, naming, and compatibility rules — live in [AGENTS.md](AGENTS.md). Read it before making any change here; this file only adds Claude Code-specific notes on top of it.

## Markdown formatting

Do not hard-wrap Markdown paragraphs. Keep each paragraph on a single line unless there is an explicit semantic reason to add a line break, such as a list item, code block, table, heading, or intentionally separated paragraph.

## Versioning & changelog (mandatory)

- `src/VERSION` is the single source of truth.
- Every meaningful change (page, component, CSS behavior, docs, reusable pattern) gets an entry in `CHANGELOG.md`.
- Bump `src/VERSION` when a change affects structure, public pages, components, build, deploy, behavior, or docs. The version in `CHANGELOG.md` must match `src/VERSION`.
- Do not bump the version for minimal changes.

## When you finish a task

Summarize: what changed, which files changed, whether `CHANGELOG.md` and `src/VERSION` were updated, and any follow-up needed.
