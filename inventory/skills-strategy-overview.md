# Skills Strategy Overview

## North Star

Build a Figma-to-code workflow that can reliably deliver implementation
from real-world design files.

The default priority is:

1. use existing project spec or design-system rules first
2. capture undocumented team rules if they exist but are not written down
3. extract only the missing rules from Figma when no adequate spec exists
4. implement code with both visual fidelity and structural correctness
5. verify the built result and feed recurring mistakes back into the skill

## Core Principles

- existing rules beat inferred rules
- explicit platform profile beats platform guessing
- clarified intent beats model invention
- structural correctness matters, not just visual similarity
- messy design files are raw material, not automatically source of truth
- skills should encode workflow judgment, not only tool syntax
- mature skills should accumulate `gotchas`
- smaller composable skills are preferred, with larger orchestrating skills
on top

## Workflow We Are Building

1. Confirm the target tech-stack profile.
2. Check whether a usable spec or design-system rule set already exists.
3. If rules exist but are undocumented, capture them into a reusable skill
  or editable rule file.
4. If the design file is messy, clean it just enough to reduce
  implementation noise.
5. If coverage is missing, infer a rough rule draft from the design.
6. Let a human revise the rule draft.
7. Implement code using the spec plus the design context.
8. Verify the built result against Figma using the platform-appropriate
  surface.
9. Turn repeated failure modes into skill gotchas.

## Platform Profile

Every major workflow should receive a tech-stack profile with at least:

- `target`: `web` | `ios` | `android`
- `framework`: for example `react`, `swiftui`, `compose`
- `token_format`: for example `css-vars`, `swift-tokens`,
`compose-tokens`

Reference:

- [tech-stack-profile.md](/Users/markun/Documents/Codex/Mars/figma-to-code-skills/inventory/tech-stack-profile.md)

## Skills We Need

### A. Foundation layer

These are base capabilities that support everything else.

- `figma`
General read access to design context, screenshots, variables, metadata,
and assets.
- `figma-use`
Structured write access to Figma files for cleanup, organization,
component editing, variables, and layout fixes.

### B. Core delivery layer

These are the most important skills for the first version of the workflow.

- `figma-capture-design-system`
Capture existing but undocumented design-system knowledge through
interview and convert it into an explicit implementation reference,
including platform-specific rules.
- `figma-ai-implementation-cleanup`
Reduce messy layers, bad naming, hidden legacy content, and other noise
that makes implementation unstable.
- `figma-create-design-system-rules`
Generate a rough rule set when no complete spec exists, or fill missing
parts when the spec is partial. The output must be profile-aware.
- `figma-implement-design`
Turn Figma design context plus rules into implementation code for the
declared target platform and framework.
- `figma-verify-implementation`
Compare built UI against Figma, annotate differences, and classify what
matters using a platform-appropriate verification path.

### C. System-enrichment layer

These are important, but not all of them need to be in the very first
milestone.

- `figma-code-connect-components`
Map Figma components to real code components once repeated patterns are
clear enough. This is framework-dependent and should only be used where
Code Connect support matches the target stack.
- `figma-generate-library`
Build or update a Figma design system library from codebase and tokens.
- `figma-export-slices`
Export slices and assets needed by implementation according to the
target platform asset profile.

### D. Gap-filling and acceleration layer

These are useful when the project is incomplete, but they should not
override the main source-of-truth rules.

- `figma-sketch-to-system-components`
Expand sketches or low-fidelity drafts into components that stay within
the established design system.
- `figma-generate-design`
Generate or update Figma screens from code or page structure.
- `figma-create-new-file`
Create a new blank Figma or FigJam file as setup support.

## Recommended Build Order

### Phase 1: Must-have for the first real workflow

- `figma`
- `figma-use`
- `tech-stack-profile`
- `figma-capture-design-system`
- `figma-ai-implementation-cleanup`
- `figma-create-design-system-rules`
- `figma-implement-design`
- `figma-verify-implementation`

### Phase 2: Improve engineering linkage and reuse

- `figma-code-connect-components`
- `figma-export-slices`
- `figma-generate-library`

### Phase 3: Fill missing design coverage faster

- `figma-sketch-to-system-components`
- `figma-generate-design`
- `figma-create-new-file`

## Scenario Coverage

### 1. Project already has a design system or spec

Use:

- `tech-stack-profile`
- `figma-capture-design-system` if the rules are mostly implicit
- `figma-implement-design`
- `figma-verify-implementation`

Outcome:

- implement against the existing system instead of re-inventing rules

### 2. Project has partial rules, but not enough to implement safely

Use:

- `tech-stack-profile`
- `figma-capture-design-system`
- `figma-create-design-system-rules`
- `figma-implement-design`
- `figma-verify-implementation`

Outcome:

- preserve what already exists and infer only the missing pieces

### 3. Design file is messy, old, or inconsistent

Use:

- `tech-stack-profile`
- `figma-ai-implementation-cleanup`
- `figma`
- `figma-use`
- `figma-create-design-system-rules`
- `figma-implement-design`

Outcome:

- reduce noise before implementation and avoid turning accidental mess
into standards

### 4. Design is visually complete, but component mapping to code is weak

Use:

- `tech-stack-profile`
- `figma-code-connect-components`
- `figma-implement-design`
- `figma-verify-implementation`

Outcome:

- better reuse of real code components and less implementation drift

### 5. Design is incomplete and only sketches or low-fi ideas exist

Use:

- `tech-stack-profile`
- `figma-sketch-to-system-components`
- `figma-generate-design`
- `figma-implement-design`

Constraint:

- only for gap-filling
- should follow the existing system when one exists

### 6. Need to maintain or build the design system itself

Use:

- `tech-stack-profile`
- `figma-generate-library`
- `figma-create-design-system-rules`
- `figma-code-connect-components`

Outcome:

- strengthen the bridge between design system and implementation system

### 7. Need exported assets for implementation

Use:

- `tech-stack-profile`
- `figma-export-slices`

Outcome:

- implementation-ready assets with better naming and export flow

## What Is Already Covered vs. What Still Needs Building

### Already represented as existing skills

- `figma`
- `figma-use`
- `figma-ai-implementation-cleanup`
- `figma-create-design-system-rules`
- `figma-implement-design`
- `figma-code-connect-components`
- `figma-generate-library`
- `figma-generate-design`
- `figma-export-slices`
- `figma-create-new-file`

### Candidate skills we should likely add

- `tech-stack-profile`
- `figma-capture-design-system`
- `figma-sketch-to-system-components`
- `figma-verify-implementation`

## Current Recommendation

If we want the first version to be useful quickly, the workflow should be
centered on this path:

1. capture or confirm rules
2. confirm platform profile
3. clean messy design when needed
4. infer only missing rules
5. implement
6. verify
7. record gotchas

That gives us the strongest coverage for the main target scenario:

"There is a real design draft, no perfect spec, and we still need to ship
good code."