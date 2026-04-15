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
- Dialog section: `1922:32133`
- Dialog core block: `1922:31967`

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
- **Pre-implementation asset check (hard gate):** Before writing any icon
geometry in a component, check whether the icon has already been exported
into the repo. If `src/assets/figma/*.svg` already contains the source
icon, implementation must import that file — do not write or keep a
handwritten SVG substitute. This check must happen before implementation
starts, not as a cleanup step afterward.
- Newly added provisional Figma state cards must be explicitly approved by
the user or team before they become implementation input.
- Provisional state cards for an existing component must start from the
approved baseline component and preserve all unchanged parts, including
icon assets, text, and structure. Only the state-specific delta should
change.
- When `get_design_context` returns a CSS transform on an icon, verify the
exported SVG orientation before copying it. The asset may already encode
the correct direction — copying the transform blindly causes double-rotation.
- Stateful borders/strokes must not change geometry between states.
- `figma-execution-shell` is now in main; use it as the protocol wrapper for
real component cases, then tighten it only after a real run exposes a stable
gap.

## Tab Status

- considered functionally closed for now
- all 8 variants were implemented and checked
- close icon flow uses source-exported assets
- product-layer hover-close behavior lives in provisional validation, not in
the canonical tab component set

## InputBox Status

- **closed** — all 4 states verified, geometry stable
- commits: `d6afa94` (4 states), `ef0099c` (geometry fix)
- deferred non-blockers: `ic_` rename, `开关` bridge exception,
focus-state shadow token mismatch accepted as-is

## Toolbar Status

- **closed** — all 5 states verified, committed, and pushed
- commits: `eb13c90` (Toolbar.tsx + assets), `dbd1136` (bookmark icon viewBox fix)
- provisional boards confirmed:
  - NavIcon disabled (`1872:10395`): `opacity: 0.3` on 24×24 wrapper ✓
  - Bookmark bookmarked + URLBar focused (`1873:10395`): icons correct ✓
- deferred non-blocker: `border border-[0.5px]` redundancy in `urlFocused`

## Dialog Status

- **in progress** — Phase 4 validation case for the execution shell
- shell milestones:
  - PR `#18` merged — initial `figma-execution-shell`
  - PR `#19` merged — shell v2 gate tightening
- current code state in `agentic-browser-ui`:
  - Dialog structure and static variant axes implemented
  - `closeVariant='hover'` now forces the hover icon
  - image content branch now renders even with empty `imageSrc` (gray placeholder)
  - visual fidelity pass has started
- current open issues:
  - horizontal image dialog still uses the text-dialog spacing shell; spacing is too loose vs Figma
  - button-type verify cards in `App.tsx` are still handwritten examples, not real `DialogButton` branches
- interpret current checkpoint as:
  - implementation-complete
  - verification-partial

## Open Questions

- Dialog visual verify still needs one more pass before closeout.

## Current Local Changes To Remember

- `figma-to-code-skills`: Phase 4 shared-state sync in progress on current branch
- `agentic-browser-ui`: Dialog implementation is local and uncommitted on `main`

## Next Recommended Action

Finish Dialog visual verify / fix, then close the case before starting the next component or making another shell-quality pass.
