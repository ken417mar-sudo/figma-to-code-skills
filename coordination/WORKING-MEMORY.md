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
- Stateful borders/strokes must not change geometry between states. This applies equally to static components: use `outline` or `inset box-shadow` instead of `border` when Figma specifies exact section heights. Apply `outline` to the element itself (not a parent) to avoid clipping by `overflow: hidden`.
- `figma-execution-shell` is the protocol wrapper for all real component cases.
- Compact action-icon controls should separate interactive size from icon size.
  Default pattern: `24×24` button/hit area with a `16×16` icon frame unless the formal source says otherwise.
- Exported SVG canvas size is packaging data, not the rendered-size contract.
  If a small icon looks wrong in code, inspect the SVG viewBox / padding and normalize the asset before changing component layout.
- Section headers with optional actions should be modeled as separate slots (`label` + optional `action`) rather than as a single undifferentiated row.
- If Figma gives an explicit inner row width, preserve it instead of defaulting list items to `w-full`.
- For icon-size review comments, debug in this order: outer button box → rendered icon box → exported SVG canvas.
- Hidden Figma layers (`hidden="true"`) are a valid source for alternate states when confirmed to represent a distinct product state. Call `get_design_context` with the hidden layer's node ID directly.
- Figma layer name prefixes such as `【H2】`, `【H3】` are Chinese Figma workflow annotation labels, not visible copy. Strip them before rendering; align typography to the node spec.
- All skill README changes must go through a feature branch + PR. Never commit directly to main.
- Newly exported assets must be `git add`-ed before committing. A clean local build does not guarantee CI will pass on a fresh checkout.

## Component Status

| Component | Status | Deferred |
|---|---|---|
| Tab | closed | hover-close lives in provisional validation |
| InputBox | closed | focus-shadow token mismatch accepted as-is; compact sidebar bg remains a deferred non-blocker |
| Toolbar | closed | `border border-[0.5px]` redundancy in urlFocused |
| Dialog | closed (2026-04-16) | HYQiHei font — shared typography pass |
| AIToolsRow | closed (2026-04-17) | active state remains proposal-level |
| Sidebar | closed (2026-04-17) | formal default-only pass; SVG color hardcoding + interaction/collapsed states deferred |
| BrowserResultPage / AssistantSidebarPanel | closed (2026-05-01) | collapsed launcher closed (PR #13, 56×24 geometry fixed); panel-specific chip/composer states deferred |
| WorkspacePage / TaskChatPanel | closed (2026-04-22) | Phase 6 Repeatability complete |
| TaskResultPage | closed (2026-05-01) | running state (PR #10) + completed state (PR #11) both merged |
| FileListCard (列表卡片/展开) | closed (2026-05-01) | PR #12 merged; geometry fixed via outline/inset-shadow |

## Phase Status

- Phase 6 Repeatability: **complete** (2026-04-22).
- Phase B — Existing-rule capture validation: **complete** (2026-04-24).
- Phase C — TaskResultPage chain + provisional cleanup: **complete** (2026-05-01).
  - agentic-browser-ui PRs #10–#13 merged
  - figma-to-code-skills PRs #37–#38 merged; 79e67f9 (doc sync)
  - All provisional markers cleared

## Next Candidates

No active track. Next: pick a new narrow component/state slice from Figma.
