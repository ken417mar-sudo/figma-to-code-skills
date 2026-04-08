# Case 04: Candidate Foundations From Agentic Browser

## Figma target

- File key: `iIbL9V4UrFeORPaM7KVji7`
- Sampled nodes:
  - `1714:976` (`页签`)
  - `1714:1012` (`关闭`)
  - `1714:971` (`书签`)
  - `1708:30342` (`InputBox`)
  - `1708:30119` (`首页`)
  - `1708:30337` (`侧边栏展开`)

## Goal

Draft a first-pass candidate list for Figma foundations:

- `Variables`
- reusable `样式`

This pass is intentionally conservative. It identifies what looks stable
enough to promote, and what still needs human semantic confirmation.

## Current file state

This case now has two phases.

### Phase A: before the provisional foundations pass

At the first inspection, this file did **not** have local:

- variable collections
- paint styles
- text styles
- effect styles

Practical meaning:

- any foundation promotion from this file would be a first formalization
- naming needed review before it could be treated as canonical

### Phase B: after the provisional foundations pass

The file now contains three local collections:

- `color/provisional`
- `spacing/provisional`
- `radius/provisional`

This means the workflow has already crossed the line from candidate
foundations into real provisional foundations.

At the same time, inspection of representative components showed that
some nodes already carry variable aliases from elsewhere in the Figma
ecosystem, especially inside `关闭`.

Practical meaning:

- the next step is not just “bind components”
- the workflow must first decide whether to:
  - preserve those external aliases,
  - remap them to the new local provisional variables,
  - or create an explicit bridge plan between the two

## Strong candidate variables

These values repeat enough across components and pages to justify a
provisional token pass.

### Color variables

- `text/primary` -> `#333333`
  - repeated across labels, body text, icons, and component internals
- `surface/base` -> `#ffffff`
  - repeated in tab containers, input surfaces, and white UI panels
- `border/default` -> `#d9d9d9`
  - repeated in tab and general UI boundary treatment
- `text/secondary` -> `#666666`
  - repeated in secondary labels and chrome text
- `text/tertiary` -> `#999999`
  - repeated in placeholders and section labels
- `state/hover-overlay` -> `#000000@0.04`
  - repeated in tab hover treatment and close hover treatment
- `surface/app-bg` -> `#ebeef5`
  - repeated as outer app/background treatment
- `surface/window` -> `#fafafa`
  - repeated as inner window body treatment
- `border/subtle` -> `#000000@0.08`
  - repeated in toolbar borders and light separators
- `focus/ring` -> `#0080ff@0.20`
  - repeated in `InputBox` focus treatment

### Radius variables

- `radius/sm` -> `8`
  - repeated in tabs, chips, and small rounded containers
- `radius/md` -> `12`
  - repeated in window surfaces and quick-action cards
- `radius/lg` -> `24`
  - repeated in `InputBox`
- `radius/pill` -> `99`
  - repeated in icon-button and pill-like controls

### Spacing variables

- `space/4`
- `space/8`
- `space/12`
- `space/16`
- `space/24`

These values recur consistently enough in gaps and paddings to justify a
first spacing scale.

## Strong candidate styles

These look reusable enough to become provisional shared styles, even if
the names should still be reviewed.

### Text styles

- `body/sm`
  - `HYQiHei/60S`, `12`, default auto line-height, `#333333`
- `body/md`
  - `HYQiHei/60S`, `14`, default auto line-height, `#333333`
- `placeholder/md`
  - `HYQiHei/55S`, `16`, `24px` line-height, `#000000@0.30`
- `chrome/label/sm`
  - `HYQiHei/55S`, `12`, `14px` line-height, `#999999`
- `headline/lg`
  - `HYQiHei/50S`, `28`, auto line-height, `#000000`

### Effect or stroke styles

- `focus/ring/input`
  - derived from the recurring `InputBox` focus outline
- `border/subtle/toolbar`
  - derived from the recurring light border treatment in top chrome

## Candidate foundations that need review before promotion

These patterns are visible, but their semantic meaning is not stable
enough to name automatically.

### Brand or accent colors

- `#009bff`
- `#1f62ee`
- `#ffca28`
- `#ff0057`

These appear in icons or branded visuals, but the current sample does not
prove whether they are:

- true semantic tokens
- brand-only illustration colors
- or one-off asset colors

### Mixed font systems

The file currently mixes:

- `HYQiHei`
- `PICO Sans`
- `PICO Sans VFE SC`
- `SF Pro`

This needs human confirmation before we formalize a canonical text-style
taxonomy. Right now, the file may represent:

- intentional role-based typography
- platform-specific carryover
- or historical inconsistency

### Precision-only values

Several radii and gaps appear as fractional values that look
implementation-derived rather than design-system-derived:

- `0.8888...`
- `1.3333...`
- `3.7037...`
- `6.6666...`

These should not be promoted directly. They should be normalized into the
nearest intentional token only after review.

## Recommended first promotion order

1. Create provisional color variables for:
   - `text/primary`
   - `text/secondary`
   - `text/tertiary`
   - `surface/base`
   - `surface/window`
   - `surface/app-bg`
   - `border/default`
   - `border/subtle`
   - `state/hover-overlay`
   - `focus/ring`
2. Create provisional spacing variables:
   - `4`, `8`, `12`, `16`, `24`
3. Create provisional radius variables:
   - `8`, `12`, `24`, `99`
4. Create provisional text styles for the strongest repeated HYQiHei
   roles.
5. Leave accent colors and mixed-family typography unresolved until
   reviewed.

## Workflow implication

This file is ready for a **provisional foundations pass**, not yet for a
fully canonical library pass.

That means:

- we can create a first `Variables` collection safely
- we can create a small set of provisional text or border styles safely
- we should still keep naming and semantic review in the loop before
  treating those foundations as final

## New finding after the write pass

The provisional foundations are now present in the file, but component
binding should still happen in a controlled order.

### Binding implication

Not every component is equally safe for the first wave.

#### Best first target: `InputBox`

Reason:

- it clearly uses localizable primitives:
  - surface fill
  - subtle border
  - focus ring
  - large radius
- those map cleanly to the new local provisional variables
- its structure is richer than `关闭`, so it provides a better end-to-end
  test of local variable usage

#### Good second target: `页签`

Reason:

- its selected-state container uses white fill and a blue-tinted border
- radius is stable
- but the blue accent treatment is still semantically unresolved, so only
  the already-confirmed parts should be rebound first

#### Not a first-wave target: `书签`

Reason:

- it depends on accent/brand colors that are still unresolved
- promoting or rebinding it too early would force brand-token decisions
  we have not reviewed yet

### Additional caution

`关闭` looks simple, but it already contains external variable aliases on
its vector strokes. That makes it a good inspection target, but not the
cleanest first local-binding target unless we first decide how to handle
external aliases.
