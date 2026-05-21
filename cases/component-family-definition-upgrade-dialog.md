# Component Family Definition — UpgradeDialog

## Status

`closed` — 3 variants verified + 1 inferred. agentic-browser-ui PRs #22, #23 merged; #27 (geometry/layout/framing fix) pending merge.

**Phase K note:** PR #22 was implemented from a scaled instance `2080:7977` (310×216, rounded-16, outline). Phase L (PR #23) corrected to the formal component set source. PR #27 fixed state-specific radius regression (升级前 rounded-16, others rounded-12), added pt-6 for non-升级前 states, corrected success/failure button structure (content flex-1 + button shrink-0 sibling), and fixed logo/triangle asset framing (Figma inset wrappers).

## Source

- Figma file: `iIbL9V4UrFeORPaM7KVji7`
- Canonical source: `2080:40359` — 升级弹窗 component set, 联想规范 page
- Phase K source (deprecated): `2080:7977` — scaled instance in 顶栏 board, 310×216

## Scope

UpgradeDialog covers 4 variants from the formal component set:

- `升级前` (320×356): logo 40px + version row + changelog + restart button
- `升级中` (320×222): logo 96px + progress bar (正在升级中)
- `升级成功` (320×222): logo + success text + restart button (hidden layer — inferred from structure)
- `升级失败` (320×222): warning icon composite (circle + triangle + exclamation) + retry button

**Component boundary:** distinct from `Dialog.tsx` — different border (`border-[0.5px] rgba(0,0,0,0.08)` + shadow vs `outline`), different radius (`12px` vs `24px`).

## Implementation

- File: `agentic-browser-ui/src/components/UpgradeDialog.tsx`
- Verify surface: `agentic-browser-ui/src/App.tsx` UpgradeDialog verify cards
- PRs: agentic-browser-ui #22 (Phase K), #23 (Phase L), #27 (geometry/layout/framing fix); figma-to-code-skills #57, #60, #64
- Exported assets (6): `upgrade-logo`, `upgrade-version-logo`, `upgrade-version-logo-mask`, `upgrade-fail-circle`, `upgrade-fail-triangle`, `upgrade-fail-exclaim`

## Component Axes

| Axis | Values | Definition status |
|---|---|---|
| state | `升级前` \| `升级中` \| `升级成功` \| `升级失败` | prop-driven |
| progress | 0–100 | prop-driven (升级中 only) |
| onRestart | callback | prop-driven (升级前 / 升级成功) |
| onRetry | callback | prop-driven (升级失败) |

## Geometry

### Shared root
| Property | Value |
|---|---|
| root | `320 × 356` (升级前) / `320 × 222` (升级中/成功/失败) |
| border radius | `16px` (升级前) / `12px` (升级中/成功/失败) |
| border | `0.5px solid rgba(0,0,0,0.08)` |
| shadow | `0px 4px 30px 0px rgba(0,0,0,0.1)` |
| padding | `px-[24px] pb-[24px]`; `pt-[6px]` for 升级中/成功/失败; 升级前 has no explicit pt (top spacing from user_id row `py-[16px]`) |

### 升级前 (320×356)
| Property | Value |
|---|---|
| logo slot | `40 × 40` |
| version row | logo-mask + version text, `137.9 × 14` logo |
| changelog | scrollable text area |
| restart button | `w-full h-[32px]`, `rounded-[8px]`, `bg-black` |

### 升级中 (320×222)
| Property | Value |
|---|---|
| logo slot | `96 × 96`, centered |
| progress bar track | `271 × 8` (browser-measured; Figma spec 272, 1px tolerance under 0.5px border), `rounded-[24px]`, `#d7d7db` |
| progress bar fill | CSS `width: {progress}%`, `#18181b`, `rounded-[24px]`, `shrink-0` |

### 升级失败 (320×222)
| Property | Value |
|---|---|
| warning icon slot | `60 × 60`, composite of 3 SVG layers |
| circle background | `upgrade-fail-circle`, fill `#FDE8E8`, viewBox `0 0 60 60` |
| triangle | `upgrade-fail-triangle`, warning slot `53 × 53` at `left:3 top:4`; inner vector inset `9.43% 3.77% 11.32% 3.77%` → rendered frame ~49×42, fill `#EF4444` |
| exclamation | `upgrade-fail-exclaim`, `15.1% × 39.82%` of triangle slot |
| retry button | `w-full h-[32px]`, `rounded-[8px]`, `bg-black` |

## Verification Status

| Check | Status |
|---|---|
| Figma design context | passed: component set `2080:40359` inspected; 升级前/升级中/升级失败 visible; 升级成功 hidden/inferred |
| Asset inventory | passed: 6 assets exported and recorded in slices-name-map.json |
| State-geometry scan | passed: Phase K geometry corrected (310→320, 216→222/356, outline→border+shadow); PR #27 corrected radius (升级前 r16, others r12), pt-6 for non-升级前, button structure (content flex-1 + button shrink-0), logo inset (7.5%/7.57%), triangle inset (9.43%/3.77%/11.32%/3.77%) |
| Build | passed: `npm run build` |
| Lint | passed: `npm run lint` |
| git diff --check | passed |
| Codex P2 review | passed: upgrade-fail-circle SVG empty group fixed (circle cx=30 cy=30 r=30 fill=#FDE8E8) |
| DOM evidence (升级前) | bundle: `borderRadius:u?16:12` ✓, `paddingTop:u?0:6` ✓, `shadow 4px 30px` ✓; logo slot 40×40, inner glyph ~33.95×34 (7.5%/7.57% inset) |
| DOM evidence (升级中) | logo slot 96×96, inner glyph ~81.47×81.61; progress track 271×8 at y≈189.5; button not present in this state |
| DOM evidence (升级失败) | content flex-1 + button shrink-0 sibling; warning outer 60×60 at y≈38; triangle frame ~49×42 (Figma inset 9.43%/3.77%/11.32%/3.77%); button y≈165.5 h=32, bottom gap≈24.5px |
| DOM evidence (升级成功) | inferred only — hidden Figma layer; button structure mirrors 升级失败 (content flex-1 + button shrink-0) |

## Durable Lessons

- **Outline for exact-size dialog surfaces**: use `outline` instead of `border` when the Figma source specifies an exact frame size. `border` participates in layout under `border-box` sizing and shifts both root height and inner content width. `outline` is non-layout-affecting. *(Phase K lesson — corrected in Phase L to border+shadow per formal source.)*
- **Pin root height explicitly**: when a dialog has a fixed Figma height, set `height` explicitly on the root rather than relying on auto height.
- **Progress bar compression**: in a fixed-height flex column, always add `shrink-0` to the progress bar and `h-[N] shrink-0` to the label row to prevent flex compression.
- **State-specific border radius**: multi-variant dialogs may have different radii per state. Always check each variant's root class in Figma design context — do not assume a single radius applies globally. 升级前 is `rounded-[16px]`; 升级中/成功/失败 are `rounded-[12px]`.
- **Instance-context vs canonical component-set source**: a scaled instance in a board (e.g. 310×216 in 顶栏) may differ from the formal component set (320×222/356 in 联想规范). Always preflight the canonical component set before implementing. Phase K was derived from an instance; Phase L corrected from the formal source.
- **Hidden variant handling**: hidden Figma variants (e.g. 升级成功 `2080:40415`) return blank renders from get_design_context and get_screenshot. Infer structure from sibling variants and metadata; document as inferred in case card.
- **Empty SVG export from ellipse nodes**: Figma ellipse nodes can export as empty SVG groups. Detect by checking for missing path/circle elements. Fix by pixel-sampling the rendered screenshot to confirm fill color, then hand-authoring the circle element with correct viewBox.

## Deferred

- `升级成功` variant: hidden layer, structure inferred from siblings. Needs visual confirmation when Figma layer becomes visible.
- `upgrade-version-logo-mask`: mask-alpha effect deferred; current impl renders logo directly without mask.
- Interactive wiring (progress prop is static evidence only).
