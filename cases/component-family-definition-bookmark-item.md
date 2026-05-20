# Component Family Definition — BookmarkItem

## Status

`closed` — bookmark bar chip implemented from Figma `1708:30231~30233`. agentic-browser-ui PR #24 merged.

## Source

- Figma file: `iIbL9V4UrFeORPaM7KVji7`
- Source nodes: `1708:30231~30233` — 书签 instances in bookmark bar area `1708:30228`
- Page: Agentic Browser (`1708:29412`)

## Scope

BookmarkItem is a bookmark bar chip: `[icon 16×16] [label 12px]`. Three source instances:

| Node | Label | Width | Icon type |
|---|---|---|---|
| `1708:30233` | Collection | 85px | Generic star icon (visible) |
| `1708:30231` | Airbnb | 66px | App favicon, bg `#ff0057`, radius `8px` (hidden) |
| `1708:30232` | Disney + | 78px | App favicon, bg `#06062a`, radius `60px` (hidden) |

Width is content-driven (text length). Height is fixed at 24px.

**Component boundary:** distinct from the toolbar bookmark star button (`Toolbar.tsx` right actions area). BookmarkItem is the bookmark bar chip; the toolbar bookmark button is a separate star icon button.

## Implementation

- File: `agentic-browser-ui/src/components/BookmarkItem.tsx`
- Used in: `agentic-browser-ui/src/components/Toolbar.tsx` (right actions, Collection chip)
- PRs: agentic-browser-ui #24, figma-to-code-skills #61
- Exported assets: none new — reuses `toolbar-bookmark-icon@1x.svg` (star icon, `#FFCA28`)

## Component Axes

| Axis | Values | Definition status |
|---|---|---|
| label | string | prop-driven |
| appIconSrc | string (optional) | prop-driven — omit for generic star icon |
| appIconBg | string (optional) | prop-driven — background color for app favicon slot |
| appIconRadius | string (optional, default `8px`) | prop-driven — border radius for app favicon slot |

## Geometry

| Property | Value |
|---|---|
| height | `24px` |
| padding | `px-[4px]` |
| gap | `gap-[4px]` |
| icon slot | `size-[16px]`, `shrink-0` |
| app icon slot | `overflow-clip`, bg + radius from props |
| label | `text-[12px]`, `leading-normal`, `text-[var(--color-text-secondary)]` (`#666`), SF Pro, `whitespace-nowrap` |

## Verification Status

| Check | Status |
|---|---|
| Figma design context | passed: all 3 instances inspected (30231, 30232, 30233) |
| Asset inventory | passed: reuses existing star icon; no new export needed |
| State-geometry scan | passed: width is content-driven, height fixed 24px |
| Build | passed: `npm run build` |
| Lint | passed: `npm run lint` |
| git diff --check | passed |

## Durable Lessons

- **Inline extraction**: when a component is already implemented inline in a parent, extract it to a standalone file rather than duplicating. The inline `bookmarked` prop in Toolbar was a state flag for the star button, not a BookmarkItem prop — removing it clarified the component boundary.
- **Content-driven width**: bookmark bar chips have no fixed width — width is determined by label text length. Do not set a fixed width; let the container be `shrink-0` and width auto.
- **Two icon slot types in one component**: generic icon (plain img) and app favicon (img with bg + radius) can share one component with optional props rather than two separate components.
