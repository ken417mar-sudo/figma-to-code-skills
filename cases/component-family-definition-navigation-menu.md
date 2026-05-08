# Component Family Definition — NavigationMenu

## Status

`in-progress` — implementation complete, visual verification pending

## Source

- Figma file: `iIbL9V4UrFeORPaM7KVji7`
- Source node: `2080:42251` (TabMenu 区域，联想规范页 `925:13013`)
- Component name in Figma: NavMenu / 导航菜单

## Scope

Pill-style horizontal navigation menu. Supports 3–10 items with a selected
state, optional overflow "more" button. Right-side control button (管理)
is out of scope for this case — not used in agentic-browser-ui.

## Implementation

- File: `agentic-browser-ui/src/components/NavigationMenu.tsx`
- Branch: `feature/navigation-menu`
- Exported asset: `src/assets/figma/nav-more-icon@1x.svg` (icon/更多, from design context)

## Component Axes

### NavOptionItem

| Axis | Values |
|---|---|
| state | Normal, Selected |

- Normal: `bg-white border-[0.5px] border-[rgba(0,0,0,0.1)] text-[#18181b]`
- Selected: `bg-[#18181b] text-white border-transparent`
- Geometry rule: `border-[0.5px]` reserved in all states (transparent when selected) — no layout shift on state change
- Padding: `px-[16px] py-[5px]`, radius: `rounded-[12px]`, text: `14px / 22px HYQiHei:60S`

### MoreButton

- Shown when `showMore=true`
- Same pill geometry as Normal NavOptionItem
- Icon: `nav-more-icon@1x.svg` (15×3px three-dot, `currentColor`)
- Icon container: `size-[18px]` wrapper, icon `w-[15px] h-[3px]`

### NavigationMenu (container)

- `gap-[12px]` between items
- `flex items-center justify-between` outer layout

## Verification Status

| Check | Status |
|---|---|
| Build passes (tsc + vite) | ✓ |
| Selected pill geometry stable (no layout shift) | ✓ rule applied |
| MoreButton uses exported asset | ✓ |
| Visual match vs Figma screenshot | pending |
| DOM geometry measurement | pending |

## Deferred

- Right-side 管理/control button (not in agentic-browser-ui scope)
- Hover/pressed states (not shown in formal Figma spec node)
- Overflow scroll behavior for > 10 items
