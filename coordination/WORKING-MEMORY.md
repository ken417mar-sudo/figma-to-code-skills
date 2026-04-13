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
- current active issue: [#13](https://github.com/ken417mar-sudo/figma-to-code-skills/issues/13) — permanent coordination log, never close
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

- **closed** — all 4 states verified, geometry stable
- commits: `d6afa94` (4 states), `ef0099c` (geometry fix)
- deferred non-blockers: `ic_` rename, `开关` bridge exception

## Toolbar Status

- **in progress** — code written (Toolbar.tsx), NOT yet committed
- workflow violation: code was written before Figma provisional states were added (now remediated)
- provisional board updated:
  - NavIcon disabled state (`1872:10395`): 4 cards, rule: `opacity: 0.3` on button wrapper ✓
  - Bookmark bookmarked + URLBar focused (`1873:10395`): designs added ✓ (blocker cleared)
- next step: implement `bookmarked` + `urlFocused` → verify → commit

## Open Questions

None — all Toolbar provisional states are in Figma.

## Current Local Changes To Remember

- `figma-to-code-skills` clean and pushed. latest: `1ebd443`
- `agentic-browser-ui`: Toolbar.tsx + assets written, NOT committed (pending verification)

## Next Recommended Action

User to add Bookmark bookmarked and URLBar focused designs to Figma provisional
board, then implement those two states and verify all Toolbar states.
