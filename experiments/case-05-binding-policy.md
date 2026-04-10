# Case 05: Local Variables vs External Alias Binding Policy

## Goal

Define the workflow rule for what to do when a file contains both:

- newly created local provisional variables
- and pre-existing external variable aliases already attached to
  components

Without this policy, broad component binding can easily create a mixed
and incoherent source-of-truth situation.

## Figma target

- File key: `iIbL9V4UrFeORPaM7KVji7`
- Local provisional collections:
  - `color/provisional`
  - `spacing/provisional`
  - `radius/provisional`
- Representative components inspected:
  - `InputBox` `1708:30342`
  - `页签` `1714:976`
  - `关闭` `1714:1012`
  - `书签` `1714:971`

## New finding

After the provisional foundations pass, the file now contains real local
variables.

At the same time, some components already contain external variable
aliases, especially inside `关闭`.

Practical meaning:

- the next step is not simply “bind everything to the local variables”
- the workflow needs an explicit policy before broad rebinding starts

## Policy options

### 1. Preserve

Use this when the external alias source is already authoritative for the
project and the local provisional set is only exploratory.

Implication:

- local variables remain draft references
- canonical component bindings keep pointing to the external source

### 2. Remap

Use this when the new local variables are intended to become the file's
actual source of truth.

Implication:

- representative components are rebound to the local variables
- external aliases are removed from the rebound components
- this should start with low-risk components first

### 3. Bridge

Use this when the project is in transition and both systems need to
coexist temporarily.

Implication:

- some components keep external aliases
- some components adopt the new local variables
- the file needs a clear note that this is a migration state, not a final
  library state

## Recommended policy for this file right now

Use a **bridge-first** policy with a controlled remap order.

Reason:

- the local provisional collections are new and not yet human-reviewed
- at least one representative component (`关闭`) already uses external
  aliases
- the project still has unresolved accent-color and typography questions

So the workflow should:

1. keep the external alias usage visible instead of wiping it blindly
2. start local rebinding only on clean, low-risk components
3. delay alias-heavy or brand-heavy components until naming and source of
   truth are clearer

## Recommended first-wave binding order

### 1. `InputBox`

Best first-wave target.

Why:

- maps cleanly to local provisional variables
  - surface fill
  - subtle border
  - focus ring
  - large radius
- does not depend on unresolved accent/brand colors
- is structurally rich enough to prove the binding workflow

### 2. `页签`

Good second-wave target.

Why:

- radius and white surface are good local-binding candidates
- selected-state border treatment is visible

Constraint:

- do not force unresolved blue accent semantics into a canonical local
  token yet

### 3. `关闭`

Not the first local-binding target.

Why:

- already contains external aliases
- simple visually, but riskier from a source-of-truth perspective

### 4. `书签`

Do not use in the first wave.

Why:

- depends on unresolved accent/brand colors
- would force premature brand-token decisions

## Workflow rule

If a file contains both local provisional variables and external aliases:

- inspect representative components first
- decide whether the file is in preserve, remap, or bridge mode
- start rebinding with low-risk components only
- do not rebind brand-heavy or alias-heavy components in the first wave
- record the chosen policy before large-scale library work continues
