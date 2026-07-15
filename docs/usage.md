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
- `.col1` … `.col12` — column widths on a 12-column grid. Columns stack full-width by default and take their fractional width from `min-width: 800px` upward.
- `.g-row.gutter` — above `min-width: 800px`, adds horizontal spacing between the row's columns instead of having them sit flush against each other.
- `.col-offset1` … `.col-offset11` — used on a column above `min-width: 800px` to push it right by that many columns of empty space, without needing an empty placeholder column.
- `.g-row.flex-align` — above `min-width: 800px`, switches the row to `display: flex; align-items: center` instead of floats.
- `.align-top`, `.align-middle`, `.align-bottom` — used on a column inside `.g-row.flex-align` to set `align-self`.

See [docs/examples/grid.html](examples/grid.html) for runnable examples of equal and unequal columns, gutters, offsets, and flex alignment.

## Structure and spacing (`commons.css`)

### Input behavior

- `.noselect` — disables text selection.

### Position and alignment

- `.fixed`, `.absolute` — `position` shortcuts.
- `.left-aligned`, `.right-aligned`, `.center-aligned` — `text-align` shortcuts.
- `.res-left-aligned`, `.res-right-aligned` — center text below `min-width: 800px`, then align left/right at and above it.

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
- `.res-pad-left{10,20,40,60,80}`, `.res-pad-right{10,20,40,60,80}` — zero below `min-width: 800px`, the named value at and above it.
- `.res-margin-left{10,20,30,40,50}`, `.res-margin-right{10,20,30,40,50}` — zero below `min-width: 800px`, the named value at and above it.
- `.res-top-margin-{10,20,30,40,50,80}` — the named `margin-top` value below `min-width: 800px`, zero at and above it.

### Go to top

```html
<a class="goto-top" href="#top" aria-label="Go to top">&uarr;</a>
```

Fixed-position button, hidden by default (`display: none`); a consuming project's JavaScript is expected to toggle its visibility on scroll.

## Images (`image.css`)

- `.light-shadow` — default soft drop shadow, even on all sides.
- `.subtle-shadow` — lighter drop shadow than `.light-shadow`, for a barely-there lift.
- `.base-shadow` — drop shadow offset toward the bottom, for a "resting on a surface" effect.
- `.rounded-img` — rounded corners.
- `.circle-img` — fully circular image (requires a square image or container).
- `.img-cover` — fills its container using `object-fit: cover`; pair with a fixed-size or `.aspect-ratio-*` container.
- `.img-contain` — fits inside its container using `object-fit: contain`, without cropping.
- `.img-grayscale` — grayscale by default, full color on hover.
- `.img-zoom-wrap` — wrapper that clips and smoothly zooms its child `<img>` on hover.
- `.img-caption-wrap` / `.img-caption` — overlays a caption with a dark gradient at the bottom of the image; wrap the image and a `.img-caption` element in `.img-caption-wrap`.

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

- `.datalist-table` — the table itself; rows highlight on hover by default.
- `.datalist-no-hover` — add to `.datalist-table` to disable the row hover highlight, for non-clickable rows.
- `.datalist-row-alt` — zebra-striping modifier for a `<tr>`.
- `.datalist-action-link` — inline command/link inside a cell (edit, delete, etc.).
- `.datalist-empty` — "no results" panel shown when the table has no rows.
- `.datalist-summary` — footer row pairing a record count with `.datalist-pager`.
- `.datalist-pager` / `.datalist-pager-current` — pagination list and its current-page indicator.

All colors, plus font size/weight and header corner rounding, are customizable per project via `--datalist-*` CSS variables; each has a fallback so the module works unstyled out of the box:

- `--datalist-font-size` (`13px`) — base font size for the table and `.datalist-empty`, so the empty-state message never renders larger than the table content.
- `--datalist-font-weight` (`600`) — header (`th`) font weight.
- `--datalist-action-font-weight` (`400`) — `.datalist-action-link` font weight; raise it per project for a heavier-looking action link.
- `--datalist-head-radius` (`6px`) — rounds the top-left/top-right corners of the header row; set to `0` to disable.
- `--datalist-head-bg` / `--datalist-head-color` — header background/text color.
- `--datalist-row-hover-bg`, `--datalist-row-alt-bg` — row hover and zebra-stripe background.
- `--datalist-text-color` — body cell text color.
- `--datalist-empty-bg` / `--datalist-empty-color` — empty-state panel colors.
- `--datalist-action-color` / `--datalist-action-hover-color` — row action link colors.
- `--datalist-summary-color` — summary/footer text color.
- `--datalist-pager-bg` / `--datalist-pager-color` / `--datalist-pager-border`, `--datalist-pager-hover-bg` / `--datalist-pager-hover-color` — pager link colors.
- `--datalist-pager-current-bg` / `--datalist-pager-current-color` / `--datalist-pager-current-border` — current-page indicator colors.
