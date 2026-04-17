# Trial: Component Family Definition — Dialog

> 试验版第二样本。用于验证 Component Family Definition 结构对多 axis、
> 结构分支、内容分支类组件的通用性。
> 参照 AIToolsRow 样本格式，回放验证 Figma / code / verify 三段。

---

## Family Boundary

**Family name:** Dialog  
**Root component:** `Dialog`（组合容器）  
**Sub-families（内部独立可复用）:**
- `CloseIcon` — 关闭按钮，4 variants
- `DialogButton` — 操作按钮，3 types × 2 states
- `ButtonGroup` — 按钮组合，3 layouts
- `DialogContent` — 内容区，3 variants

**Out of scope:**
- 遮罩层（overlay/backdrop）未在 Figma 中定义，不在 family 内
- 动画/过渡效果未在 Figma 中定义，不在 family 内

---

## Semantic Slots

### Dialog（根容器）

| Slot | Description |
|---|---|
| `content` | DialogContent 区域 |
| `buttons` | ButtonGroup 区域 |
| `container` | w-320px，rounded-24px，bg-white，border 0.5px，shadow |

### CloseIcon

| Slot | Description |
|---|---|
| `icon` | SVG 图标（default/hover/circle 三种资源） |
| `hit-area` | 32×32px 按钮容器 |

### DialogButton

| Slot | Description |
|---|---|
| `label` | 文字，14px，HYQiHei:60S |
| `container` | h-44px（solid/outline）/ h-24px（text），rounded-12px/8px |

### DialogContent

| Slot | Description |
|---|---|
| `title` | 20px，HYQiHei:75W |
| `description` | 16px，HYQiHei:60S |
| `image` | aspect-ratio 288/162，rounded-16px（仅 image variant） |
| `close` | CloseIcon 实例 |

---

## Axes

### Formal axes（Figma 中有正式定义）

| Axis | Component | Values |
|---|---|---|
| `variant` | CloseIcon | `default` \| `hover` \| `none` \| `circle` |
| `type` | DialogButton | `solid` \| `outline` \| `text` |
| `state` | DialogButton | `default` \| `hover` |
| `layout` | ButtonGroup / Dialog | `single` \| `vertical` \| `horizontal` |
| `contentVariant` | DialogContent / Dialog | `text` \| `title-left` \| `image` |

### Provisional axes

なし — Dialog は全 axis が Figma 正式定義から実装。provisional state は使用しなかった。

---

## Required States

| Component | State | Formal / Provisional |
|---|---|---|
| CloseIcon | default / hover / none / circle | formal（Figma component set に全 4 variants） |
| DialogButton | default / hover | formal（Figma component set に全 6 combos） |
| DialogContent | text / title-left / image | formal |
| ButtonGroup | single / vertical / horizontal | formal |

**特記:** Dialog は AIToolsRow と異なり、provisional state を一切使用しなかった。全実装が Figma 正式定義から導出。

---

## Visual Tokens

### DialogButton

| Type | State | bg | border | text |
|---|---|---|---|---|
| solid | default | `#1a1a1a` | — | white |
| solid | hover | `#333` | — | white |
| outline | default | transparent | `rgba(0,0,0,0.12)` | `var(--color-text-primary)` |
| outline | hover | `rgba(0,0,0,0.04)` | `rgba(0,0,0,0.12)` | `var(--color-text-primary)` |
| text | default | — | — | `var(--color-text-tertiary)` |
| text | hover | — | — | `var(--color-text-primary)` |

### Dialog container

| Property | Value |
|---|---|
| bg | white |
| border | `0.5px solid rgba(0,0,0,0.12)` |
| border-radius | 24px |
| shadow | `0px 10px 20px 0px rgba(100,106,112,0.15)` |
| width | 320px |

---

## Asset Slots

| Asset | File | Notes |
|---|---|---|
| CloseIcon default | `dialog-close-default@1x.svg` | `<img>` 可用（固定色，非 currentColor） |
| CloseIcon hover | `dialog-close-hover@1x.svg` | `<img>` 可用 |
| CloseIcon circle | `dialog-close-circle@1x.svg` | `<img>` 可用 |
| image placeholder | `dialog-image-placeholder@1x.png` | `<img>` 可用 |

**Asset rule:** CloseIcon は固定色 SVG のため `<img>` 使用可。currentColor 不要。
（AIToolsRow との違い：theme-reactive でないため inline SVG 不要）

---

## Promotion Rule

全 axis が formal 定義から実装済み。provisional state なし。
**昇格ゲートは存在しない** — 全 axes が既に formal。

---

## Code Prop API

```tsx
// CloseIcon
interface CloseIconProps {
  variant?: 'default' | 'hover' | 'none' | 'circle'
  onClick?: () => void
}

// DialogButton
interface DialogButtonProps {
  type?: 'solid' | 'outline' | 'text'
  label?: string
  onClick?: () => void
}
// hover state は内部 useState で管理

// ButtonGroup
interface ButtonGroupProps {
  layout?: 'single' | 'vertical' | 'horizontal'
  primaryLabel?: string
  secondaryLabel?: string
  onPrimary?: () => void
  onSecondary?: () => void
}

// DialogContent
interface DialogContentProps {
  variant?: 'text' | 'title-left' | 'image'
  title?: string
  description?: string
  imageSrc?: string
  onClose?: () => void
  closeVariant?: CloseIconVariant
}

// Dialog（root）
interface DialogProps {
  layout?: 'single' | 'vertical' | 'horizontal'
  contentVariant?: 'text' | 'title-left' | 'image'
  closeVariant?: CloseIconVariant
  title?: string
  description?: string
  imageSrc?: string
  primaryLabel?: string
  secondaryLabel?: string
  onClose?: () => void
  onPrimary?: () => void
  onSecondary?: () => void
}
// resolvedCloseVariant: closeVariant ?? (onClose ? 'default' : 'none')
```

---

## Verify Matrix

| Case | Component | Axis combo | Coverage |
|---|---|---|---|
| V1 | CloseIcon | variant=default | ✅ verified |
| V2 | CloseIcon | variant=hover | ✅ verified |
| V3 | CloseIcon | variant=none | ✅ verified |
| V4 | CloseIcon | variant=circle | ✅ verified |
| V5 | DialogButton | type=solid, state=default | ✅ verified |
| V6 | DialogButton | type=solid, state=hover | ✅ verified |
| V7 | DialogButton | type=outline, state=default | ✅ verified |
| V8 | DialogButton | type=outline, state=hover | ✅ verified |
| V9 | DialogButton | type=text, state=default | ✅ verified |
| V10 | DialogButton | type=text, state=hover | ✅ verified |
| V11 | ButtonGroup | layout=single | ✅ verified |
| V12 | ButtonGroup | layout=vertical | ✅ verified |
| V13 | ButtonGroup | layout=horizontal | ✅ verified |
| V14 | DialogContent | variant=text | ✅ verified |
| V15 | DialogContent | variant=title-left | ✅ verified |
| V16 | DialogContent | variant=image | ✅ verified |

**Coverage status:** visual-verification-complete（2026-04-16）

---

## Replay Validation

### 1. 能否解释 Figma provisional / formal 结构？

✅ 可以。
- Figma 中所有 sub-family 均有正式 component set（关闭 × 4、按钮 × 6、按钮组合 × 3、弹窗内容 × 3）
- Family Definition 的 formal axes 完整覆盖了 Figma 中的所有 variant 维度
- provisional axes 为空，与实际情况一致（Dialog case 未使用任何 provisional state）
- 这与 AIToolsRow 形成对比：AIToolsRow 有 provisional interaction axis，Dialog 没有

### 2. 能否映射到最终实现的 prop API / structural branches？

✅ 可以。
- `contentVariant` axis → `DialogContent` 内部 3 个 if 分支（text / title-left / image）
- `layout` axis → `ButtonGroup` 内部 3 个 if 分支（single / vertical / horizontal）
- `type` axis → `DialogButton` 内部 `styles` / `textStyles` record lookup
- `variant` axis（CloseIcon）→ 4 个 if 分支（none / circle / default+hover）
- `state` axis（DialogButton）→ 内部 `useState(hovered)`，不作为外部 prop
- Semantic slots 直接对应实现结构（content wrap / button wrap / close position）

### 3. 能否映射到最终 verify case / closeout 口径？

✅ 可以。
- Verify Matrix 16 个 case 与 INDEX.md 记录的"CloseIcon × 4、DialogButton × 6、ButtonGroup × 3、DialogContent × 3"完全对应
- 每个 axis combo 都有对应 verify case，无遗漏
- coverage status 与 INDEX.md closeout 记录一致

### 结论

三段全部通过。Dialog 作为多 axis、多结构分支、多内容分支的复合组件，同样能被一张 Family Definition 卡完整解释。

**与 AIToolsRow 的关键差异（验证通用性的核心数据点）：**
- AIToolsRow：有 provisional axis（interaction），promotion gate 存在
- Dialog：无 provisional axis，全 formal，promotion gate 不存在
- 两种情况 Family Definition 格式都能正确表达，说明格式有通用性

**建议：** 两个样本均通过，可以将 Component Family Definition 正式化为 `figma-create-design-system-rules` 的输出格式。
