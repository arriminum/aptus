# Changelog

All notable changes to Aptus CSS are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project follows the version recorded in `src/VERSION`.

This changelog starts tracking changes from `2.1.3` onward. Changes prior to that version were not recorded here.

## Unreleased

## [3.0.1] - 2026-07-22

### Fixed

- `datalist.css`: render `--datalist-table-border` separators on body cells so borders between rows remain visible when the table uses the separate border model. (patch)

## [3.0.0] - 2026-07-19

### Added

- New module `breadcrumb.css` with a responsive `.breadcrumb` component that shows the last two items on mobile and the full trail from `768px` upward. (minor)
- New module `eyebrow.css` with `.eyebrow` and `.eyebrow-mark` for compact section labels with an optional decorative mark. (minor)
- `commons.css`: `.res-center-aligned` for centering text only at mobile widths (`max-width: 767.98px`). (minor)
- `image.css`: `.elevated-shadow` for a stronger, more elevated drop shadow. (minor)
- `image.css`: `.contained-shadow` for a tighter, closer drop shadow. (minor)
- `image.css`: `.framed-shadow` for a subtle border combined with a light shadow. (minor)
- `docs/examples/image.html`: added examples for `.elevated-shadow`, `.contained-shadow`, and `.framed-shadow`. (minor)
- Runnable examples and usage documentation for the breadcrumb and eyebrow modules. (minor)

### Changed

- `image.css`: redesigned `.subtle-shadow`, `.light-shadow`, and `.base-shadow` with a new layered shadow scale, visibly changing their existing rendering. (major)
- `grid.css`: `.g-row.gutter` now only spaces columns from each other, leaving the first column's left edge and the last column's right edge flush with the surrounding container. The row's negative side margins were removed (no longer needed since the edge columns have no outer padding to compensate for), which also prevents gutter rows from overflowing their container. (patch)
- `rpack.json`: added `breadcrumb.css` and `eyebrow.css` to the generated module list. (minor)

## [2.8.0] - 2026-07-15

### Added

- New module `datalist.css` for tables of data fetched from a service: `.datalist-table`, `.datalist-row-alt`, `.datalist-no-hover`, `.datalist-empty`, `.datalist-action-link`, `.datalist-summary`, `.datalist-pager`, `.datalist-pager-current`. Colors, font size/weight, and header corner rounding are customizable via `--datalist-*` CSS variables with fallbacks, including `--datalist-font-size`, `--datalist-font-weight`, `--datalist-action-font-weight`, and `--datalist-head-radius`. (minor)
- `docs/examples/datalist.html`, runnable examples covering the basic table, hover states, row actions, empty state, and the summary/pager footer. (minor)
- `grid.css`: `.g-row.gutter`, adding horizontal spacing between a row's columns instead of having them sit flush against each other. (minor)
- `grid.css`: `.col-offset1`–`.col-offset11`, pushing a column right by that many columns of empty space without needing a placeholder column. (minor)
- `docs/examples/grid.html`, runnable examples of the grid covering equal/unequal columns, gutters, offsets, and flex alignment. (minor)
- `image.css`: `.subtle-shadow` for a lighter drop shadow than `.light-shadow`. (minor)
- `image.css`: `.base-shadow` for a drop shadow offset toward the bottom, giving images a "resting on a surface" effect. (minor)
- `image.css`: `.rounded-img` and `.circle-img` for rounded and fully circular images. (minor)
- `image.css`: `.img-cover` and `.img-contain`, `object-fit` helpers meant to pair with `.aspect-ratio-*` (from `ui.css`) or other fixed-size containers. (minor)
- `image.css`: `.img-grayscale`, a grayscale-by-default filter that reveals full color on hover. (minor)
- `image.css`: `.img-zoom-wrap`, a wrapper that clips and smoothly zooms its child image on hover. (minor)
- `image.css`: `.img-caption-wrap` / `.img-caption`, for overlaying a caption with a dark gradient at the bottom of an image. (minor)

### Removed

- Polaroid image utilities (`.pol-img`, `.pol-shadow`) removed from `image.css`; they were an old, unused visual style and duplicated the shadow utilities. (major)
- `.four-col` removed from `grid.css`; it was a broken leftover (the same selector repeated four times with an undocumented `min-width: 1096px` breakpoint) with no confirmed usage in any consuming project. (major)

### Changed

- `image.css`: `.def-shadow` renamed to `.light-shadow` (previous `.light-shadow` values are gone; the old lighter shadow is now `.subtle-shadow`). Consuming projects using `.def-shadow` must switch to `.light-shadow`. (major)
- Module file renamed from `src/message-bar.css` to `src/notification.css` (distribution file: `dist/notification.min.css`) to better reflect its content: message bar, form error box, overlay, and toast notifications. (major)
- Message bar (`.msg-bar-info`, `.msg-bar-error`): added CSS variables for color customization (`--color-text-inverse`, `--color-success`, `--color-error`) with sensible fallbacks for better theming flexibility. (minor)
- Message bar: added `box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15)` to improve visual hierarchy and separation from page content. (minor)
- Message bar: mobile breakpoint aligned with project standard, changed from `max-width: 600px` to `max-width: 767.98px` (matching `.mob-hidden` and other responsive utilities). (patch)
- Form error icon (`.form-error-icon`): mask image URL changed from an absolute path (`/res/img/aptus/form-error.svg`) to a path relative to the CSS file (`../img/aptus/form-error.svg`), so apps installed under a subdirectory of the web root resolve the icon correctly with no extra configuration. This assumes the standard `res/{css,img,js}` sibling layout documented in `docs/requirements.md`; if a consuming project serves `dist/notification.min.css` from a location where `../img/aptus/` does not resolve to the actual image directory, the icon will fail to load silently (the form error text still renders). (patch)

### Fixed

- `grid.css`: removed duplicated `width: 100%` declarations in the `.col1`–`.col12` base rule and obsolete `-webkit-box-sizing` / `-moz-box-sizing` vendor prefixes. (patch)

## [2.6.0] - 2026-07-14

### Removed

- Message bar close button (`.msg-bar-close-button`, `.msg-close-icon`): removed from the component as messages auto-dismiss and the button had poor UX on mobile, taking up valuable screen space.

### Changed

- Message bar text (`.msg-bar-text`): simplified layout from `inline-block` with margins to `display: block` with padding for cleaner, more predictable rendering.
