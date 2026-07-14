# Conventions

This document explains how to work inside Aptus CSS: what belongs in the library, how to name and structure classes, and how to keep changes safe for the projects that already consume it. Read this before adding, renaming, or removing anything public.

## Before making a change

- Consult [docs/usage.md](usage.md) and [docs/examples/](examples/) first. Do not assume a class does not exist just because it does not appear in the examples; check the actual `src/*.css` files.
- Understand the existing structure before creating new files or a new module. A new module is only justified when no existing one is a reasonable home for the change.
- Do not create a second grid system. `.g-row` and `.col1`–`.col12` (see [src/grid.css](../src/grid.css)) are the only grid; extend it instead of building a parallel one.
- Do not duplicate an existing class under a new name. Search `src/` for equivalent behavior before adding something new.

## What belongs in Aptus

A class or component belongs in Aptus when it is genuinely reusable across projects: reset rules, grid, page structure, spacing, alignment, typography basics, responsive images, form patterns, common UI elements (message bars, status badges, spinners, lists), and small utility classes for frequent behaviors.

A feature should be promoted from a single project into Aptus once it has proven to be generic and reusable, not before.

## What does not belong in Aptus

Do not add directly to the library:

- Client-specific brand colors or visual identity.
- Styles used by a single page.
- Components used by only one project.
- WordPress- or plugin-specific rules.
- Selectors tightly coupled to one project's particular HTML structure.
- Improvised fixes without an explanation.
- Classes that duplicate existing functionality.
- Global rules with a high risk of affecting unrelated elements.
- Hard dependencies on an external CSS framework.
- JavaScript behavior that belongs to another library.

Page- or project-specific classes stay in the consuming project's own CSS, with a prefix specific to that context, for example `.course-hero`, `.contact-form`, `.product-gallery`. They must not be added to Aptus just because they appear in one site.

## Naming conventions

Class names should be:

- Clear and short without being cryptic.
- Consistent with the naming already used in the module.
- Reusable, not tied to a specific project.

Avoid names that are too generic to be safe as global, load-bearing CSS, since they are prone to colliding with a consuming project's own styles, plugins, or third-party CSS: `.card`, `.box`, `.wrapper`, `.media`, `.content`. When a generic-sounding class is genuinely needed, prefer a more specific name or a coherent prefix consistent with the module it lives in (`ui-`, `msg-`, `gdpr-`, `res-`, `mob-`, `el-`).

## Code style

- Indent with 2 spaces. Do not use tabs.
- Keep class names short, without becoming cryptic (see [Naming conventions](#naming-conventions) above).
- Every comment must be written in English, regardless of the language used elsewhere in the project or in commit messages.
- Head each block of related classes with a short, uppercase comment naming the group, in the form `/* GROUP_NAME ----- */`. For example:

  ```css
  /* INPUT ----- */

  .noselect {
    -webkit-user-select: none;
    -ms-user-select: none;
    user-select: none;
  }


  /* POSITION ----- */

  .fixed {
    position: fixed;
  }
  .absolute {
    position: absolute;
  }
  ```

- Separate each block/group of classes from the next with 3 blank lines, as shown above.

## Utility classes and `!important`

Aptus does not generate one class per CSS property. Utilities exist for specific, frequently repeated behaviors (visibility, spacing, alignment, responsive width), not as a general-purpose atomic CSS system.

`!important` is reserved for utilities whose explicit purpose is to override an element's normal styling, such as `.full-width`, `.mob-hidden`, `.mob-full-width`, `.top*`, and `.bottom*`. Do not add `!important` to a class that is not meant to act as a forceful override.

## Spacing utilities

Spacing utilities in `src/commons.css` exist in three naming families for historical reasons — all are valid and coexist:

- **Direct scale** (`.left10`, `.pad20`): names that directly indicate pixels; simple, short form.
- **Semantic abbreviations** (`.mx-auto`, `.w-100`, `.h-auto`): Bootstrap-style descriptive names for common patterns.
- **Responsive** (`.res-pad-left10`, `.res-margin-top-20`): conditional values at mobile vs. desktop breakpoints, prefixed with `res-`.

Do not create a fourth family. When adding spacing utilities, extend one of the existing families to match its pattern.

## Responsiveness

Components and utilities must work across common screen widths. The mobile-oriented utility classes in `src/commons.css` (`.mob-hidden`, `.mob-full-width`) use:

```css
@media (max-width: 767.98px) {
  /* mobile rules */
}
```

The grid's desktop column widths in `src/grid.css` activate above `min-width: 768px`. Do not introduce additional breakpoints without a strong technical reason; keep responsive utilities aligned with these two breakpoints.

## Compatibility and changes to existing classes

Before changing a class that already exists, verify:

1. Where it is used, in this repository's examples and, as far as can be known, in consuming projects.
2. Whether the change alters its public behavior (output, layout, visual result).
3. Whether older consuming projects could be affected.
4. Whether a compatible alternative exists (a new class or modifier instead of changing the existing one).
5. Whether the change needs a `CHANGELOG.md` entry.
6. Whether documentation and examples need updating.

Do not rename or remove a public class without considering a migration path. When practical, keep the old class working as an alias during a transition instead of breaking it outright.

Do not assume a class is unused just because it does not appear in `docs/examples/`; the examples are illustrative, not an exhaustive usage census.

## Versioning and changelog

- `src/VERSION` is the single source of truth for the current version.
- Every meaningful change (a page, a component, CSS behavior, documentation, or a newly reusable pattern) gets an entry in `CHANGELOG.md`.
- Bump `src/VERSION` when a change affects structure, public classes, components, build, deploy, behavior, or documentation. The version recorded in `CHANGELOG.md` must match `src/VERSION`.
- Do not bump the version for minor, non-meaningful changes.

## Build and generated files

- Edit only files under `src/`. Never edit files under `dist/` by hand; they are generated by `rpack build` / `rimi build`.
- Run the build (`rpack build` or `rimi build`) after any change in `src/` before considering the change complete. See [requirements.md](requirements.md) for the exact commands.

## Scope of changes

- Keep each change small, objective, and traceable to a clear reason.
- Do not perform broad refactors without a concrete need; a bug fix does not require surrounding cleanup.
- When a change is incompatible with existing usage, explain why in the commit and in `CHANGELOG.md`.
- Update `README.md` or `docs/usage.md` whenever public usage changes, and update `docs/examples/` whenever public behavior changes.

## Testing checklist

At minimum, verify changes:

- On desktop and mobile widths.
- Inside and outside the grid.
- On forms, long text, and small and large images.
- On both flex and block layout contexts.
- Against the relevant page(s) in `docs/examples/`.
- In a Chromium-based browser, and in Firefox when possible.

Pay particular attention to: horizontal overflow, broken grid rows, excessive selector specificity, unexpectedly global rules, conflicts between modules, unintended spacing changes, and regressions at the mobile breakpoint.
