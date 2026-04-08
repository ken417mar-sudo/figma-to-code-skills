# Case 03: Provisional State Supplement Board

## Figma target

- File key: `iIbL9V4UrFeORPaM7KVji7`
- Original parent board: `1714:1024` (`组件`)
- Current standalone test board: `1787:10395`
  (`组件补充测试 / provisional / standalone`)

## Goal

Test whether we can safely supplement an existing component board with a
separate validation-only state section, without modifying the project's
formal component sets.

This case is about workflow support, not final design-system authorship.

## What was done

Created a new framed section inside the `组件` board:

- `组件补充测试 / provisional`

The section was explicitly labeled as workflow validation only.

Later, after the first pass exposed clipping and overflow, the section
was promoted into a standalone test board on the same page so it no
longer competed with the formal component board for space.

Inside it, two state groups were added:

### 1. `InputBox` states

Using the existing component source:

- `InputBox` component: `1708:30342`

Added state cards:

- `default`
- `focus`
- `disabled`
- `error`

Implementation approach:

- create instances from the existing `InputBox` component
- apply lightweight visual overrides per state
- keep everything in a separate provisional section instead of editing
  the formal source component

### 2. `关闭` control states

Using the existing component samples:

- `Hover=off` component: `1714:1013`
- `Hover=on` component: `1714:1017`

Added state cards:

- `default`
- `hover`
- `focus`
- `pressed`

Implementation approach:

- instantiate existing variants
- derive additional validation states through non-destructive visual
  treatment
- keep them separate from the formal component set

## Why this matters

This proves a useful workflow capability:

- when a project has explicit component work but incomplete state
  coverage, we can add a validation-only supplement board
- we do not have to immediately mutate the official component set
- we can use the supplement board to test missing states before deciding
  whether they belong in the formal design system

## What worked

- existing components were discoverable and reusable:
  - `页签` and `关闭` are real `COMPONENT_SET`s
  - `InputBox` and `AIToolsRow` are reusable `COMPONENT`s
- a separate provisional frame could be added safely
- the new section is visually distinct and clearly marked as non-final
- the resulting board is strong enough for workflow validation and review

## Limitations observed

### 1. Supplement board quality is enough for testing, not final authorship

The new states are useful for validating workflow logic, but they should
not be treated as automatically approved final component states.

### 2. Compact single-row comparison layouts are fragile for large inputs

`InputBox` is large. The first single-row layout overflowed horizontally
and then caused the outer section to clip downstream content. The board
only became stable after the test section was moved to its own frame and
the `InputBox` states were split into two horizontal rows.

### 3. Product semantics are still missing

A board like this can add generic states such as:

- focus
- disabled
- error
- pressed

But it still cannot invent product-specific rules such as:

- exact validation copy
- actual business error conditions
- accessibility text requirements
- state priority rules

Those still need human confirmation.

## Workflow conclusion

This case proves that the workflow can do more than observe Figma. It can
also add a safe provisional testing layer on top of an existing component
board.

That makes this a useful bridge between:

- pure analysis
- and formal design-system maintenance

## Recommended rule

If we supplement a component board ourselves, do it under these
constraints:

- create a separate `provisional` or `validation` section
- do not modify formal component sets by default
- label added states clearly as workflow/test states
- treat the output as review material, not canonical spec
- if the supplement grows beyond the parent board, move it into a
  standalone validation board on the same page rather than stretching
  the formal board
- size the validation board to fully contain its children, then reflow
  large components into multiple rows instead of allowing horizontal
  overflow
