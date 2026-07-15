# Versioning

Aptus CSS uses **Semantic Versioning** ([semver.org](https://semver.org)) to signal the impact of each release to consuming projects.

## Version format

Versions follow `MAJOR.MINOR.PATCH`:

- `MAJOR` — breaking changes that require updates in consuming projects.
- `MINOR` — new features or non-breaking improvements, backward-compatible.
- `PATCH` — bug fixes, small corrections, internal improvements.

Current version: see [src/VERSION](../src/VERSION)

## When to bump

A **bump** is an intentional increment to the version number, decided and requested by the project owner. Bumps are not automatic — they happen only when explicitly chosen.

### PATCH bump (e.g., 2.5.0 → 2.5.1)

Increment `PATCH` for:

- Bug fixes (broken styles, incorrect calculations, cross-browser issues).
- Corrections to existing classes that do not change their intended behavior or output.
- Documentation fixes and example corrections.
- Internal refactoring with zero behavioral change.

**No breaking changes. Consuming projects can upgrade safely without any code changes.**

### MINOR bump (e.g., 2.5.0 → 2.6.0)

Increment `MINOR` for:

- New classes or components (grid columns, utilities, UI patterns).
- New features added to existing classes (new CSS variables, responsive variants).
- Enhanced documentation.
- Additions to the public API that do not alter existing behavior.

**Backward-compatible. Consuming projects can upgrade without changes, though they may benefit from new features.**

### MAJOR bump (e.g., 2.5.0 → 3.0.0)

Increment `MAJOR` for:

- Removing or renaming an existing public class.
- Changing the behavior or output of an existing class in a way that breaks consuming projects.
- Restructuring modules or changing public naming conventions.
- Removing or altering default styles in a way that visibly changes output.

**Breaking changes. Consuming projects must review and update their CSS or HTML to remain compatible.**

## How to request a bump

1. **Finish the work.** Complete all CSS changes, documentation, and testing.
2. **Ask for a bump.** Tell the maintainer which type (patch, minor, or major) and why.
3. **Maintainer updates version and changelog.** The version is incremented in `src/VERSION`, and the changes are recorded in `CHANGELOG.md` under the new version header with an ISO date.
4. **Build and deploy.** The build is run and the release is deployed to the library path.

## Changelog

Every bump must be accompanied by an entry in [CHANGELOG.md](../CHANGELOG.md), following the [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) format.

Changes are grouped under:
- `Added` — new classes, components, features.
- `Changed` — modifications to existing behavior or structure.
- `Fixed` — bug fixes and corrections.
- `Removed` — deletion of public classes (usually only for MAJOR bumps).

Date format in changelog entries is ISO 8601 (YYYY-MM-DD).

### Tagging each entry with its impact

Every entry added under `[Unreleased]` must end with an explicit impact tag — `(patch)`, `(minor)`, or `(major)` — decided at the time the change is made, using the rules above. This is mandatory even though the bump itself is requested later by the maintainer ([see "How to request a bump"](#how-to-request-a-bump)): tagging at the time of the change captures the reasoning while it is fresh, so nobody has to re-derive it from the diff when the bump is finally requested. When the maintainer asks for a bump, the highest tag among the accumulated `[Unreleased]` entries determines the bump type for the whole batch.

## Rationale

Aptus is a shared library consumed by multiple external projects that are not in this repository. A "no usages found here" search is not proof that a change is safe — projects outside this repo depend on current behavior.

Explicit version bumps give those projects a clear signal:
- **PATCH**: safe to upgrade, likely a fix.
- **MINOR**: safe to upgrade, new optional features.
- **MAJOR**: requires review and possible code changes before upgrading.

See [AGENTS.md](../AGENTS.md) and [docs/conventions.md](conventions.md) for more on compatibility and scope.
