# Changelog

All notable changes to Aptus CSS are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project follows the version recorded in `src/VERSION`.

This changelog starts tracking changes from `2.1.3` onward. Changes prior to that version were not recorded here.

## [Unreleased]

## [2.6.0] - 2026-07-14

### Removed

- Message bar close button (`.msg-bar-close-button`, `.msg-close-icon`): removed from the component as messages auto-dismiss and the button had poor UX on mobile, taking up valuable screen space.

### Changed

- Message bar text (`.msg-bar-text`): simplified layout from `inline-block` with margins to `display: block` with padding for cleaner, more predictable rendering.

## [2.5.0] - 2026-07-14

### Changed

- Reset stylesheet (`reset.css`): improved accessibility by replacing blanket `outline: none` with `focus-visible` states that show a 2px outline with `currentColor` and 2px offset, visible on links and form elements.
- Reset stylesheet: removed `height: 100%` from `body` to prevent unexpected scrolling behavior.
- Reset stylesheet: removed `background: none` from form elements, allowing default browser backgrounds while maintaining `border: none` for styling flexibility.

### Added

- Reset stylesheet: `font-size: 16px` on `html` for consistent `rem` calculations across consuming projects.
- Reset stylesheet: styles for previously unstyled elements — `fieldset` (margin, padding, border reset), `hr` (modern border-based style with `currentColor`), `code` and `pre` (monospace font-family), `small` (0.875em sizing).

## [2.4.0] - 2026-07-14

### Changed

- GDPR banner (`gdpr.css`): responsive layout improved; `display: inline-block` changed to `display: block` with `margin: 0 auto` for proper centering and width handling.
- GDPR banner breakpoint aligned with project standard: `max-width: 1048px` removed and replaced with single mobile breakpoint at `max-width: 767.98px` (matching other responsive utilities).
- GDPR banner: `border-radius: 8px 8px 8px 8px` simplified to `border-radius: 8px`.
- GDPR banner: `z-index` lowered from `9991` to `1000` (standard for fixed overlays).
- GDPR banner: `!important` removed from media query (unnecessary due to CSS cascade specificity).

### Added

- GDPR banner color customization via CSS variables: `--gdpr-bg`, `--gdpr-border`, `--gdpr-text`, `--gdpr-button-bg`, `--gdpr-button-border`, `--gdpr-button-text`, `--gdpr-button-bg-hover`, `--gdpr-button-text-hover`, all with sensible fallbacks.
- `docs/examples/gdpr.html`: complete reference and interactive test page for the GDPR banner component, including responsive behavior demonstration and JavaScript integration example.

## [2.3.0] - 2026-07-14

### Changed

- Responsive breakpoint for grid and responsive utilities standardized to `min-width: 768px` (previously 800px), aligning with industry standard breakpoints and eliminating the intermediate breakpoint gap. Mobile utilities remain at `max-width: 767.98px`.

## [2.2.0] - 2026-07-14

### Added

- New spacing utilities: `.top60`, `.bottom60`, `.left40`–`.left60`, `.right40`–`.right60` for direct margin utilities; expanded `.pad*` scale to 10–100px (increments of 10); expanded responsive padding (`.res-pad-*`) to 10–100px; expanded responsive margin (`.res-margin-*`) to include 60px variant.
- New flexbox utility classes: `.flex-row`, `.flex-col`, `.flex-wrap`, `.flex-nowrap`, `.justify-{start,center,end,between,around}`, `.align-{start,center,end,stretch}`.
- New text utilities: `.text-truncate` (single-line ellipsis), `.text-clamp-1` through `.text-clamp-5` (multi-line clamping with `-webkit-line-clamp` and standard `line-clamp`).
- New aspect ratio utilities: `.aspect-ratio-1x1`, `.aspect-ratio-16x9`, `.aspect-ratio-4x3`, `.aspect-ratio-21x9`, `.aspect-ratio-3x2`.
- Moved `.status-active`, `.status-inactive` from `commons.css` to `ui.css` as `.ui-status-active`, `.ui-status-inactive` (old class names retained as aliases in `ui.css` for compatibility).
- Moved `.def-list` and `.simple-list` from `commons.css` to `ui.css`.
- `docs/conventions.md`: documented three coexisting spacing utility families (direct scale, semantic abbreviations, responsive) and updated `!important` guidance to include `.top*` and `.bottom*` utilities.

### Fixed

- `.status-inactive` now uses `--color-gray` instead of incorrectly referencing `--color-green`; fallback changed to `#595959`.
- `.invisible` no longer contains redundant `visibility: hidden;` declaration.
- `.simple-list` padding corrected: changed from `padding-left: 1.2em` to `padding-left: 0` (list has no bullets).
- Renamed `.res-top-margin-*` → `.res-margin-top-*` for consistency with `.res-margin-left-*` and `.res-margin-right-*` naming.
- All `.top*` and `.bottom*` margin utilities now include `!important` for consistency and clarity of intent.

### Changed

- Applied `!important` to all `.top*` and `.bottom*` margin utilities (previously inconsistent).

## [2.1.3] - 2026-07-14

### Added

- Project documentation: `README.md`, `CLAUDE.md`, `AGENTS.md`, `docs/requirements.md`, `docs/conventions.md`, and `docs/usage.md`.
- `LICENSE` file (MIT).
- This `CHANGELOG.md` file.
