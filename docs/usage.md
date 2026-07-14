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
- `.g-row.flex-align` — above `min-width: 800px`, switches the row to `display: flex; align-items: center` instead of floats.
- `.align-top`, `.align-middle`, `.align-bottom` — used on a column inside `.g-row.flex-align` to set `align-self`.

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

- `.pol-img` — polaroid-style framed image (white border and soft shadow).
- `.pol-shadow` — standalone polaroid-style shadow, no border.
- `.def-shadow` — default drop shadow.
- `.light-shadow` — lighter drop shadow.

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

## Message bar and forms (`message-bar.css`)

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
