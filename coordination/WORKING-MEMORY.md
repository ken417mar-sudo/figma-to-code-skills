# Working Memory

Compact project memory for starting a new thread quickly.
**New to this project? Read [coordination/ONBOARDING.md](ONBOARDING.md) first.**

## Repos

- `figma-to-code-skills` — `/Users/markun/Documents/Codex/Mars/figma-to-code-skills` — workflow rules, gotchas, skill definitions
- `agentic-browser-ui` — `/Users/markun/Documents/Codex/Mars/agentic-browser-ui` — implementation testbed for Figma-to-code cases

## Shared Coordination

- stable entry: `coordination/INDEX.md`
- current active issue: [#13](https://github.com/ken417mar-sudo/figma-to-code-skills/issues/13) — permanent coordination log, never close

## Active Figma File

- file key: `iIbL9V4UrFeORPaM7KVji7`
- main board: `1708:29412`

Key node IDs:
| Component | Node ID |
|---|---|
| Tab component set | `1714:976` |
| Close off/on | `1714:1013` / `1714:1017` |
| InputBox | `1708:30342` |
| AIToolsRow | `1708:30180` |
| Dialog section | `1922:32133` |
| Sidebar | `1708:30337` |
| BrowserResultPage with assistant sidebar expanded | `1708:30204` |

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
- Missing interaction states must be confirmed first; then they can be added as `provisional` validation states.
- Common interaction patterns can justify proposing provisional states, but cannot silently redefine canonical component rules.
- All icon resources default to the export workflow, preferably `svg`. Inline as SVG component with `currentColor` for theme-reactive icons; only use `<img>` for intentionally fixed colors.
- **Pre-implementation asset check (hard gate):** For every design-owned icon or image, complete the export check before implementation. If the asset already exists in `src/assets/figma/`, import it. If it does not exist yet, export it first. Do not ship component code with inline SVG, placeholder geometry, or handwritten replacement icons while that export check is still incomplete.
- Provisional boards must be standalone (not inside a formal artboard) and have clear canvas separation from neighboring boards.
- Provisional state cards must apply state to the root control container, not by appending extra layers.
- Do not promote a component set to canonical while any family boundary or state axis is still provisional — even if the user explicitly requests it.
- Stateful borders/strokes must not change geometry between states.
- `figma-execution-shell` is the protocol wrapper for all real component cases.
- Compact action-icon controls should separate interactive size from icon size.
  Default pattern: `24×24` button/hit area with a `16×16` icon frame unless the formal source says otherwise.
- Exported SVG canvas size is packaging data, not the rendered-size contract.
  If a small icon looks wrong in code, inspect the SVG viewBox / padding and normalize the asset before changing component layout.
- Section headers with optional actions should be modeled as separate slots (`label` + optional `action`) rather than as a single undifferentiated row.
- If Figma gives an explicit inner row width, preserve it instead of defaulting list items to `w-full`.
- For icon-size review comments, debug in this order: outer button box → rendered icon box → exported SVG canvas.

## Component Status

| Component | Status | Deferred |
|---|---|---|
| Tab | closed | hover-close lives in provisional validation |
| InputBox | closed | focus-shadow token mismatch accepted as-is |
| Toolbar | closed | `border border-[0.5px]` redundancy in urlFocused |
| Dialog | closed (2026-04-16) | HYQiHei font — shared typography pass |
| AIToolsRow | closed (2026-04-17) | active state remains proposal-level |
| Sidebar | closed (2026-04-17) | formal default-only pass; SVG color hardcoding + interaction/collapsed states deferred |

## Component Family Definition

Three historical validation cards written and replay-validated (2026-04-17):
- `experiments/trial-component-family-definition-aitoolsrow.md`
- `experiments/trial-component-family-definition-dialog.md`
- `experiments/trial-component-family-definition-sidebar.md`

All three passed Figma / code / verify three-segment validation. The format
is now formalized as the required component-scoped output of
`figma-create-design-system-rules` when the family boundary is clear.
Key formal constraints now locked:
- `definition_status` and `verification_status` stay independent.
- composite-family root cards describe composition; independently reusable or
  independently verifiable sub-families get their own cards.
- live cards should be updated in place instead of being recreated as new
  "trial" documents.

## Sidebar Progress

- Figma MCP recovery confirmed on 2026-04-17.
- Formal default-only pass completed 2026-04-17 by Claude Code: 6 formal states all passed (V1–V2, V5, V7, V9–V10).
- Section-header padding bug fixed (`pl-[12px] pr-[4px]` for Projects, `px-[12px]` for History).
- Implementation is now committed, pushed, and visible in `agentic-browser-ui` PR #4 (`codex/sidebar-phase4`).
- Deferred (non-blocking): SVG icon colors hardcoded (#333/#999), theme-reactive未确认; interaction/collapsed states unconfirmed.

## Active Case: BrowserResultPage / Assistant Sidebar

- New source node selected on 2026-04-20: `1708:30204` (`网页结果页`).
- User-directed scope order: first clean up hierarchy and naming, then move into implementation.
- Family boundary is treated as:
  - composite root: `BrowserResultPage`
  - simple sub-family: `AssistantSidebarPanel`
- Live cards:
  - `cases/component-family-definition-browser-result-page.md`
  - `cases/component-family-definition-assistant-sidebar-panel.md`
- Implementation has started in `agentic-browser-ui` on branch `codex/browser-result-assistant-sidebar` (PR #5); build passes, visual verify still pending.
- Intentionally provisional:
  - collapsed page state
  - hidden toolbar launcher reference (`1708:30243`) as canonical click-to-open source
  - panel-specific chip / composer interaction states beyond existing families

## Next Recommended Action

1. Review the live hierarchy / naming cards for the BrowserResultPage case.
2. Reuse existing `Toolbar` / `InputBox` families where possible during implementation.
3. Keep the collapsed launcher flow provisional until the hidden reference is explicitly confirmed as canonical.
