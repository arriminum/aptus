# CLAUDE.md

This file guides Claude Code in this repository. The full rules for working on Aptus CSS — what to read first, which files are editable, build and validation commands, scope, naming, and compatibility rules — live in [AGENTS.md](AGENTS.md). Read it before making any change here; this file only adds Claude Code-specific notes on top of it.

## Markdown formatting

Do not hard-wrap Markdown paragraphs. Keep each paragraph on a single line unless there is an explicit semantic reason to add a line break, such as a list item, code block, table, heading, or intentionally separated paragraph.

## Versioning & changelog (mandatory)

See the "Versioning & changelog" section in [AGENTS.md](AGENTS.md) — in short: bumping `src/VERSION` is manual and only happens when the user explicitly asks for it in the conversation, never on an agent's own initiative. Until then, log pending changes in `CHANGELOG.md` under `Unreleased`.

## When you finish a task

Summarize: what changed, which files changed, whether `CHANGELOG.md` and `src/VERSION` were updated, and any follow-up needed.
