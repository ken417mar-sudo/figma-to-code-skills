# Case 02: Explicit Component Variants

## Figma target

- File key: `iIbL9V4UrFeORPaM7KVji7`
- Board node: `1714:1024`
- Board name: `组件`

## Goal

Test the part of the workflow that comes after simple pattern detection:

- read explicit component boards
- validate whether variant axes are already well named
- verify whether a component is ready for normalization or already
  normalized
- identify what can be promoted directly into rule generation or library
  work

## Why this case matters

Case 01 proved that the workflow can detect repeated patterns from page
designs and propose candidate components.

Case 02 is different:

- this board already contains explicit component examples
- variant dimensions are already named in the canvas
- multiple states are laid out systematically

That makes it useful for testing the back half of component
normalization.

## High-value areas on this board

### 1. `页签`

- Container node: `1714:976`
- Variant samples:
  - `类型=新页签, 选中=未选中, 交互=默认`
  - `类型=新页签, 选中=选中, 交互=默认`
  - `类型=页签, 选中=未选中, 交互=默认`
  - `类型=页签, 选中=选中, 交互=默认`
  - `类型=新页签, 选中=未选中, 交互=悬停`
  - `类型=新页签, 选中=选中, 交互=悬停`
  - `类型=页签, 选中=未选中, 交互=悬停`
  - `类型=页签, 选中=选中, 交互=悬停`

This is strong evidence for a normalized component model with three axes:

- `类型`
- `选中`
- `交互`

The board provides a near-complete matrix for the visible states on this
component.

### 2. `关闭`

- Container node: `1714:1012`
- Variant samples:
  - `Hover=off`
  - `Hover=on`

This is a much smaller component, but it is still valuable because it
shows a clean two-state interaction axis.

### 3. `书签`

- Symbol node: `1714:971`

This appears to be a simpler standalone component sample with less
variant coverage. It is useful as a contrast against the more explicit
variantized components.

## What this case proves

### 1. The workflow can validate explicit variant naming

This board is strong enough to test whether our process can read
already-defined axes instead of trying to infer them from visual
differences.

For `页签`, the current board gives us explicit evidence that:

- `类型` is a real axis
- `选中` is a real axis
- `交互` is a real axis

That is significantly stronger than Case 01, where those dimensions had
to be inferred.

### 2. The workflow can distinguish “already normalized” from “needs normalization”

`页签` is no longer just a candidate component. It is effectively already
organized as a variant matrix.

That means the workflow should:

- stop treating it like a fuzzy repeated pattern
- recognize it as an explicit component board
- reuse the existing variant naming rather than inventing new axis names

### 3. The workflow can test rule capture from explicit components

This board is good enough to extract rules such as:

- tab sizing consistency
- selected vs unselected styling
- hover overlay behavior
- special treatment for `类型=页签` versus `类型=新页签`

### 4. The project shows real page-level reuse of component concepts

This is not just an isolated component playground.

Evidence from other boards in the same file:

- `网页结果页` (`1708:30204`) uses tab-like structures, `InputBox`, and
  assistant-side surfaces in a full page context.
- `侧边栏展开` (`1708:30337`) contains named symbols and instances such as
  `InputBox`, `AIToolsRow`, `Sidebar`, `Tab/Active`, and `Tab/Inactive`.

Practical meaning:

- explicit component work is already connected back to real screens
- this project is a better test bed for rule extraction than a pure
  component playground
- the workflow can start validating whether component naming and page
  usage stay aligned

### 5. The workflow can separate component-board quality from library readiness

This board is strong enough to validate a component and its axes, but that
does not automatically mean the whole project is ready for design-system
library generation.

Evidence gathered in this case:

- the variant structure for `页签` is explicit and strong
- the interaction axis for `关闭` is explicit and strong
- variable data on this board is still narrow (`浏览器kv`, `中性色/置灰`,
  `中性色/正文`)

Practical meaning:

- this is enough to support rule capture and component normalization
- this is not enough to prove full token-system readiness for broader
  library generation

## What is still missing

Even this board does not prove everything.

### 1. Full production rule coverage

The visible axes are strong, but this board alone does not guarantee:

- focus states
- disabled states
- pressed states
- keyboard interaction behavior
- content overflow behavior

### 2. Cross-component consistency

This board proves `页签` is well organized. It does not yet prove the same
quality level exists across the rest of the system.

### 3. Library readiness across the whole project

One good component board is not the same as a complete normalized design
system library.

### 4. Broader component coverage

The project gives us strong evidence for tabs and a small hoverable close
control, but it still does not prove that other major parts of the system
have equally explicit component coverage.

Examples that still look less explicit than `页签`:

- `InputBox`
- `AIToolsRow`
- assistant-side content blocks
- header action families

## New workflow capability unlocked by this case

Case 02 adds a capability that Case 01 could not fully support:

- validate explicit component-set intent
- validate variant-axis naming quality
- promote an existing component board into rule capture and later library
  work with much higher confidence

In short:

- Case 01 tests component discovery
- Case 02 tests explicit variant normalization

## Useful workflow implications

### For `figma-capture-design-system`

This board is strong enough to capture concrete statements like:

- `页签` has three visible axes: `类型`, `选中`, `交互`
- hover is treated as an explicit interaction axis
- small action icons like `关闭` already have their hover state modeled

### For `figma-create-design-system-rules`

This board is strong enough to move some rules from inferred to
confirmed, especially around:

- variant naming
- component state boundaries
- visual treatment differences between selected and unselected states

### For `figma-generate-library`

This board is the first kind of evidence that could justify library work,
because it already looks like component-set documentation rather than raw
screen design.

At the same time, it should be treated as a partial readiness signal, not
full readiness:

- component-variant structure looks strong
- token coverage still looks limited
- a broader component board would still be needed before treating the
  project as fully library-ready

## Overall project value for the workflow

This project is stronger than Case 01 in three ways:

1. it contains real pages, not only a single flat screen
2. it contains an explicit component board with named variant axes
3. it shows page-level reuse of component concepts

That makes it a good intermediate test project between:

- messy page-only drafts
- and a truly mature design-system library

## Confirmed rules extractable from this board

These can be treated as strong candidates for confirmed or nearly
confirmed rules, pending human review:

- `页签` uses an explicit three-axis model:
  - `类型`
  - `选中`
  - `交互`
- hover is modeled as a first-class interaction axis, not as an ad hoc
  visual note
- selected tabs use a stronger active container treatment than
  unselected tabs
- `类型=页签` includes a divider treatment that does not appear on every
  tab variant
- small dismiss or close controls can also carry their own hover axis

## New gotcha surfaced in this case

### Code Connect context access may be plan-limited

Attempting to use `get_context_for_code_connect` on this board returned a
plan or seat restriction rather than component metadata.

Implication:

- the workflow must not assume Code Connect context tools are available
- explicit variant boards should still be readable through metadata and
  design context alone
- a missing Developer seat should be treated as an environment limitation,
  not as absence of component structure

## Best next test after this case

The next most valuable test file would be one of these:

- a fuller component page with focus, disabled, and pressed states
- a form component board with input validation states
- a card or list component board showing density and content-amount
  variants
- a project where multiple components are already documented this way, so
  we can test broader library-readiness rather than one strong example
