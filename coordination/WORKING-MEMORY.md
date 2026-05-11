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
| Sidebar icon-only source | `1708:30181` |
| BrowserResultPage with assistant sidebar expanded | `1708:30204` |
| AssistantSidebar collapsed launcher | `1708:30243` |
| AssistantSidebarPanel compact input | `1708:30323` |
| AssistantSidebarPanel prompt list | `1708:30311` |
| TaskResultPage | `1708:30544` |
| FileListCard (列表卡片/展开) | `1708:30738` |
| NavigationMenu (pill-style nav) | `2080:42251`, `2080:42252` |
| ModelCard / Card board | `2080:40041`; first slice `2080:40042`, `2080:40051`, `2080:40064`, `2080:40079` |

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
- Scope expansions of an existing component must also rerun preflight
  when they add a new axis, optional control, design-owned asset, or
  verification surface. Treat them as small follow-up cases, not free
  patches on a closed component.

## Component Status

| Component | Status | Deferred |
|---|---|---|
| Tab | closed | hover-close lives in provisional validation |
| InputBox | closed | focus-shadow token mismatch accepted as-is; compact sidebar bg remains a deferred non-blocker |
| Toolbar | closed | `border border-[0.5px]` redundancy in urlFocused |
| Dialog | closed (2026-04-16) | HYQiHei font — shared typography pass |
| AIToolsRow | closed (2026-04-17) | active state remains proposal-level |
| Sidebar | verified (expanded + icon-only source) | expanded/default pass closed; icon-only source `1708:30181` matches existing collapsed implementation; hover/active rows + animation deferred |
| BrowserResultPage / AssistantSidebarPanel | closed (2026-05-07) | collapsed launcher closed (PR #13, 56×24 geometry fixed); panel-specific chip/composer verified with no drift; fully closed |
| WorkspacePage / TaskChatPanel | closed (2026-04-22) | Phase 6 Repeatability complete |
| TaskResultPage | closed (2026-05-01) | running state (PR #10) + completed state (PR #11) both merged |
| FileListCard (列表卡片/展开) | closed (2026-05-01) | PR #12 merged; geometry fixed via outline/inset-shadow |
| NavigationMenu | closed (2026-05-09) | PR #14 initial pill nav + PR #15 full variant/manage control; case PRs #43–#44; 1162px surface, 32px pills, 12px tab gap, ManageButton 16px side padding |
| SearchBar | closed (2026-05-09) | agentic-browser-ui PR #16 merged; source `2080:8086`; 240×32, rounded-12, 1.5px border, search+clear icons 18×18 |
| ModelCard | closed (2026-05-11) | first slice from Card board `2080:40041`: 模型广场 Normal/Hover/loading/Selected; DOM evidence all cards 284×132, loading track 244×6/fill 73×6; excludes 写作助手, AI 搜索, AI Space, local tag |

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
  - figma-to-code-skills PR #45 merged: follow-up scope expansions of existing components must rerun preflight when adding a new axis, optional control, design-owned asset, or verification surface.
  - agentic-browser-ui PR #14 + figma-to-code-skills PR #43 merged: initial `2080:42251` NavigationMenu.
  - agentic-browser-ui PR #15 + figma-to-code-skills PR #44 merged: full `2080:42252` NavigationMenu variant board, including optional 管理 control.
  - DOM evidence: 1162px full-width surface, 32px NavOption/More/Manage buttons, 12px tab gap, ManageButton 16px left/right padding.
- Phase F — Sidebar icon-only source confirmation: **complete** (2026-05-09). figma-to-code-skills PR #46 merged.
  - Figma `1708:30181` confirmed as the source for the icon-only/collapsed-like Sidebar rail.
  - `1990:11765` resolves to a single Sidebar component (`1708:30408`) under a plain frame, not a component set, so icon-only is source-confirmed but not a formal Figma variant axis.
  - Existing browser implementation measured: collapsed aside 240×816, padding 16px, icon row 60×24, gap 12px, buttons 24×24, icons 16×16.
- Phase G — SearchBar: **complete** (2026-05-09). agentic-browser-ui PR #16 + figma-to-code-skills PR #48 merged.
- Phase H — ModelCard first slice: **closed** (2026-05-11).
  - Source board: `2080:40041`.
  - Scope: 模型广场 `2080:40042` Normal, `2080:40051` Hover download overlay, `2080:40064` loading progress overlay, `2080:40079` Selected.
  - Value: compact stateful card case with exported icon/progress assets and geometry-sensitive strokes.
  - PRs: agentic-browser-ui PR #17 and figma-to-code-skills PR #50.
  - Verification: `npm run build`, `npm run lint`, `git diff --check`, browser DOM measurement passed. DOM evidence: four cards `284 × 132`; Hover button `88 × 32`; loading track `244 × 6`; loading fill `73 × 6`; Selected outline `1px #000`.

## Next Candidates

No active track.

After Phase H candidates:
- Expand Card to AI Space only if first slice reveals reusable overlay/progress rules worth broadening
- SearchBar micro-drift cleanup from Codex review (6px icon-to-text gap, black text, focused with-value wording)
- BookmarkButton bookmarked state (`1708:30231~30233`) — reframe as standalone extraction/formalization
- Tab bar (`2080:8062`, 1166×52) — instance in 顶栏 board, likely a new component
- Upgrade dialog progress state (`2080:7977`) — has download progress bar state
- ChatBubble / 对话气泡 remains weak for capability validation; keep it for reuse/formalization cleanup only
