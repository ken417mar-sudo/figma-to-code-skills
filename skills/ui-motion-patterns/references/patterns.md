# UI Motion Pattern Templates

These templates are original starting points for common web interaction
motion. Adapt names, selectors, tokens, durations, and state attributes to
the target project. Do not paste them unchanged into production code when
the project already has naming or token conventions.

## Motion Defaults

- Micro feedback: `120ms-180ms`
- Buttons, cards, tabs: `180ms-240ms`
- Dropdowns, modals, panels, pages: `220ms-320ms`
- Standard ease: `cubic-bezier(0.22, 1, 0.36, 1)`
- Gentle open ease: `cubic-bezier(0.16, 1, 0.3, 1)`
- Fast close ease: `cubic-bezier(0.4, 0, 1, 1)`

Prefer `transform`, `opacity`, and carefully scoped `filter`. Avoid
`transition: all`.

## Tab Indicator

Use for segmented controls and navigation tabs when the active background
or underline should glide between measured tab positions.

```css
.motion-tabs {
  position: relative;
  display: inline-flex;
}

.motion-tab-indicator {
  position: absolute;
  inset-block: 4px;
  left: 0;
  width: var(--motion-tab-width, 0px);
  border-radius: 999px;
  background: var(--color-accent);
  transform: translateX(var(--motion-tab-x, 0px));
  transition:
    transform var(--motion-tab-dur, 220ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1)),
    width var(--motion-tab-dur, 220ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1));
  pointer-events: none;
}

@media (prefers-reduced-motion: reduce) {
  .motion-tab-indicator {
    transition: none !important;
  }
}
```

```js
function syncTabIndicator(root, activeTab) {
  root.style.setProperty("--motion-tab-x", activeTab.offsetLeft + "px");
  root.style.setProperty("--motion-tab-width", activeTab.offsetWidth + "px");
}
```

## Dropdown Reveal

Use for menus and popovers that should scale/fade from the trigger
origin. Keep focus and outside-click behavior in the component code.

```css
.motion-dropdown {
  transform-origin: top center;
  transform: scale(var(--dropdown-pre-scale, 0.97));
  opacity: 0;
  pointer-events: none;
  transition:
    transform var(--dropdown-open-dur, 220ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1)),
    opacity var(--dropdown-open-dur, 220ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1));
  will-change: transform, opacity;
}

.motion-dropdown.is-open {
  transform: scale(1);
  opacity: 1;
  pointer-events: auto;
}

.motion-dropdown.is-closing {
  transform: scale(var(--dropdown-close-scale, 0.99));
  opacity: 0;
  pointer-events: none;
  transition-duration: var(--dropdown-close-dur, 140ms);
}

@media (prefers-reduced-motion: reduce) {
  .motion-dropdown {
    transition: none !important;
    transform: none !important;
  }
}
```

## Modal Open And Close

Use a three-state flow when the modal must animate out before being hidden:
`closed -> open -> closing -> closed`.

```css
.motion-modal-overlay {
  opacity: 0;
  pointer-events: none;
  transition: opacity var(--modal-overlay-dur, 180ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1));
}

.motion-modal {
  opacity: 0;
  transform: translateY(8px) scale(0.96);
  transition:
    opacity var(--modal-open-dur, 240ms) var(--modal-open-ease, cubic-bezier(0.16, 1, 0.3, 1)),
    transform var(--modal-open-dur, 240ms) var(--modal-open-ease, cubic-bezier(0.16, 1, 0.3, 1));
}

.motion-modal-overlay.is-open,
.motion-modal-overlay.is-closing {
  pointer-events: auto;
}

.motion-modal-overlay.is-open {
  opacity: 1;
}

.motion-modal-overlay.is-open .motion-modal {
  opacity: 1;
  transform: translateY(0) scale(1);
}

.motion-modal-overlay.is-closing {
  opacity: 0;
  transition-duration: var(--modal-close-dur, 140ms);
}

.motion-modal-overlay.is-closing .motion-modal {
  opacity: 0;
  transform: translateY(6px) scale(0.98);
  transition-duration: var(--modal-close-dur, 140ms);
}

@media (prefers-reduced-motion: reduce) {
  .motion-modal-overlay,
  .motion-modal {
    transition: none !important;
    transform: none !important;
  }
}
```

## Panel Or Page Switch

Use for switching content panels without reflowing the surrounding layout.
If inactive panels must be removed from flow, do it after the exit state
finishes.

```css
.motion-panel {
  opacity: 0;
  transform: translateY(var(--panel-travel, 10px));
  filter: blur(var(--panel-blur, 3px));
  transition:
    opacity var(--panel-dur, 220ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1)),
    transform var(--panel-dur, 220ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1)),
    filter var(--panel-dur, 220ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1));
}

.motion-panel.is-active {
  opacity: 1;
  transform: translateY(0);
  filter: blur(0);
}

@media (prefers-reduced-motion: reduce) {
  .motion-panel {
    transition: none !important;
    transform: none !important;
    filter: none !important;
  }
}
```

## Page Side By Side

Use for forward/back flows where two pages occupy the same viewport or
panel slot. Keep the wrapper dimension fixed so page motion does not
change surrounding layout.

```css
.motion-page-stack {
  position: relative;
  overflow: hidden;
}

.motion-page {
  position: absolute;
  inset: 0;
  opacity: 0;
  pointer-events: none;
  transform: translateX(var(--page-exit-x, 8px));
  filter: blur(var(--page-blur, 2px));
  transition:
    opacity var(--page-fade-dur, 200ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1)),
    transform var(--page-slide-dur, 200ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1)),
    filter var(--page-slide-dur, 200ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1));
}

.motion-page[data-page-id="previous"] {
  --page-exit-x: -8px;
}

.motion-page-stack[data-page="previous"] .motion-page[data-page-id="previous"],
.motion-page-stack[data-page="next"] .motion-page[data-page-id="next"] {
  opacity: 1;
  pointer-events: auto;
  transform: translateX(0);
  filter: blur(0);
}

@media (prefers-reduced-motion: reduce) {
  .motion-page {
    transition: none !important;
    transform: none !important;
    filter: none !important;
  }
}
```

## Card Resize

Use when a component's own card body intentionally changes size, such as
expanded/collapsed details. Prefer animating fixed numeric dimensions or a
measured CSS variable; avoid `height: auto` transitions unless the
framework supplies a measured transition primitive.

```css
.motion-resize-card {
  width: var(--card-width, 320px);
  height: var(--card-height, 180px);
  overflow: hidden;
  transition:
    width var(--card-resize-dur, 260ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1)),
    height var(--card-resize-dur, 260ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1));
}

.motion-resize-card[data-size="compact"] {
  --card-width: var(--card-compact-width, 280px);
  --card-height: var(--card-compact-height, 120px);
}

.motion-resize-card[data-size="expanded"] {
  --card-width: var(--card-expanded-width, 320px);
  --card-height: var(--card-expanded-height, 220px);
}

@media (prefers-reduced-motion: reduce) {
  .motion-resize-card {
    transition: none !important;
  }
}
```

## Card Hover Lift

Use sparingly on repeated cards. Keep travel small so dense layouts remain
stable and scannable.

```css
.motion-card {
  transition:
    transform var(--card-motion-dur, 180ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1)),
    box-shadow var(--card-motion-dur, 180ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1)),
    border-color var(--card-motion-dur, 180ms) ease;
  will-change: transform;
}

.motion-card:hover,
.motion-card:focus-visible {
  transform: translateY(var(--card-hover-y, -2px));
}

@media (prefers-reduced-motion: reduce) {
  .motion-card {
    transition: none !important;
    transform: none !important;
  }
}
```

## Icon Swap

Use for toggles and status icons where both icons can remain in the DOM.

```css
.motion-icon-stack {
  position: relative;
  display: inline-grid;
  place-items: center;
}

.motion-icon {
  grid-area: 1 / 1;
  transition:
    opacity var(--icon-swap-dur, 180ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1)),
    transform var(--icon-swap-dur, 180ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1)),
    filter var(--icon-swap-dur, 180ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1));
}

.motion-icon[aria-hidden="true"] {
  opacity: 0;
  transform: scale(var(--icon-hidden-scale, 0.72));
  filter: blur(var(--icon-hidden-blur, 3px));
}

@media (prefers-reduced-motion: reduce) {
  .motion-icon {
    transition: none !important;
    transform: none !important;
    filter: none !important;
  }
}
```

## Text Swap

Use when command or status text changes, such as `Processing` to
`Complete`. Keep both text nodes in the same grid cell when possible.

```css
.motion-text-swap {
  display: inline-grid;
  place-items: center;
}

.motion-text-swap > span {
  grid-area: 1 / 1;
  transition:
    opacity var(--text-swap-dur, 160ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1)),
    transform var(--text-swap-dur, 160ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1)),
    filter var(--text-swap-dur, 160ms) var(--motion-ease, cubic-bezier(0.22, 1, 0.36, 1));
}

.motion-text-swap > span[aria-hidden="true"] {
  opacity: 0;
  transform: translateY(var(--text-swap-y, 6px));
  filter: blur(var(--text-swap-blur, 3px));
}

@media (prefers-reduced-motion: reduce) {
  .motion-text-swap > span {
    transition: none !important;
    transform: none !important;
    filter: none !important;
  }
}
```

## Badge Pop

Use for small status dots or count badges. Avoid applying this pattern to
large blocks.

```css
@keyframes motion-badge-pop {
  from {
    transform: translate(var(--badge-x, 8px), var(--badge-y, -8px)) scale(0.4);
    opacity: 0;
    filter: blur(var(--badge-blur, 3px));
  }
  to {
    transform: translate(0, 0) scale(1);
    opacity: 1;
    filter: blur(0);
  }
}

.motion-badge.is-entering {
  animation: motion-badge-pop var(--badge-pop-dur, 260ms) var(--badge-pop-ease, cubic-bezier(0.16, 1, 0.3, 1)) both;
}

@media (prefers-reduced-motion: reduce) {
  .motion-badge.is-entering {
    animation: none !important;
    transform: none !important;
    filter: none !important;
  }
}
```

## Number Change

Use for short counters and metric deltas. Render each character or number
group as a stable inline block so width changes do not collapse the row.

```css
@keyframes motion-number-in {
  from {
    transform: translateY(var(--number-travel, 8px));
    opacity: 0;
    filter: blur(var(--number-blur, 2px));
  }
  to {
    transform: translateY(0);
    opacity: 1;
    filter: blur(0);
  }
}

.motion-number-group {
  display: inline-flex;
  align-items: baseline;
  font-variant-numeric: tabular-nums;
}

.motion-number-group.is-entering .motion-number-char {
  animation: motion-number-in var(--number-dur, 420ms) var(--number-ease, cubic-bezier(0.16, 1, 0.3, 1)) both;
}

.motion-number-char[data-stagger="1"] {
  animation-delay: var(--number-stagger, 50ms);
}

.motion-number-char[data-stagger="2"] {
  animation-delay: calc(var(--number-stagger, 50ms) * 2);
}

@media (prefers-reduced-motion: reduce) {
  .motion-number-group .motion-number-char {
    animation: none !important;
    transform: none !important;
    filter: none !important;
  }
}
```

## State Machine Template

Use this shape for dropdowns, modals, and panels that need an animated
exit before unmount or `display: none`.

```js
function createClosingState(setState, closeDuration) {
  let closeTimer = null;

  function open() {
    if (closeTimer) {
      window.clearTimeout(closeTimer);
      closeTimer = null;
    }
    setState("open");
  }

  function close() {
    setState("closing");
    if (closeTimer) window.clearTimeout(closeTimer);
    closeTimer = window.setTimeout(() => {
      setState("closed");
      closeTimer = null;
    }, closeDuration);
  }

  function cleanup() {
    if (closeTimer) window.clearTimeout(closeTimer);
  }

  return { open, close, cleanup };
}
```

## Review Checklist

- Resting UI matches design before and after animation.
- Opening and closing behavior are both handled.
- Motion does not alter layout or hit-target geometry unexpectedly.
- Keyboard, focus, and escape behavior still work for overlays and menus.
- Reduced-motion mode removes nonessential travel, blur, and animation.
- Timers or animation listeners cannot race under repeated clicks.
