# Trial: Component Family Definition — AIToolsRow

> 试验版。用于回放验证 Component Family Definition 结构是否能作为
> Figma / code / verify 三段的共同锚点。
> 如果验证通过，此格式将正式化为 `figma-create-design-system-rules` 的输出格式。

---

## Family Boundary

**Family name:** ToolPill  
**Container:** AIToolsRow（行级容器，不属于 ToolPill family 本身）  
**Variants in family:**
- `text` — icon + label，flex-1 自适应宽度
- `icon-only` — 仅 icon，固定宽度（更多按钮）

**Out of scope:**
- AIToolsRow 行容器本身不是 ToolPill family 成员
- 未来可能的 disabled 状态尚未在 Figma 中出现，不在当前 family 内

---

## Semantic Slots

| Slot | text variant | icon-only variant |
|---|---|---|
| `icon` | 16×16 SVG，currentColor | 24×24 SVG，currentColor |
| `label` | 12px 文字，HYQiHei:60S | — （无 label） |
| `container` | flex-1，h-40px，px-12px，rounded-99px | w-64px fixed，h-40px，rounded-99px |

---

## Axes

### Formal axes（Figma 中有正式定义）

| Axis | Values |
|---|---|
| `variant` | `text` \| `icon-only` |

### Provisional axes（用户确认但 Figma 中无正式组件）

| Axis | Values | Status |
|---|---|---|
| `interaction` | `default` \| `hover` \| `active` | hover 已确认；active 为 proposal-level |

---

## Required States

| State | Formal / Provisional | Notes |
|---|---|---|
| default | formal | Figma source 中有正式定义 |
| hover | provisional-confirmed | 用户确认，provisional board 已建 |
| active | provisional-proposal | 用户确认方向，但未正式 sign-off |

---

## Visual Tokens per State

| State | border | background | shadow |
|---|---|---|---|
| default | `rgba(0,0,0,0.12)` 0.5px | transparent | `0px 0px 24px 0px rgba(10,88,245,0.02)` |
| hover | `rgba(0,0,0,0.20)` 0.5px | `rgba(0,0,0,0.04)` | same |
| active | `rgba(0,0,0,0.28)` 0.5px | `rgba(0,0,0,0.08)` | same |

Text color: `var(--color-text-primary)` / `#333`

---

## Asset Slots

| Asset | File | Notes |
|---|---|---|
| 视频编辑 icon | `aitoolsrow-video@1x.svg` | fill=currentColor |
| 定时任务 icon | `aitoolsrow-schedule@1x.svg` | fill=currentColor |
| 技能和工作流 icon | `aitoolsrow-skill@1x.svg` | BOOLEAN_OPERATION → stroke=currentColor fill=none |
| 个人知识库 icon | `aitoolsrow-knowledge@1x.svg` | fill=currentColor |
| 更多 icon | `aitoolsrow-more@1x.svg` | fill=currentColor |

**Asset rule:** 所有 icon 必须以 inline SVG + currentColor 实现，不得用 `<img src>` 引用。

---

## Promotion Rule

- `variant` axis 已 formal，可保持
- `interaction` axis 中 `active` 仍为 proposal-level
- **当前不可升格为正式 Figma component set**，直到 `active` 状态经用户正式 sign-off

---

## Code Prop API

```tsx
// ToolPill (text)
interface ToolPillProps {
  icon: React.ReactNode   // inline SVG component
  label: string
  onClick?: () => void
}

// ToolPill (icon-only)
interface ToolPillIconOnlyProps {
  icon: React.ReactNode
  label?: string          // aria-label fallback
  onClick?: () => void
}

// AIToolsRow (container)
interface AIToolsRowProps {
  onToolClick?: (label: string) => void
  onMoreClick?: () => void
}
```

Interaction state 通过 `useState` 管理（hovered / active），不作为外部 prop 暴露。

---

## Verify Matrix

| Case | Variant | State | Coverage |
|---|---|---|---|
| V1 | text | default | ✅ verified |
| V2 | text | hover | ✅ verified |
| V3 | text | active | ✅ verified |
| V4 | icon-only | default | ✅ verified |
| V5 | icon-only | hover | ✅ verified |
| V6 | icon-only | active | ✅ verified |

**Verify surface:** 704px（Figma source-of-truth 原始宽度）  
**Coverage status:** visual-verification-complete（2026-04-17）

---

## Replay Validation

回放验证三个问题：

### 1. 能否解释 Figma provisional / formal 结构？

✅ 可以。
- Figma 中只有 default 状态有正式组件定义
- hover / active 在 provisional board 中以独立 frame 存在（control 级别，非 row 级别）
- Family Definition 的 formal/provisional axis 区分正确映射了这个结构
- `active` 的 proposal-level 标注也准确反映了当时的状态

### 2. 能否映射到最终实现的 prop API / structural branches？

✅ 可以。
- `variant` axis → `ToolPill` vs `ToolPillIconOnly` 两个组件
- `interaction` axis → 组件内部 `useState(hovered/active)`，不作为外部 prop
- Semantic slots → icon/label/container 直接对应实现结构
- Asset slots → 5 个 SVG 文件，inline SVG 规则已执行

### 3. 能否映射到最终 verify case / closeout 口径？

✅ 可以。
- Verify Matrix 的 6 个 case 与实际验证覆盖完全对应
- Verify surface 704px 规则在 Family Definition 中有明确记录
- Coverage status 与 INDEX.md 的 closeout 记录一致

### 结论

三段都能被同一张卡解释。Component Family Definition 结构有真实解释力，不是新文档负担。

**建议下一步：** 用 InputBox 或 Dialog 做第二样本验证通用性。
