# Component Family Definition — Sidebar

> composite family  
> definition produced: 2026-04-17  
> status: controlled trial-run (pre-implementation)

---

## Family Boundary

**Family name:** Sidebar  
**Family type:** composite  
**Root component:** `Sidebar`（240×816px 독립 컴포넌트）  
**Sub-families（각자 독립 복용/검증 가능）:**
- `SidebarHeader` — 타이틀 + collapse 버튼
- `QuickActionItem` — 빠른 실행 항목 (icon + label)
- `ProjectItem` — 프로젝트 항목 (icon + label)
- `HistoryItem` — 히스토리 항목 (text + optional more button)
- `SectionHeader` — 섹션 레이블 (Projects / History)
- `UserInfo` — 하단 아바타 영역

**Out of scope:**
- Sidebar collapsed 상태 — 이 보드에 없음, 별도 확인 필요
- Toolbar / TabBar / WindowBody — Sidebar 외부 레이아웃, 별도 컴포넌트
- AIToolsRow / InputBox — 이미 closed case

---

## Semantic Slots

### Sidebar (root)

| Slot | Description |
|---|---|
| `header` | SidebarHeader 영역 |
| `list` | QuickActions + Projects + History 섹션 |
| `userInfo` | 하단 UserInfo 영역 |
| `container` | w-240px, h-816px, bg rgba(0,0,0,0.02), border-r 0.5px rgba(0,0,0,0.08) |

### QuickActionItem / ProjectItem

| Slot | Description |
|---|---|
| `icon` | 16×16 SVG, iconWrap 24×24px (p-4px) |
| `label` | 14px, PICO Sans VFE SC Regular, leading-20px |
| `container` | w-216px, h-40px, px-8px py-5px, rounded-12px |

### HistoryItem

| Slot | Description |
|---|---|
| `text` | 14px, PICO Sans Regular, truncate |
| `moreButton` | 우측 more 버튼 (hover 시 노출 여부 미확인) |
| `container` | w-216px, h-40px, px-12px py-8px, rounded-12px |

### SectionHeader

| Slot | Description |
|---|---|
| `label` | 14px, HYQiHei:55S, color #999 |
| `actionButton` | 우측 + 버튼 (Projects 섹션만) |
| `container` | w-full, h-28px, px-12px py-2px |

---

## Axes

### Formal axes（Figma에 정식 정의）

| Axis | Component | Values | definition_status |
|---|---|---|---|
| `variant` | Sidebar | `expanded` | formal |

### Provisional axes（미확인 — 확인 필요）

| Axis | Component | Values | definition_status | 비고 |
|---|---|---|---|---|
| `interaction` | QuickActionItem | `default` \| `hover` \| `active` | **미확인** | Figma에 default만 존재 |
| `interaction` | ProjectItem | `default` \| `hover` \| `active` | **미확인** | 동상 |
| `interaction` | HistoryItem | `default` \| `hover` \| `active` | **미확인** | hover 시 more 버튼 노출 여부도 미확인 |
| `collapsed` | Sidebar | `expanded` \| `collapsed` | **미확인** | collapsed 보드 없음 |

---

## Required States

| Component | State | definition_status | verification_status |
|---|---|---|---|
| Sidebar | expanded | formal | not-covered |
| QuickActionItem | default | formal | not-covered |
| QuickActionItem | hover | **미확인** | not-covered |
| QuickActionItem | active | **미확인** | not-covered |
| ProjectItem | default | formal | not-covered |
| ProjectItem | hover | **미확인** | not-covered |
| HistoryItem | default | formal | not-covered |
| HistoryItem | hover | **미확인** | not-covered |
| SidebarHeader | default | formal | not-covered |
| UserInfo | default | formal | not-covered |

---

## Visual Tokens

### Sidebar container

| Property | Value |
|---|---|
| width | 240px |
| height | 816px |
| bg | `rgba(0,0,0,0.02)` |
| border-right | `0.5px solid rgba(0,0,0,0.08)` |
| padding | `px-8px` |

### QuickActionItem / ProjectItem (default)

| Property | Value |
|---|---|
| height | 40px |
| padding | `px-8px py-5px` |
| border-radius | 12px |
| bg | transparent |
| label font | PICO Sans VFE SC Regular, 14px, #333 |

### HistoryItem (default)

| Property | Value |
|---|---|
| height | 40px |
| padding | `px-12px py-8px` |
| border-radius | 12px |
| bg | transparent |
| text font | PICO Sans Regular, 14px, #333, truncate |

### SectionHeader

| Property | Value |
|---|---|
| height | 28px |
| padding | `pl-12px pr-4px py-2px` |
| label | HYQiHei:55S, 14px, #999 |

---

## Asset Slots

| Asset | Node name | Notes |
|---|---|---|
| icon-sidebar-collapse | `icon-sidebar-collapse` | export 필요 |
| icon-new-task | `icon-new-task` | export 필요 |
| icon-auto-run | `icon-auto-run` | export 필요 |
| icon-skills | `icon-skills` | export 필요 |
| icon-project | `icon-project` | export 필요 |
| icon-avatar | `icon-avatar` | export 필요 |
| icon-add (+ button) | `icon-add` | export 필요 |

**Asset rule:** theme-reactive 여부 미확인. export 후 SVG 구조 확인 필요.

---

## Promotion Rule

- `variant` axis (expanded): formal, 승격 가능
- `interaction` axis (QuickActionItem / ProjectItem / HistoryItem): **미확인** — 사용자 확인 후 provisional-confirmed로 승격 가능
- `collapsed` axis: **미확인** — Figma에 collapsed 보드 없음, 확인 필요
- **현재 승격 불가** — interaction states 미확인 상태

---

## Confirm Required (구현 전 확인 필요)

다음 항목을 확인한 후 구현을 시작합니다:

1. **QuickActionItem / ProjectItem hover + active** — 필요한가? 토큰은?
   - 제안: AIToolsRow ToolPill과 동일한 패턴 (`rgba(0,0,0,0.04)` hover / `rgba(0,0,0,0.08)` active)
   
2. **HistoryItem hover** — hover 시 우측 more 버튼 노출되는가?
   - 제안: hover 시 bg `rgba(0,0,0,0.04)` + more 버튼 노출

3. **Sidebar collapsed 상태** — 이번 case에 포함하는가?
   - 제안: 이번 case는 expanded만, collapsed는 별도 case로 분리

4. **UserInfo** — 클릭 가능한가? hover 상태 있는가?
   - 제안: 이번 case는 static으로 구현

---

## Verify Matrix

> verified: 2026-04-17 by Claude Code

| Case | Component | Axis combo | definition_status | verification_status | notes |
|---|---|---|---|---|---|
| V1 | Sidebar | expanded | formal | **passed** | 240×816, bg/border/padding 全部对齐 |
| V2 | QuickActionItem | default | formal | **passed** | 216×40, icon 16px, font/leading 对齐 |
| V3 | QuickActionItem | hover | TBD | not-covered | provisional 未确认，scope 外 |
| V4 | QuickActionItem | active | TBD | not-covered | provisional 未确认，scope 外 |
| V5 | ProjectItem | default | formal | **passed** | 与 QuickActionItem 同结构，对齐 |
| V6 | ProjectItem | hover | TBD | not-covered | provisional 未确认，scope 外 |
| V7 | HistoryItem | default | formal | **passed** | 216×40, PICO Sans + font-feature-settings 对齐 |
| V8 | HistoryItem | hover | TBD | not-covered | provisional 未确认，scope 外 |
| V9 | SidebarHeader | default | formal | **passed** | padding fix 后对齐（Projects: pl-12 pr-4，History: px-12） |
| V10 | UserInfo | default | formal | **passed** | border/avatar 尺寸对齐 |

### Open items（不阻塞 formal pass）

- SVG 图标颜色硬编码（`#333333` / `#999999`）——theme-reactive 未确认，待决策
- Provisional states（V3/V4/V6/V8）——需用户确认后才能进入 scope
