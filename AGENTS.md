# AGENTS.md

Guidance for AI agents and automated contributors working in the Aptus CSS repository. Aptus is a shared, reusable CSS library consumed by multiple external projects; treat every public class as an API. Prefer fixing or extending an existing rule over creating a parallel one.

## Read first, by task type

- **Adding or changing a CSS class or component**: read [docs/conventions.md](docs/conventions.md), then [docs/usage.md](docs/usage.md) and [docs/examples/](docs/examples/) to check whether an equivalent already exists.
- **Changing the grid, spacing, or breakpoints**: read [docs/conventions.md](docs/conventions.md) (responsiveness section) before touching `src/grid.css` or the responsive utilities in `src/commons.css`.
- **Build, distribution, or deploy questions**: read [docs/requirements.md](docs/requirements.md).
- **Writing or updating documentation**: read [README.md](README.md) to keep it in sync with `docs/`.

## Files you may edit

- `src/*.css` — the actual library source.
- `src/VERSION`, `src/APP_NAME` — version and project name, when a change requires bumping the version.
- `docs/*.md`, `docs/examples/*.html`, `README.md`, `CHANGELOG.md`, `AGENTS.md`, `CLAUDE.md`.
- `rpack.json`, `rimi.json` — only when the build/module configuration itself must change (for example, a new module is added).

## Files that are generated — never edit by hand

- Everything under `dist/`, including `dist/*.min.css`, `dist/VERSION`, `dist/APP_NAME`. These are produced by `rpack build` / `rimi build`. Edit the matching `src/` file and rebuild instead.

## Build

```bash
rpack build     # minify src/*.css into dist/*.min.css
rimi build      # copy VERSION/APP_NAME, then run rpack build
rimi deploy     # build and install into the local CSS lib path
```

Run the build after any change under `src/`. Full details, including which tool produces which file, are in [docs/requirements.md](docs/requirements.md).

## Validating a change

There is no automated test suite or linter in this repository. Validate manually:

- Open the relevant page in `docs/examples/` (or add a section to it) and check the change in a browser.
- Check both desktop and mobile widths, and the intermediate range between the grid breakpoint (`min-width: 800px`) and the mobile-utility breakpoint (`max-width: 767.98px`).
- Check the change inside and outside `.g-row`/`.col*`, and against long text and small/large images where relevant.
- Watch for: horizontal overflow, broken grid rows, unexpectedly high specificity, rules that leak beyond their intended scope, and conflicts between modules.

## Creating a new class

1. Confirm it does not already exist or nearly exist ([docs/usage.md](docs/usage.md), `src/*.css`).
2. Confirm it is genuinely reusable across projects, not specific to one client or page (see "Scope" below).
3. Name it consistently with the module it belongs to (see naming rules in [docs/conventions.md](docs/conventions.md)).
4. Add it to the appropriate `src/*.css` module; do not start a new module unless no existing one fits.
5. Add or extend an example in `docs/examples/`, and document it in `docs/usage.md`.

## Scope: what belongs in Aptus, and what does not

Aptus holds reset, grid, structure, spacing, typography basics, responsive images, form patterns, and genuinely common UI components and utilities. It must never accumulate client-specific colors or branding, single-page or single-project styles, WordPress/plugin-specific rules, selectors coupled to one project's HTML, or a hard dependency on another CSS framework. The full rationale and examples are in [docs/conventions.md](docs/conventions.md) — read it before deciding either way.

## Compatibility

Aptus is consumed by multiple external projects that are not in this repository, so a "no usages found here" search is not proof a class is unused. Before renaming or removing a public class: check where it is used in `docs/examples/`, assess whether the change alters public behavior, prefer an additive/compatible alternative when one exists, and consider keeping the old class as a temporary alias. Never make a breaking change silently — it must be documented in `CHANGELOG.md` and explained.

## Markdown formatting

Do not hard-wrap Markdown paragraphs. Keep each paragraph on a single line unless there is an explicit semantic reason to add a line break, such as a list item, code block, table, heading, or intentionally separated paragraph.

## Versioning & changelog (mandatory)

- `src/VERSION` is the single source of truth.
- Every meaningful change (page, component, CSS behavior, docs, reusable pattern) gets an entry in `CHANGELOG.md`.
- Bumping `src/VERSION` is manual and requires an explicit request from the user in the conversation. An agent must never bump the version on its own initiative, even for a change that "affects structure, public classes, components, build, deploy, behavior, or docs."
- When a change would warrant a version bump under the criteria above but the user has not asked for one, add the `CHANGELOG.md` entry under an `Unreleased` heading (not tied to a version number) and note in your summary that a bump is pending user approval.
- Tag every `Unreleased` entry with `(patch)`, `(minor)`, or `(major)` at the time you write it, per the rules in [docs/versioning.md](docs/versioning.md). Decide this while the change is fresh in context — do not leave it untagged for a future bump request to re-derive from the diff.
- Once the user asks for a bump, move the `Unreleased` entries under the new version heading (the bump type is the highest tag among them) and update `src/VERSION` to match.

## What to update alongside a change

- `CHANGELOG.md` and `src/VERSION`, per the rules above.
- `docs/usage.md` and/or `README.md`, whenever public usage changes.
- `docs/examples/*.html`, whenever public behavior changes.
- `docs/conventions.md`, only when a convention itself changes, not for every class added.

## Never do without prior analysis

- Never edit files under `dist/`.
- Never remove or rename a public class without checking impact and considering a migration path.
- Never introduce a second grid system or duplicate an existing utility.
- Never add a framework dependency (Bootstrap, Tailwind, or similar).
- Never add client-specific or page-specific styles directly to `src/`.
- Never bypass the build after changing `src/` — always run `rpack build` / `rimi build` before considering a CSS change complete.

## When you finish a task

Summarize: what changed, which files changed, whether `CHANGELOG.md` and `src/VERSION` were updated, and any follow-up needed.
