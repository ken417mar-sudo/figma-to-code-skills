# Component Family Definition — WorkspacePage

> composite family  
> definition produced: 2026-04-21  
> last updated: 2026-04-21

---

## Family Boundary

**Family name:** `WorkspacePage`  
**Family type:** composite  
**Figma source:** `2025:11950` (`默认`)  
**Sub-families:**
- `TaskChatPanel` — left chat + task-launch surface (400px)
- `WorkspaceSidebar` — narrow icon sidebar (48px) — already implemented, reuse
- `TitleBar` — macOS-style title bar with traffic lights (448×40)
- `WorkspaceToolbar` — right-side view switcher + actions (1144×40)

**Root card scope:** page-level composition, layout split, canonical naming,
and binding of sub-families into the full workspace shell.

**Out of scope:**
- hover / active states on toolbar icons
- sidebar expand / collapse interaction
- workspace preview content (wallpaper only in this board)
- chat message interaction states
- collapsed or alternate layout variants

---

## Naming Normalization

| Raw Figma node | Node ID | Canonical name | Role |
|---|---|---|---|
| `默认` | `2025:11950` | `WorkspacePage` | page root |
| `窗口区` | `2025:11951` | `WorkspacePage/Window` | window shell |
| `工具栏` (left, 448×40) | `2025:12363` | `TitleBar` | macOS title bar |
| `控制栏` | `2025:12375` | `TitleBar/Controls` | traffic lights + collapse |
| `系统` | `2025:12376` | `TitleBar/TrafficLights` | red/yellow/green dots |
| `工具栏` (right, 1144×40) | `2025:11955` | `WorkspaceToolbar` | view switcher + actions |
| `功能` (inside WorkspaceToolbar) | `2025:11956` | `WorkspaceToolbar/ViewSwitcher` | PC/手机/自定义 |
| `更多` | `2025:11973` | `WorkspaceToolbar/Actions` | 书签 + More |
| `内容区` | `2025:12004` | `WorkspacePage/Content` | three-column content area |
| `Sidebar` | `2025:12005` | `WorkspaceSidebar` | existing component, reuse |
| `对话区` | `2025:12085` | `TaskChatPanel` | child family card |
| `环境` | `2025:12361` | `WorkspacePreview` | wallpaper, no component needed |

Naming rule for this case:
- use `Workspace*` for page-shell and right-side containers
- use `TaskChat*` for the left chat panel and its internals
- keep reused families (`WorkspaceSidebar`, `InputBox`) under their established names

---

## Semantic Slots

| Slot | Description |
|---|---|
| `titleBar` | macOS window chrome, traffic lights, 448×40 |
| `workspaceToolbar` | right-side view switcher + bookmark + more, 1144×40 |
| `sidebar` | narrow icon sidebar, 48×852, reuses `WorkspaceSidebar` |
| `chatPanel` | task chat + input surface, 400×852, child family `TaskChatPanel` |
| `workspacePreview` | environment / wallpaper area, 1144×852 |

---

## Axes

### Formal axes

| Axis | Values | definition_status |
|---|---|---|
| `layout` | `default` (sidebar + chat + preview) | formal |
| `workspacePreview` | `wallpaper` | formal |

### Provisional axes

| Axis | Values | definition_status |
|---|---|---|
| `sidebar` | `collapsed` | provisional-proposal |
| `workspacePreview` | `app / web / mobile` | provisional-proposal |

---

## Required States

| Component | State / Value | definition_status | verification_status |
|---|---|---|---|
| `WorkspacePage` | `layout=default` | formal | pending |
| `TitleBar` | `default` | formal | pending |
| `WorkspaceToolbar` | `default` | formal | pending |
| `WorkspaceSidebar` | `default` | formal | coverage-complete (Phase 4) |
| `TaskChatPanel` | `default` (analysis in progress) | formal | pending |
| `WorkspacePreview` | `wallpaper` | formal | pending |

---

## Visual Tokens

### Page shell

| Property | Value |
|---|---|
| page size | `1600 × 900` |
| window shell | `1592 × 892`, inset `4px` |
| app background | `--color-surface-app-bg` (`#ebeef5`) |
| layout split | TitleBar+WorkspaceToolbar `40px` top / content `852px` |
| column split | sidebar `48px` + chat `400px` + preview `1144px` |

### TitleBar

| Property | Value |
|---|---|
| size | `448 × 40` |
| traffic light dot size | `14 × 14` |
| traffic light gap | `22px` between centers |
| traffic light x offset | `8px` from left edge |
| traffic light y offset | `13px` from top |

### WorkspaceToolbar

| Property | Value |
|---|---|
| size | `1144 × 40` |
| view switcher icons | `24 × 24`, gap `8px`, x offset `8px` |
| actions cluster x offset | `1062px` from toolbar left |
| divider | `2px` wide, `8px` height, centered vertically |
| bookmark icon | `24 × 24` |
| More icon | `24 × 24` |

---

## Asset Slots

| Asset | Naming convention | Notes |
|---|---|---|
| PC view icon | `workspacetoolbar-desktop@1x.svg` | `2025:11957` |
| Mobile view icon | `workspacetoolbar-mobile@1x.svg` | `2025:11962` |
| Custom view icon | `workspacetoolbar-custom@1x.svg` | `2025:11966` |
| Bookmark icon | `workspacetoolbar-bookmark@1x.svg` | `2025:11978` |
| More icon | `workspacetoolbar-more@1x.svg` | `2025:11984` |
| Wallpaper | `workspacepreview-wallpaper@1x.png` | `2025:12362` instance |

---

## Promotion Rule

- Do not promote `sidebar=collapsed` or `workspacePreview=app/web/mobile`
  until a dedicated board or explicit user confirmation exists.
- `WorkspaceSidebar` is already formal — do not re-verify its internal states.

---

## Code Prop API

```ts
interface WorkspacePageProps {
  sidebarState?: 'expanded' | 'collapsed'
  workspacePreviewContent?: ReactNode
  chatPanelContent?: ReactNode
}
```

---

## Verify Matrix

| Case | Component | Axis combo | definition_status | verification_status |
|---|---|---|---|---|
| V1 | `WorkspacePage` | `layout=default` | formal | pending |
| V2 | `TitleBar` | `default` | formal | pending |
| V3 | `WorkspaceToolbar` | `default` | formal | pending |
| V4 | `TaskChatPanel` | `default` (analysis in progress) | formal | pending |
