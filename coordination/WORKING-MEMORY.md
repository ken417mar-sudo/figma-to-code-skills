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
| AssistantSidebar collapsed launcher | `1708:30243` |
| AssistantSidebarPanel compact input | `1708:30323` |
| AssistantSidebarPanel prompt list | `1708:30311` |
| TaskResultPage | `1708:30544` |
| FileListCard (列表卡片/展开) | `1708:30738` |
| NavigationMenu (pill-style nav) | `2080:42251`, `2080:42252` |

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
- Official Figma MCP skills are the upstream boundary reference, but local
  stricter gates still apply when validated cases prove they are needed:
  asset export-first, provisional approval, hidden-layer product-state
  confirmation, Code Connect maturity checks, and rendered verification.
- `ui-motion-patterns` is a web-only motion rule/template layer. Use it
  after source-of-truth and state confirmation; it does not authorize
  inventing new states or masking static Figma geometry drift.
- New component slices must pass preflight before code is considered
  implementation-ready: component-family card or minimum scope note,
  asset inventory, state-geometry scan, and verification surface. Review
  should grep for unclassified inline SVGs and state-only 0.5px borders.

## Component Status

| Component | Status | Deferred |
|---|---|---|
| Tab | closed | hover-close lives in provisional validation |
| InputBox | closed | focus-shadow token mismatch accepted as-is; compact sidebar bg remains a deferred non-blocker |
| Toolbar | closed | `border border-[0.5px]` redundancy in urlFocused |
| Dialog | closed (2026-04-16) | HYQiHei font — shared typography pass |
| AIToolsRow | closed (2026-04-17) | active state remains proposal-level |
| Sidebar | closed (2026-04-17) | formal default-only pass; SVG color hardcoding + interaction/collapsed states deferred |
| BrowserResultPage / AssistantSidebarPanel | closed (2026-05-07) | collapsed launcher closed (PR #13, 56×24 geometry fixed); panel-specific chip/composer verified with no drift; fully closed |
| WorkspacePage / TaskChatPanel | closed (2026-04-22) | Phase 6 Repeatability complete |
| TaskResultPage | closed (2026-05-01) | running state (PR #10) + completed state (PR #11) both merged |
| FileListCard (列表卡片/展开) | closed (2026-05-01) | PR #12 merged; geometry fixed via outline/inset-shadow |
| NavigationMenu | closed (2026-05-09) | PR #14 initial pill nav + PR #15 full variant/manage control; case PRs #43–#44; 1162px surface, 32px pills, 12px tab gap, ManageButton 16px side padding |

## Phase Status

- Phase 6 Repeatability: **complete** (2026-04-22).
- Phase B — Existing-rule capture validation: **complete** (2026-04-24).
- Phase C — TaskResultPage chain + provisional cleanup: **complete** (2026-05-01).
  - agentic-browser-ui PRs #10–#13 merged
  - figma-to-code-skills PRs #37–#38 merged; 79e67f9 (doc sync)
  - All provisional markers cleared
- Phase D — official skills alignment + motion skill + AssistantSidebarPanel closeout: **complete** (2026-05-07).
  - figma-to-code-skills PR #39 merged: official Figma MCP skills alignment
  - figma-to-code-skills PR #40 merged: `ui-motion-patterns` skill and templates
  - AssistantSidebarPanel compact composer (`1708:30323`) and prompt list (`1708:30311`) verified with no drift
  - `coordination/INDEX.md` cleaned up and Phase D state written
  - Both repos have no open PRs or active track
- Phase E — NavigationMenu + new-slice preflight hard gate: **complete** (2026-05-09).
  - figma-to-code-skills PR #42 merged: new component slices require scope note/case card, asset inventory, and state-geometry scan before code.
  - agentic-browser-ui PR #14 + figma-to-code-skills PR #43 merged: initial `2080:42251` NavigationMenu.
  - agentic-browser-ui PR #15 + figma-to-code-skills PR #44 merged: full `2080:42252` NavigationMenu variant board, including optional 管理 control.
  - DOM evidence: 1162px full-width surface, 32px NavOption/More/Manage buttons, 12px tab gap, ManageButton 16px left/right padding.

## Next Candidates

No active track. Next: pick a new narrow component/state slice from Figma.

Current candidates:
- BookmarkButton bookmarked state (`1708:30231~30233`)
- Sidebar TitleBar (`1708:30268`)
- Sidebar collapsed state — first confirm whether Figma has a formal
  variant before treating it as implementation input
- 顶栏变体 (`2080:7520`) if it can be narrowed to a stateful slice
- ChatBubble / 对话气泡 is a weak validation case unless the goal is only
  extracting/reusing the existing embedded bubble from `TaskChatPanel`
