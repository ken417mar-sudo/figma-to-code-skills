# Case 01: Component Normalization Front-Half

## Figma target

- File key: `iIbL9V4UrFeORPaM7KVji7`
- Node: `1708:30119`
- Frame name: `首页`

## Goal

Test how far the current Phase 1 workflow can go on the front half of
component normalization:

- detect repeated UI patterns
- identify likely component candidates
- propose probable variant or state relationships
- mark unresolved dimensions instead of over-normalizing

This case is not meant to prove full library generation.

## Skills exercised

- `figma`
- `figma-capture-design-system`
- `figma-create-design-system-rules`
- `figma-implement-design`
- `figma-verify-implementation`

Supporting smoke coverage had already been done separately for:

- `figma-use`
- `figma-ai-implementation-cleanup`

## Useful evidence in this file

### Strong normalization candidates

#### 1. Tabs

- `Tab/Active` (`1708:30194`)
- `Tab/Inactive` (`1708:30195`)

Why this is strong:

- same footprint and outer shell
- adjacent usage inside `TabBar/Tabs`
- same conceptual content slot
- obvious visual state difference

Probable normalization result:

- one `Tab` component
- at least one axis like `state=active|inactive`

What is still missing:

- more state coverage beyond the two visible tab states
- confirmation of canonical variant naming

#### 2. AI tools pills

- `AIToolsRow` (`1708:30180`)

Why this is strong:

- repeated `40px` pill structure
- repeated icon + text composition
- repeated border, radius, and shadow treatment
- one trailing compact `more` pill that looks related

Probable normalization result:

- one chip or quick-action component family
- likely text pill plus compact/more variant, or a close sibling pattern

What is still missing:

- explicit confirmation whether the compact `more` pill belongs to the
  same component set
- state coverage such as hover, selected, disabled

#### 3. Icon buttons

- toolbar nav icons
- sidebar icon buttons

Why this is strong:

- repeated `24px` button shell
- repeated centered `16px` icon treatment
- consistent spatial structure

Probable normalization result:

- one icon-button primitive
- usage-specific variants or icon slots layered on top

What is still missing:

- evidence for full interaction state model
- confirmation of whether toolbar and sidebar share one primitive or only
  happen to look similar in this file

### Likely component candidates, but not enough evidence yet

#### 1. InputBox

- `InputBox` (`1708:30179`)

Why it matters:

- clearly a reusable composite block
- contains a prompt field area plus accessory actions

Why it is not fully normalizable yet:

- only one visible state
- no evidence for focus, typing, disabled, loading, or error states
- no proof yet of which subparts are slots versus fixed composition

#### 2. Header action family

- `BookmarkButton`
- `MoreButton`
- `ChatButton`

Why it is interesting:

- they appear as a coordinated right-side action cluster

Why it is unresolved:

- too little visible variation to determine whether these are:
  - one family with variants
  - several separate components
  - one-off actions sharing only layout alignment

#### 3. Window controls

- close / minimize / fullscreen dots

Why they should stay low-priority:

- repeated visually, but likely system chrome rather than a project-level
  reusable component target

## What this file can prove

- Phase 1 can identify repeated patterns confidently enough to propose
  component candidates.
- Phase 1 can separate strong candidates from weak candidates.
- Phase 1 can suggest likely state or variant relationships.
- Phase 1 can mark unresolved axes instead of inventing a fake component
  model.

## What this file cannot prove

- full state coverage for reusable components
- canonical variant-property naming
- cross-page reuse evidence
- whether similar blocks should become one component set or multiple
  sibling components
- production-ready library normalization

## Practical workflow conclusion

This file is good enough for the front half of component normalization,
but not the back half.

Meaning:

- use it to test detection, grouping, and provisional rule extraction
- do not use it alone to claim that component normalization is solved
- do not promote its candidates straight into a formal library without
  more design evidence

## Best next Figma test file

To push this workflow further, the most valuable next file would contain:

- one page or section with the same component shown in multiple states
- clearer component-set intent
- more explicit variant dimensions
- evidence across more than one screen or usage context

Good examples:

- button states page
- input states page
- tabs, chips, or cards shown as a component set
- a design-system page with named variants and properties
