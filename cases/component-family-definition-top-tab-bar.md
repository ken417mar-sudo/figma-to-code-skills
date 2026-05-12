# Component Family Definition — TopTabBar

## Status

`closed` — operation + tab-strip first slice from Figma `2080:8062`.
Global actions (功能组, window controls) intentionally deferred.

## Source

- Figma file: `iIbL9V4UrFeORPaM7KVji7`
- Source node: `2080:8062` — Tab bar, 1166×52
- Confirmed state: home-selected (only state present in source node)

## Scope

TopTabBar is the application top bar. This first slice covers the left group only:

- Back/forward navigation buttons (32×32, disabled at `opacity-30`)
- 3-tab strip: 主页 (home-selected), 设置 (inactive), 小程序名称 (inactive)

The right-side global actions (新版本 pill, 签到 pill, user chip, pin/min/max/close window controls) are out of scope for this pass.

This is a distinct component family from:
- `Tab.tsx` — browser page tabs, 40px height, close controls
- `NavigationMenu.tsx` — pill-style content nav

## Implementation

- File: `agentic-browser-ui/src/components/TopTabBar.tsx`
- Verify surface: `agentic-browser-ui/src/App.tsx` TopTabBar verify card
- PRs: agentic-browser-ui #20, figma-to-code-skills (this PR)
- Exported assets:
  - `src/assets/figma/topbar-nav-arrow@1x.svg` — forward arrow (node `2080:3949`); rotated 180° for back
  - `src/assets/figma/topbar-home@1x.svg` — frame-preserving normalization of node `1020:11765`; 18×18 canvas, Union glyph 12.16×14.33 at translate(2.92, 1.84); `currentColor` fill → `#3f4046`
  - `src/assets/figma/topbar-settings@1x.svg` — manually composed from two child paths of node `6198:451788` (gear outline + center circle); `currentColor` stroke → `#18181b`
  - `src/assets/figma/topbar-apps-logo@1x.png` — PNG 36×36 (node `I2080:8062;1122:12338;1494:53862`), rendered at 18×18

## Component Axes

| Axis | Values | Definition status |
|---|---|---|
| selectedTabId | any tab id | prop-driven |
| canGoBack | true / false | prop-driven |
| canGoForward | true / false | prop-driven |
| global actions | — | out of scope for first slice |

## Geometry

| Property | Value |
|---|---|
| root size | `1166 × 52` |
| padding | `px-[14px] py-[10px]` |
| nav button size | `32 × 32` |
| nav button gap | `4px` |
| nav arrow SVG | `11.5 × 11.5` |
| gap: nav → tabs | `16px` |
| tab height | `32px` |
| tab min/max width | `38px / 200px` |
| tab padding | `px-[10px]` |
| active tab bg | `white`, `rounded-[8px]`, `drop-shadow-[0px_0.5px_0px_rgba(0,0,0,0.05)]` |
| inactive divider | `1px × 17px`, `rgba(0,0,0,0.16)`, absolute right-0 top-[7.5px], non-layout-affecting |
| icon size | `18 × 18` |
| icon-text gap | `6px` |
| tab text | `12px / 18px`, HYQiHei:60S, `#18181b` |
| disabled nav opacity | `0.3` |

## Verification Status

| Check | Status |
|---|---|
| Figma design context | passed: node `2080:8062` inspected |
| Asset inventory | passed: 4 assets exported/normalized, all recorded in slices-name-map.json |
| State-geometry scan | passed: inactive divider is absolute-positioned, non-layout-affecting |
| Build | passed: `npm run build` in agentic-browser-ui |
| Lint | passed: `npm run lint` |
| git diff --check | passed |
| Codex DOM review | passed (3 rounds): bar 1166×52; nav buttons 32×32; nav svg 11.5×11.5; tabs 200×32; active home bg white; home slot 18×18 with visible path 12.16×14.33 at #3F4046; settings svg 18×18 stroke #18181B; apps img 18×18 natural 36×36; inactive divider 1×17 top 7.5 |

## Durable Lessons

- **Frame-preserving normalization**: when exporting an icon, always export from the frame node (e.g. `1020:11765`), not the inner path/union. Exporting only the inner path gives a viewBox matching the path bounds, which stretches the glyph when rendered at the frame size. Fix: use an 18×18 canvas SVG and translate the path to its correct inset position.
- **currentColor requires an explicit color class**: SVG components using `currentColor` inherit from CSS `color`. If no `text-*` class is set on the component, the color falls back to black. Always set the source color explicitly on the icon component.
- **Shared arrow with rotation**: a single directional arrow SVG can serve both back and forward by applying `rotate(180deg)` in CSS — no need to export two separate assets.

## Deferred

- Right-side global actions: 新版本 pill, 签到 pill, user chip, pin/min/max/close window controls
- Hover/active states for nav buttons and tabs (no component set or hidden variants found in source node)
