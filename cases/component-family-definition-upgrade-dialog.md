# Component Family Definition — UpgradeDialog

## Status

`closed` — downloading state from Figma `2080:7977`. agentic-browser-ui PR #22 merged.

## Source

- Figma file: `iIbL9V4UrFeORPaM7KVji7`
- Source node: `2080:7977` — 升级弹窗, 310×216
- Confirmed state: downloading (75% progress shown)

## Scope

UpgradeDialog is a standalone upgrade/download progress dialog. This case covers the downloading state only.

**Component boundary:** distinct from `Dialog.tsx` — different border style (`outline outline-1 outline-black` vs `0.5px grey border/shadow`), different radius (`16px` vs `24px`), no button group, logo + progress bar only.

Deferred states: pre-download default and download-complete states (not present in source node).

## Implementation

- File: `agentic-browser-ui/src/components/UpgradeDialog.tsx`
- Verify surface: `agentic-browser-ui/src/App.tsx` UpgradeDialog verify cards (progress=75/30/100)
- PRs: agentic-browser-ui #22, figma-to-code-skills (this PR)
- Exported assets: none — progress bar uses CSS width, logo is a placeholder slot

## Component Axes

| Axis | Values | Definition status |
|---|---|---|
| progress | 0–100 | prop-driven |
| progressLabel | string (auto-derived if omitted) | prop-driven |
| logo | ReactNode (placeholder if omitted) | prop-driven |

## Geometry

| Property | Value |
|---|---|
| root | `310 × 216`, `rounded-[16px]`, `outline outline-1 outline-black`, `pb-[24px] px-[24px]` |
| content area | `262 × 192`, `flex-col gap-[6px]` |
| logo slot | `96 × 96`, centered |
| 下载进度 area | `262 × 32`, `flex-col gap-[8px]` |
| label row | `262 × 16`, left `#18181b` 14px, right `#6b6f7a` 14px, HYQiHei:60S |
| progress bar track | `262 × 8`, `rounded-[24px]`, `#d7d7db` |
| progress bar fill | CSS `width: {progress}%`, `#18181b`, `rounded-[24px]` |

## Verification Status

| Check | Status |
|---|---|
| Figma design context | passed: node `2080:7977` inspected |
| Asset inventory | passed: no exported assets needed |
| State-geometry scan | passed: progress bar track/fill are background-color-only, non-layout-affecting |
| Build | passed: `npm run build` in agentic-browser-ui |
| Lint | passed: `npm run lint` |
| git diff --check | passed |
| Codex DOM review | passed: root 310×216; content 262×192; logo 96×96; progress area 262×32; label row 262×16; track 262×8 bg #d7d7db; fill 75%=196.5×8 bg #18181b; 30%/100% scale correctly |

## Durable Lessons

- **Outline for exact-size dialog surfaces**: use `outline` instead of `border` when the Figma source specifies an exact frame size. `border` participates in layout under `border-box` sizing and shifts both root height and inner content width. `outline` is non-layout-affecting and preserves the Figma 310×216 frame and 262px inner content width exactly.
- **Pin root height explicitly**: when a dialog has a fixed Figma height, set `height` explicitly on the root rather than relying on auto height — auto height accumulates padding + content + border and can drift from the source.
- **Progress bar compression**: in a fixed-height flex column, always add `shrink-0` to the progress bar and `h-[N] shrink-0` to the label row to prevent flex compression from collapsing the bar.

## Deferred

- Pre-download default state
- Download-complete state
- Interactive download wiring (progress prop is static evidence only)
