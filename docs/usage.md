# Usage

Reference of the public classes provided by each Aptus module, with minimal HTML examples. See [docs/examples/](examples/) for larger, runnable pages, and [conventions.md](conventions.md) for the rules behind these classes. Source: [github.com/arriminum/aptus](https://github.com/arriminum/aptus).

Each module below is compiled separately; link only the modules a page actually needs (see [requirements.md](requirements.md) for file names).

## Reset (`reset.css`)

Applies `box-sizing: border-box`, removes default margin/padding on `html`/`body`, strips list bullets and spacing on `ul`/`ol`, removes link underline/outline, makes `img`/`video` fluid, and normalizes form controls (`button`, `select`, `textarea`, `input`) to inherit font and lose default borders/background. No classes; it applies to bare elements.

## Grid (`grid.css`)

```html
<div class="g-row">
  <div class="col6">First column</div>
  <div class="col6">Second column</div>
</div>
```

- `.g-row` — row container; clears its floated columns.
- `.col1` … `.col12` — column widths on a 12-column grid. Columns stack full-width by default and take their fractional width from `min-width: 768px` upward.
- `.g-row.gutter` — from `min-width: 768px`, adds horizontal spacing between columns while keeping the row's outer edges flush with its container.
- `.col-offset1` … `.col-offset11` — used on a column from `min-width: 768px` to push it right by that many columns of empty space, without needing an empty placeholder column.
- `.g-row.flex-align` — from `min-width: 768px`, switches the row to `display: flex; align-items: center` instead of floats.
- `.align-top`, `.align-middle`, `.align-bottom` — used on a column inside `.g-row.flex-align` to set `align-self`.

See [docs/examples/grid.html](examples/grid.html) for runnable examples of equal and unequal columns, gutters, offsets, and flex alignment.

## Structure and spacing (`commons.css`)

### Input behavior

- `.noselect` — disables text selection.

### Position and alignment

- `.fixed`, `.absolute` — `position` shortcuts.
- `.left-aligned`, `.right-aligned`, `.center-aligned` — `text-align` shortcuts.
- `.res-center-aligned` — centers text only at `max-width: 767.98px`.
- `.res-left-aligned`, `.res-right-aligned` — center text below `min-width: 768px`, then align left/right at and above it.

### Display

- `.block`, `.inline-block` — `display` shortcuts.
- `.full-width` — forces the element to `display: block; width: 100%` (with `!important`), including `max-width` and `flex-basis`.
- `.mob-hidden` — hides the element (`display: none !important`) at `max-width: 767.98px`.
- `.mob-full-width` — same behavior as `.full-width`, but only applied at `max-width: 767.98px`.

### Font weight and text

- `strong`, `.strong` — `font-weight: var(--font-weight-strong, 600)`.
- `b`, `.bold` — `font-weight: var(--font-weight-bold, 700)`.
- `.uppercase` — `text-transform: uppercase`.
- `.text-break` — allows long unbroken strings to wrap (`overflow-wrap: anywhere`).

### Visibility

- `.not-visible` — `visibility: hidden`, keeps layout space.
- `.hidden` — `display: none !important`, removes layout space.
- `.invisible` — both hidden visually and removed from layout.

### Rounded corners

- `.rounded-2px`, `.rounded-4px`, `.rounded-8px` — fixed `border-radius` values.

### Status

```html
<span class="status-active">Active</span>
<span class="status-inactive">Inactive</span>
```

Compact inline badges; both currently render with the same green background variable (`--color-green`) unless the project overrides it.

### Lists

- `.def-list` — square bullets, `list-style-position: outside`.
- `.simple-list` — no bullets.

### Sizing, overflow, and margins

- `.overflow-hidden`, `.w-100`, `.h-auto`, `.mx-auto` — direct CSS shortcuts.
- `.left5` / `.left10` / `.left20` / `.left30` — `margin-left`.
- `.right5` / `.right10` / `.right20` / `.right30` — `margin-right`.
- `.top10` / `.top20` / `.top30` / `.top40` / `.top50` — `margin-top` (`.top10` uses `!important`).
- `.bottom10` / `.bottom20` / `.bottom30` / `.bottom40` / `.bottom50` — `margin-bottom`.
- `.pad10`, `.pad20` — `padding` on all sides.
- `.pad-left10` / `.pad-left20`, `.pad-right10` / `.pad-right20` — one-sided padding.
- `.hor-pad10` / `.hor-pad20` — left and right padding together.
- `.ver-pad10` / `.ver-pad20` — top and bottom padding together.
- `.res-pad-left{10,20,30,40,50,60,70,80,90,100}`, `.res-pad-right{10,20,30,40,50,60,70,80,90,100}` — zero below `768px`, the named value at `min-width: 768px` and above.
- `.res-margin-left{10,20,30,40,50,60}`, `.res-margin-right{10,20,30,40,50,60}` — zero below `768px`, the named value at `min-width: 768px` and above.
- `.res-margin-top-{10,20,30,40,50,60}` — the named `margin-top` value below `768px`, zero at `min-width: 768px` and above.

### Go to top

```html
<a class="goto-top" href="#top" aria-label="Go to top">&uarr;</a>
```

Fixed-position button, hidden by default (`display: none`); a consuming project's JavaScript is expected to toggle its visibility on scroll.

## Images (`image.css`)

- `.light-shadow` — default soft drop shadow, even on all sides.
- `.subtle-shadow` — lighter drop shadow than `.light-shadow`, for a barely-there lift.
- `.base-shadow` — drop shadow offset toward the bottom, for a "resting on a surface" effect.
- `.elevated-shadow` — stronger shadow for high-elevation surfaces.
- `.contained-shadow` — compact shadow that stays visually close to the element.
- `.framed-shadow` — subtle border combined with a very light shadow.
- `.rounded-img` — rounded corners.
- `.circle-img` — fully circular image (requires a square image or container).
- `.img-cover` — fills its container using `object-fit: cover`; pair with a fixed-size or `.aspect-ratio-*` container.
- `.img-contain` — fits inside its container using `object-fit: contain`, without cropping.
- `.img-grayscale` — grayscale by default, full color on hover.
- `.img-zoom-wrap` — wrapper that clips and smoothly zooms its child `<img>` on hover.
- `.img-caption-wrap` / `.img-caption` — overlays a caption with a dark gradient at the bottom of the image; wrap the image and a `.img-caption` element in `.img-caption-wrap`.

## Breadcrumb (`breadcrumb.css`)

```html
<nav class="breadcrumb" aria-label="Breadcrumb">
  <ol>
    <li><a href="/">Home</a></li>
    <li><a href="/guides/">Guides</a></li>
    <li aria-current="page">Current page</li>
  </ol>
</nav>
```

The component shows only the final two items on mobile and the full, wrapping trail from `min-width: 768px`. The final item truncates with an ellipsis on narrow screens. Customize it with `--font-size-small`, `--link-color`, `--text-muted-color`, and `--text-color`.

See [docs/examples/breadcrumb.html](examples/breadcrumb.html) for a runnable example.

## Eyebrow (`eyebrow.css`)

```html
<div class="eyebrow">
  <span class="eyebrow-mark" aria-hidden="true"></span>
  Featured
</div>
```

`.eyebrow` creates an uppercase section label using `--font-size-small`, `--font-weight-bold`, and `--accent-color`. Add the optional `.eyebrow-mark` child for the short gradient rule.

See [docs/examples/eyebrow.html](examples/eyebrow.html) for a runnable example.

## Modal (`modal.css`)

```html
<dialog class="ui-modal ui-modal-default" aria-labelledby="ui-modal-title-1">
  <header class="ui-modal-header">
    <h2 class="ui-modal-title" id="ui-modal-title-1">Title</h2>
    <button type="button" class="ui-modal-close" aria-label="Close">×</button>
  </header>
  <div class="ui-modal-body">…</div>
  <footer class="ui-modal-footer">…</footer>
</dialog>
```

Structural frame for a native `<dialog>` opened with `showModal()`: size, centering, a scrolling body between fixed header and footer, a blurred backdrop matching `.msg-alert-overlay`, and a bottom-sheet layout below `768px`. Content inside the body is not styled, except that the margins of its first and last child are removed (the body padding is the spacing). The header and footer have no dividers: a soft shadow appears at the top or bottom of the body only while content is scrolled out of view there. Put the main actions in `.ui-modal-footer` so they stay visible when the body scrolls. The title has the same size as the body text, in bold, whatever heading element is used. The dialog resets `text-align` to `start`, so a page-level `text-align: center` does not leak into it. Sizes: `.ui-modal-narrow` (420px), `.ui-modal-default` (640px), `.ui-modal-wide` (960px), `.ui-modal-full`. States: `.ui-modal-body.is-loading` (spinner), `.ui-modal.is-busy` (progress cursor), `.ui-modal.is-closing` (exit animation; call `close()` after ~250ms). Add `html.ui-modal-open` while a modal is open to lock page scroll. Uses `--color-surface` and `--color-text` with fallbacks. Custom properties on `.ui-modal`: `--ui-modal-padding` (30px, 20px on mobile), `--ui-modal-radius` (16px), `--ui-modal-title-size` (1em), and `--ui-modal-title-weight` (700).

See [docs/examples/modal.html](examples/modal.html) for a runnable example.

### Sheet modifier

```html
<dialog class="ui-modal ui-modal-sheet" aria-labelledby="ui-modal-title-1">…</dialog>
```

`.ui-modal-sheet` is for side panels such as a filter panel. Below `768px` it is a bottom sheet with a decorative drag handle, at most `85dvh` tall (`85vh` fallback), with the body scrolling between the fixed header and footer, the footer clearing `env(safe-area-inset-bottom)`, and the footer actions (for example "Clear" and "Apply") sharing the width. It slides up from the bottom and respects `prefers-reduced-motion`. On desktop it behaves like `.ui-modal-narrow` (a centered 420px modal); a right-side drawer was considered and left out to keep the module simple. A `.ui-modal` without the modifier is unchanged.

The sheet is demonstrated in [docs/examples/modal.html](examples/modal.html) as well.

## Menu (`menu.css`)

```html
<button type="button" class="ui-menu-trigger" aria-haspopup="menu" aria-expanded="false" aria-controls="m1" aria-label="More actions">
  <i class="fa-solid fa-ellipsis" aria-hidden="true"></i>
</button>
<div class="ui-menu" id="m1" role="menu" hidden>
  <div class="ui-menu-title">Acme Corp</div>
  <div class="ui-menu-label">Create</div>
  <a class="ui-menu-item" role="menuitem" href="…"><i class="fa-solid fa-plus" aria-hidden="true"></i>New company</a>
  <button class="ui-menu-item" role="menuitem" type="button">Export</button>
  <div class="ui-menu-sep" role="separator"></div>
  <button class="ui-menu-item ui-menu-item-danger" role="menuitem" type="button">Delete</button>
  <button class="ui-menu-item ui-menu-cancel" type="button">Cancel</button>
</div>
```

Action menu ("⋯") styles; positioning, keyboard and history behavior belong to the JS (Palatium's `ActionMenu`).

- `.ui-menu-trigger`: square icon button, 36px (44px below `768px`), with a light border; `.ui-menu-trigger-plain` drops the border for use inside rows. `[aria-expanded="true"]` marks it open.
- `.ui-menu`: `position: fixed` popover (the JS sets `top`/`left`), 200px minimum width, at most `min(320px, 100vw - 16px)`, scrolling when taller than the viewport. The `hidden` attribute hides it. The JS sets `data-placement="bottom-end|bottom-start|top-end|top-start"` so the entry animation grows from the trigger's side (default `bottom-end`).
- `.ui-menu-item`: `<a>` or `<button>` row with the same look, about 36px tall on desktop and 48px on mobile, with an optional fixed-width leading icon (`<i>`, `<svg>` or `.ui-menu-icon`). Keyboard focus shows an outline, not only a background. `[aria-disabled="true"]` (or `:disabled`) dims the item. `.ui-menu-item-danger` turns it red.
- `.ui-menu-sep` (1px separator), `.ui-menu-label` (small uppercase group title).
- `.ui-menu-title` and `.ui-menu-cancel` (use with `.ui-menu-item`) only show in sheet mode, so server-rendered menus can always include them.
- `.ui-menu-sheet`: the same menu as a bottom sheet (full width, rounded top corners, drag handle, larger items, `env(safe-area-inset-bottom)` padding, slides up). The JS must not set `top`/`left` inline in this mode. Pair it with a `<div class="ui-menu-backdrop">` (translucent dark overlay, sheet mode only).
- Animation: entry runs from `@starting-style` when `hidden` is removed; for the exit, add `.is-closing` to the menu (and backdrop), wait for `transitionend` with a timeout fallback, then set `hidden`. Durations are 140ms for the popover and 220ms for the sheet; `prefers-reduced-motion: reduce` removes them.

Theme variables (all with fallbacks, set on `:root` or on the menu): `--ui-menu-bg`, `--ui-menu-text`, `--ui-menu-muted`, `--ui-menu-border`, `--ui-menu-hover`, `--ui-menu-focus`, `--ui-menu-shadow`, `--ui-menu-radius`, `--ui-menu-padding`, `--ui-menu-font-size`, `--ui-menu-danger` / `--ui-menu-danger-strong` / `--ui-menu-danger-hover`, `--ui-menu-cancel-bg` / `--ui-menu-cancel-hover`, `--ui-menu-handle`, `--ui-menu-backdrop`, `--ui-menu-z` (1000; the backdrop sits one below), and `--ui-menu-trigger-text` / `--ui-menu-trigger-border` / `--ui-menu-trigger-border-active`. Falls back to `--color-surface` and `--color-text` where set.

See [docs/examples/menu.html](examples/menu.html) for a runnable example.

## Chips (`chip.css`)

```html
<button type="button">Filters <span class="ui-count">2</span></button>

<ul class="ui-chip-list" aria-label="Active filters">
  <li class="ui-chip">
    <span class="ui-chip-text"><span class="ui-chip-key">Stage:</span> Lead</span>
    <button type="button" class="ui-chip-remove" aria-label="Remove filter Stage: Lead"><i class="fa-solid fa-xmark" aria-hidden="true"></i></button>
  </li>
  <li><button type="button" class="ui-chip-clear">Clear all</button></li>
</ul>
```

`.ui-chip-list` is an unstyled wrapping flex list (6px gap; at least 8px between wrapped lines below `768px`). `.ui-chip` is a small pill (about 28px tall, 36px below `768px`) whose `.ui-chip-text` is cut with an ellipsis when too long; `.ui-chip-key` is a dimmer label. `.ui-chip-remove` is a 20px round button with an invisible 32px touch target (24px with a 44px target below `768px`; the row gap keeps the targets of chips on wrapped lines from overlapping). `.ui-chip-clear` is a discreet link-style button (at least 44px tall below `768px`). `.ui-count` is a small numeric badge for buttons, hidden while `:empty`, so the JS only writes or clears the number.

Theme variables (all with fallbacks): `--ui-chip-gap`, `--ui-chip-font-size`, `--ui-chip-bg`, `--ui-chip-text`, `--ui-chip-border`, `--ui-chip-key`, `--ui-chip-remove`, `--ui-chip-remove-hover`, `--ui-chip-clear`, `--ui-chip-focus`, `--ui-count-bg`, `--ui-count-text`.

See [docs/examples/chip.html](examples/chip.html) for a runnable example.

## UI (`ui.css`)

### Responsive images

```html
<img class="ui-img-md" src="example.jpg" alt="Example image">
```

- `.ui-img-tn` (124px), `.ui-img-sm` (320px), `.ui-img-md` (400px), `.ui-img-lg` (640px), `.ui-img-xl` (1256px) — fluid images capped at the given `max-width`.

### Text

- `.notetext` — muted note text.
- `.old-text` — strikethrough, for superseded values such as an old price.

### Check list

```html
<ul class="ui-check-list">
  <li>Simple setup</li>
</ul>
```

Adds a green check mark before each `li` using a CSS mask, no external icon file required.

### Sliding buttons

```html
<a class="ui-btn-slide" href="#">Default Slide</a>
<a class="ui-btn-slide ui-btn-slide-red" href="#">Red Slide</a>
<a class="ui-btn-slide ui-btn-slide-green" href="#">Green Slide</a>
```

- `.ui-btn-slide` — base sliding-background hover button, colored via `--accent-color`.
- `.ui-btn-slide-white`, `.ui-btn-slide-red`, `.ui-btn-slide-green` — color variants, combined with `.ui-btn-slide`.
- `.white-sliding-cta`, `.red-sliding-cta`, `.green-sliding-cta` (and their `-2` suffixed variants) — legacy aliases kept for backward compatibility; prefer the `.ui-btn-slide*` classes in new code.

### Text with background

```html
<span class="ui-text-bg">Default highlight</span>
<span class="ui-text-bg-red">Red highlight</span>
<span class="ui-text-bg-green">Green highlight</span>
```

- `.black-text-bg`, `.shock-red-text-bg`, `.red-text-bg`, `.green-text-bg` — legacy aliases for the same highlight styles.

### Old browser warning

```html
<div id="old-browser-warning">
  <span class="bwarn-cont">Your browser is outdated. Please update it.</span>
</div>
```

Fixed banner at the top of the viewport; `#old-browser-warning` is an id, meant to appear once per page.

### Spinner and fade effects

- `.el-spinner` — small inline rotating loader.
- `.el-fade-out` — `opacity: 0`.
- `.el-fade-up` — starts translated down and transparent; add `.visible` to transition it into place.

### UI state

- `.ui-is-loading` — mutes and disables pointer events on a control (`opacity: 0.7; pointer-events: none`), typically combined with other button classes while an action is in flight.

### Spacer

```html
<div class="spacer spacer-20"></div>
```

`.spacer` is a full-width, zero-content block whose height comes from `--spacer-size`; combine it with `.spacer-10`, `.spacer-20`, `.spacer-30`, `.spacer-40`, or `.spacer-50` to set that height.

## Notifications (`notification.css`)

### Message bar

```html
<div class="msg-bar msg-bar-info">
  <span class="msg-bar-text">Saved successfully.</span>
  <button class="msg-bar-close-button" type="button">
    <svg class="msg-close-icon">…</svg>
  </button>
</div>
```

- `.msg-bar` — fixed top bar, starts hidden (`opacity: 0`); a project's JavaScript is expected to toggle visibility.
- `.msg-bar-info`, `.msg-bar-error` — color variants.
- `.msg-bar-close-button`, `.msg-close-icon`, `.msg-bar-text` — internal structural pieces.

### Form error

```html
<div class="form-error-box-cont">
  <span class="form-error-box">
    <span class="form-error-icon"></span>
    <span class="form-error-text">This field is required.</span>
  </span>
</div>
```

`.form-error-icon` renders `/res/img/aptus/form-error.svg` as a CSS mask; per [conventions.md](conventions.md), a missing icon file must not prevent `.form-error-text` from being shown.

### Overlay and loading messages

- `.fade-overlay` — fixed, full-screen translucent overlay with blur, starts hidden.
- `.trace-message`, `.ajax-loading` — fixed toast-style message box, starts hidden and slightly translated.
- `.msg-loader-icon` — small inline loading icon for use inside `.trace-message` / `.ajax-loading`.

## Autocomplete (`autocomplete.css`)

Styling for a text-input autocomplete suggestion list (no JavaScript included):

- `.autocomplete-suggestions` — the dropdown container.
- `.autocomplete-suggestion` — a single suggestion row.
- `.autocomplete-selected` — the currently highlighted suggestion.
- `.autocomplete-group` — a group heading inside the suggestion list.

## GDPR banner (`gdpr.css`)

```html
<div id="gdpr-box" class="gdpr-bottom-box">
  <div class="gdpr-bottom-box-cont">
    <p>This site uses cookies.</p>
    <button type="button">Accept</button>
  </div>
</div>
```

- `.gdpr-bottom-box` / `.gdpr-bottom-box-cont` — fixed bottom consent banner and its inner card.
- `#gdpr-box.noshow` — id-based modifier that fades the banner out and disables pointer events; toggled by a project's JavaScript after consent is given.

## Datalist (`datalist.css`)

Styling for a table of data fetched from a service: header, hoverable rows, row actions, empty state, and a summary/pager footer.

The table does not reflow on small screens: wrap it in a container with `overflow-x: auto` so it scrolls inside that container instead of widening the page, or use the row list (`.datalist`, below), which is built for mobile.

```html
<table class="datalist-table">
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
    <tr data-id="16">
      <td>John Smith</td>
      <td>Manager</td>
    </tr>
    <tr data-id="17" class="datalist-row-alt">
      <td>Alice Doe</td>
      <td>Analyst</td>
    </tr>
  </tbody>
</table>

<div class="datalist-summary">
  <span>Total de registros: 2</span>
  <ul class="datalist-pager">
    <li><a href="#">&laquo;</a></li>
    <li><span class="datalist-pager-current">1</span></li>
    <li><a href="#">&raquo;</a></li>
  </ul>
</div>
```

- `.datalist-table` — the table itself; rows highlight on hover by default. Set `--datalist-table-border` to a complete border value (for example, `1px solid #dddddd`) to add an outer border and separators between body rows.
- `.datalist-no-hover` — add to `.datalist-table` to disable the row hover highlight, for non-clickable rows.
- `.datalist-row-alt` — zebra-striping modifier for a `<tr>`.
- `.datalist-action-link` — inline command/link inside a cell (edit, delete, etc.).
- `.datalist-empty` — centered "no results" message shown when the table has no rows; it has no background or text color of its own and inherits the surrounding text color.
- `.datalist-summary` — footer row pairing a record count with `.datalist-pager`.
- `.datalist-pager` / `.datalist-pager-current` — pagination list and its current-page indicator. Below `768px` each page link and the current page become 44px touch targets with a 14px font, and the list wraps.

All colors, plus font size/weight and header corner rounding, are customizable per project via `--datalist-*` CSS variables; each has a fallback so the module works unstyled out of the box:

- `--font-size-datalist` (no default: when unset, the table, `.datalist-summary` and `.datalist-empty` inherit the surrounding font size; the row list falls back to `14px`) — base font size for the table, the summary and `.datalist-empty`, so the empty-state message never renders larger than the table content. Define it in the consuming project (for example `13px`).
- `--datalist-font-weight` (`600`) — header (`th`) font weight.
- `--datalist-action-font-weight` (`400`) — `.datalist-action-link` font weight; raise it per project for a heavier-looking action link.
- `--datalist-head-radius` (`6px`) — rounds the top-left/top-right corners of the header row; set to `0` to disable.
- `--datalist-head-bg` / `--datalist-head-color` — header background/text color.
- `--datalist-row-hover-bg`, `--datalist-row-alt-bg` — row hover and zebra-stripe background.
- `--datalist-text-color` — body cell text color.
- `--datalist-action-color` / `--datalist-action-hover-color` — row action link colors.
- `--datalist-summary-color` — summary/footer text color.
- `--datalist-pager-bg` / `--datalist-pager-color` / `--datalist-pager-border`, `--datalist-pager-hover-bg` / `--datalist-pager-hover-color` — pager link colors.
- `--datalist-pager-current-bg` / `--datalist-pager-current-color` / `--datalist-pager-current-border` — current-page indicator colors.

### Row list

An alternative to `.datalist-table` built from `ul > li`, with one real link per row. From `768px` up the cells line up in columns under a header row; at `max-width: 767.98px` each row becomes a native-app list item (title and badge/value on line 1, muted subtitles on line 2, optional meta on line 3), edge to edge with thin separators.

```html
<div class="datalist" style="--datalist-cols: 3fr 2fr 3fr 1fr">
  <div class="datalist-head" aria-hidden="true">
    <span>Name</span><span>Role</span><span>Email</span><span>Status</span>
  </div>
  <ul class="datalist-list">
    <li class="datalist-item">
      <a class="datalist-link" href="/contact/?k=12">
        <span class="datalist-cell datalist-title">Nina Cat</span>
        <span class="datalist-cell datalist-sub">CEO</span>
        <span class="datalist-cell datalist-sub is-empty"></span>
        <span class="datalist-cell datalist-badge"><span class="datalist-tag">Inactive</span></span>
      </a>
      <div class="datalist-actions">
        <a class="datalist-action" href="tel:19981132743" aria-label="Call Nina Cat"><i class="fa-solid fa-phone" aria-hidden="true"></i></a>
      </div>
    </li>
  </ul>
  <div class="datalist-summary"><span>Showing 20 of 134</span></div>
  <div class="datalist-more"><button type="button" class="datalist-more-btn">Load more</button></div>
</div>
```

- `.datalist` — container; `--datalist-cols` (a `grid-template-columns` value) sets the desktop columns shared by `.datalist-head` and every `.datalist-link`.
- `.datalist-head` — visual header row (desktop only, mark it `aria-hidden="true"`); add `.datalist-value` to a header `span` to right-align its label.
- `.datalist-list` / `.datalist-item` — the `ul` and each `li`; the `li` is a grid `[link] [actions]`.
- `.datalist-link` — the row link, covering the whole row (hover on pointer devices, `:active` state, `:focus-visible` outline).
- `.datalist-cell` plus one slot: `.datalist-title` (line 1 left, bold, ellipsis), `.datalist-value` (right-aligned column; line 1 right, before the badge), `.datalist-badge` (line 1 right), `.datalist-sub` (line 2, joined by "·"), `.datalist-meta` (line 3, smaller), `.datalist-desk` (desktop only).
- `.is-empty` — on an empty cell: keeps its column on desktop, hidden on mobile without leaving a stray separator.
- `.datalist-actions` / `.datalist-action` — quick actions outside the link; round 40px icon buttons that always need an `aria-label`. They are always visible (desktop and mobile). The column defaults to `48px` when the list contains `.datalist-actions` (`0` otherwise) and the header reserves the same width; override with `--datalist-actions-w`.
- `.datalist-tag` — neutral pill, with `.datalist-tag-muted`, `.datalist-tag-success`, `.datalist-tag-warning`, `.datalist-tag-danger`.
- `.datalist-summary` — reused as is; placed directly inside `.datalist`, it gets side padding that lines it up with the row content.
- `.datalist-more` / `.datalist-more-btn` — centered "Load more" button; `aria-busy="true"` on the button shows a spinner and blocks clicks; `hidden` on `.datalist-more` hides it.
- `.datalist-empty` — as an `li` inside `.datalist-list`, spans the whole row.
- `.datalist-selectable` / `.datalist-select` — selectable rows: each `li` becomes `[select] [link] [actions]`, with a `label.datalist-select` around the row checkbox (the whole column, `--datalist-select-w`, `44px`, is the touch target); the header reserves the same width. The row body may be a `label.datalist-link` pointing at the checkbox (`for`), so a click anywhere on the row toggles it instead of navigating. `.is-selected` on the `li` tints the selected rows.
- `.datalist-selectbar` — selection bar placed directly inside `.datalist`, before the rows: `label.datalist-selectbar-all` (a "select all shown" checkbox lined up with the row checkboxes; use its `indeterminate` state for a partial selection), `.datalist-selectbar-count` (the selected count) and `.datalist-selectbar-actions` (bulk actions, pushed to the end; wraps below on narrow screens).

Theme variables (all with fallbacks): `--datalist-list-font-size` / `--datalist-list-font-size-mob`, `--datalist-text-color`, `--datalist-title-color`, `--datalist-title-weight`, `--datalist-sub-color`, `--datalist-meta-color`, `--datalist-head-color`, `--datalist-separator`, `--datalist-list-bg`, `--datalist-row-bg`, `--datalist-row-hover-bg`, `--datalist-row-active-bg`, `--datalist-focus-color`, `--datalist-row-pad-x` / `--datalist-row-pad-y` (and `-mob` variants), `--datalist-row-min-h` / `--datalist-row-min-h-mob`, `--datalist-row-radius`, `--datalist-col-gap`, `--datalist-action-size`, `--datalist-action-bg` / `--datalist-action-hover-bg`, `--datalist-tag-bg` / `--datalist-tag-color` (and `--datalist-tag-{muted,success,warning,danger}-{bg,color}`), `--datalist-more-bg` / `--datalist-more-color` / `--datalist-more-border` / `--datalist-more-hover-bg`, `--datalist-select-w`, `--datalist-check-size` / `--datalist-check-color`, `--datalist-row-selected-bg` / `--datalist-row-selected-hover-bg`.

See [docs/examples/datalist-list.html](examples/datalist-list.html) for a runnable example.
