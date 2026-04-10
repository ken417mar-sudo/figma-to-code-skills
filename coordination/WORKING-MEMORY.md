# Working Memory

Compact project memory for starting a new thread quickly.

## Repos

- `figma-to-code-skills`
  - path: `/Users/markun/Documents/Codex/Mars/figma-to-code-skills`
  - purpose: workflow rules, gotchas, skill definitions
- `agentic-browser-ui`
  - path: `/Users/markun/Documents/Codex/Mars/agentic-browser-ui`
  - purpose: implementation testbed for Figma-to-code cases
- `figma-export-slices-skill`
  - path: `/Users/markun/Documents/Cursor/skill_test/figma-export-slices`
  - purpose: standalone export-slices skill repo

## Shared Coordination

- stable entry: `/Users/markun/Documents/Codex/Mars/figma-to-code-skills/coordination/INDEX.md`
- current active issue: [#12](https://github.com/ken417mar-sudo/figma-to-code-skills/issues/12)
- historical issue: [#4](https://github.com/ken417mar-sudo/figma-to-code-skills/issues/4)

## Active Figma File

- file key: `iIbL9V4UrFeORPaM7KVji7`
- main board: `1708:29412`
- canonical tab component set: `1714:976`
- canonical close component set: `1714:1012`
  - off: `1714:1013`
  - on: `1714:1017`
- InputBox: `1708:30342`
- send button: `1708:30361`
- send icon: `1708:30363`
- provisional standalone board: `1787:10395`
- provisional tab interaction block: `1840:11328`

## Core Workflow

1. Confirm tech-stack profile and existing source of truth.
2. Read design context from Figma.
3. Clean messy drafts only if needed.
4. Extract rough rules and let a human confirm them.
5. Map confirmed rules into Figma foundations.
6. Export real implementation assets from source Figma.
7. Implement code from revised rules plus design context.
8. Verify against Figma and record gotchas.

## Key Rules Already Settled

- Existing spec/design-system rules outrank inferred design rules.
- Missing interaction states must be confirmed first; then they can be added
  as `provisional` validation states.
- Common interaction patterns can justify proposing provisional states, but
  cannot silently redefine canonical component rules.
- All icon resources default to the export workflow, preferably `svg`.
- If `FIGMA_TOKEN` is missing and export is required, stop and ask the user
  for the token before continuing.
- Exported SVG canvas dimensions are not the source of truth for rendered
  icon size; match the icon's in-component geometry from Figma.
- After exporting an SVG, inspect stroke/fill values before wiring. If they
  are hardcoded design-system colors, inline as SVG component with
  `currentColor`. Only use `<img>` for intentionally fixed colors (e.g.
  white arrow on colored button, brand logo).
- When `get_design_context` returns a CSS transform on an icon, verify the
  exported SVG orientation before copying it. The asset may already encode
  the correct direction — copying the transform blindly causes double-rotation.
- Stateful borders/strokes must not change geometry between states.

## Tab Status

- considered functionally closed for now
- all 8 variants were implemented and checked
- close icon flow uses source-exported assets
- product-layer hover-close behavior lives in provisional validation, not in
  the canonical tab component set

## InputBox Status

- current main task
- base implementation exists in
  `/Users/markun/Documents/Codex/Mars/agentic-browser-ui/src/components/InputBox.tsx`
- exported assets already exist for plus/model-toggle/voice/send icons
- current conclusion: layout is good enough to continue into state work
- known accepted exception: the toggle background can remain a bridge
  exception for now
- recent fix: send button arrow should not be rotated and should be sized by
  in-component geometry, not raw SVG canvas size

## Current Local Changes To Remember

- `figma-to-code-skills` has uncommitted rule updates:
  - `skills/figma-export-slices/README.md` — new SVG color-check step
  - `coordination/WORKING-MEMORY.md` — this file
- `agentic-browser-ui` is clean; latest commits:
  - `aea756b` — close/plus/voice/model-toggle converted to inline SVG + currentColor
  - `0872945` — send icon sized to natural SVG dimensions (10×11)
  - `0acbf47` — InputBox initial implementation

## Next Recommended Action

1. Continue InputBox interaction states: `focus`, `disabled`, `error`.
2. Commit figma-export-slices rule update (SVG color-check step).
3. Update INDEX.md InputBox status after inline SVG fix.
