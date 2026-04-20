# Existing Rule Capture — agentic-browser-ui

> captured: 2026-04-20  
> source: code inspection across all 8 components + index.css  
> status: confirmed-standard / tentative / unresolved-gap (per rule)

---

## Tech-Stack Profile

| Field | Value |
|---|---|
| target | web |
| framework | react (Vite + TypeScript) |
| token_format | css-vars + Tailwind v4 (`@import "tailwindcss"`) |
| design_system | custom-ds (provisional label) |
| component_source | code-components (no Figma library link) |
| asset_profile | SVG `@1x` for icons; PNG `@1x` for raster content |
| verification_surface | browser (local dev server) |

---

## Token System

### Color tokens (all provisional — defined in `src/index.css`)

| Token | Value | Usage |
|---|---|---|
| `--color-text-primary` | `#333333` | body text, icon default |
| `--color-text-secondary` | `#666666` | secondary labels |
| `--color-text-tertiary` | `#999999` | placeholder, muted |
| `--color-text-disabled` | `#cccccc` | disabled text, dividers |
| `--color-surface-base` | `#ffffff` | card / input background |
| `--color-surface-app-bg` | `#ebeef5` | page-level background |
| `--color-surface-window` | `#fafafa` | browser window shell |
| `--color-surface-overlay-white` | `rgba(255,255,255,0.8)` | model toggle pill |
| `--color-surface-button-secondary` | `rgba(0,0,0,0.1)` | send button bg |
| `--color-border-default` | `#d9d9d9` | standard border |
| `--color-border-subtle` | `rgba(0,0,0,0.08)` | subtle separator |
| `--color-border-input-default` | `#000000` | (unused in practice — tentative) |
| `--color-state-hover-overlay` | `rgba(0,0,0,0.04)` | hover overlay layer |
| `--color-focus-ring` | `rgba(0,128,255,0.2)` | focus ring (unused in practice — tentative) |
| `--color-border-focus` | `#1f63ed` | input focus border |
| `--color-border-error` | `#e53b33` | input error border |
| `--color-surface-disabled` | `#f9f9fa` | disabled input bg |

**Unresolved gap:** `--color-border-input-default` and `--color-focus-ring` are defined but not consumed by any component. Likely stale or reserved.

### Spacing tokens

| Token | Value |
|---|---|
| `--spacing-4` | `4px` |
| `--spacing-8` | `8px` |
| `--spacing-12` | `12px` |
| `--spacing-16` | `16px` |
| `--spacing-24` | `24px` |

**Tentative:** spacing tokens are defined but components use Tailwind arbitrary values (`px-[12px]`, `gap-[8px]`) directly rather than consuming the CSS vars. The tokens exist as documentation, not as enforced constraints.

### Radius tokens

| Token | Value | Usage |
|---|---|---|
| `--radius-8` | `8px` | buttons, tab inner, model toggle |
| `--radius-12` | `12px` | prompt chips |
| `--radius-24` | `24px` | InputBox shell |
| `--radius-99` | `99px` | pills, send button |

**Confirmed standard:** radius tokens are consumed via `rounded-[var(--radius-*)]` in InputBox and some components. Inconsistently applied elsewhere (arbitrary values used in parallel).

---

## Icon Rules

**Confirmed standard:**
- All design-owned icons must be exported from Figma source before implementation (hard gate).
- If the asset exists in `src/assets/figma/`, import it. If not, export it first.
- Do not ship inline SVG or handwritten geometry while the export check is incomplete.

**SVG import pattern:**
- `?react` import → use as React component with `className` for `currentColor` theming (theme-reactive icons)
- Regular import → use as `<img src={...}>` for icons with hardcoded colors baked into the SVG

**Confirmed standard — color baking rule:**
- Exported SVGs with hardcoded `#333333` = `--color-text-primary` → use as `<img>`
- Exported SVGs with hardcoded `#999999` = `--color-text-tertiary` → use as `<img>`
- Exported SVGs using `currentColor` → use as `?react` component

**Unresolved gap:** Toolbar has two inline SVG dividers (`NavDivider`, `RightDivider`) that are not exported assets. These use `currentColor` and are structural, not design-owned icons — acceptable as inline, but not explicitly documented as an exception to the export gate.

**Confirmed standard — icon sizing:**
- Compact action-icon controls: `24×24` hit area, `16×16` icon frame (default pattern)
- Exported SVG canvas size is packaging data, not rendered-size contract — normalize via `className` size, not by changing layout

---

## Stateful Border Rule

**Confirmed standard:** stateful borders must not change geometry between states. Visual ring expressed via `inset box-shadow` (not border-width change) to avoid layout shift. Applied in InputBox.

---

## Component Prop API Conventions

**Confirmed standard:**
- Boolean props for simple on/off states: `selected`, `hovered`, `bookmarked`, `urlFocused`
- Optional callback props: `onClick?`, `onClose?`, `onSend?`
- Optional `ReactNode` slots for composition: `assistantButton?: ReactNode | null`
  - `undefined` → render default; `null` → render nothing; provided value → render that value
- Default prop values always provided (no required props except label/content)

---

## Interaction State Pattern

**Confirmed standard (AIToolsRow, Tab):** hover and active states managed via local `useState` + mouse event handlers (`onMouseEnter`, `onMouseLeave`, `onMouseDown`, `onMouseUp`). No global state or CSS-only hover.

**Tentative:** Dialog close icon uses the same pattern but also accepts a `variant` prop to force hover state for Figma verify purposes. This dual-mode (prop-driven + pointer-driven) is a verify affordance, not a general pattern.

---

## Typography

**Confirmed standard:**
- `HYQiHei:60S` — primary body text, labels, button text (14px / 20px leading)
- `HYQiHei:55S` — input placeholder (16px / 24px leading)
- `PICO_Sans_VFE_SC:Light` — assistant chip label (12px)
- `SF Pro` — browser tab active label (12px, Latin/system context)
- All font families applied via inline `style={{ fontFamily: ... }}` with `PingFang SC` or `sans-serif` fallback

**Unresolved gap:** HYQiHei font loading is deferred across all components. Font may not render correctly in all environments. Shared typography pass is a known non-blocker.

**Unresolved gap:** `fontFeatureSettings: "'ss01' 1, 'cv01' 1, 'cv11' 1"` applied inconsistently — present on some HYQiHei:60S usages, absent on others.

---

## Layout Conventions

**Confirmed standard:**
- Fixed pixel dimensions for component shells (no fluid sizing within components)
- `w-full` only used inside a component when the parent constrains width
- If Figma gives an explicit inner row width, preserve it (e.g. `w-[368px]` for prompt list inside 400px panel)
- Overflow hidden on shells that clip content

**Confirmed standard — section headers with optional actions:**
- Model as separate slots (`label` + optional `action`) not as a single undifferentiated row
- Applied in Sidebar `SidebarSectionHeader`

---

## Asset Naming Convention

**Confirmed standard:** `{component}-{descriptor}@{scale}.{ext}`

Examples:
- `toolbar-back@1x.svg`
- `inputbox-send@1x.svg`
- `assistant-title-history@1x.svg`
- `dialog-close-default@1x.svg`

All assets live in `src/assets/figma/`. Source node mapping tracked in `slices-name-map.json`.

---

## Provisional State Rules

**Confirmed standard:**
- Provisional boards must be standalone (not inside a formal artboard), with clear canvas separation
- Provisional state cards must apply state to the root control container, not by appending extra layers
- Do not promote a component set to canonical while any family boundary or state axis is still provisional

---

## Unresolved Gaps Summary

| Gap | Location | Status |
|---|---|---|
| `--color-border-input-default` and `--color-focus-ring` unused | `index.css` | stale or reserved — confirm or remove |
| Spacing tokens not consumed by components | all components | tokens exist as docs only; components use arbitrary Tailwind values |
| Radius tokens inconsistently applied | mixed | some components use `var(--radius-*)`, others use arbitrary values |
| `NavDivider` / `RightDivider` inline SVG in Toolbar | `Toolbar.tsx` | structural dividers, not design-owned icons — needs explicit exception rule |
| `fontFeatureSettings` inconsistently applied | multiple | present on some HYQiHei:60S usages, absent on others |
| HYQiHei font loading | all components | deferred non-blocker, shared typography pass needed |
| Tab.tsx `CloseIcon` inline SVG | `Tab.tsx` | no exported asset exists — needs export or explicit exception |
