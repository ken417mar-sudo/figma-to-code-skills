# Coordination Index

Single entry point for all three contributors (user, Claude, Codex).
Update this file when phase, repos, or active work changes.

## Stable Memory

- Working summary for new threads:
  `coordination/WORKING-MEMORY.md`

## Current Phase

Phase 3 closed (2026-04-13) — Tab, InputBox, Toolbar all verified and committed.
Phase 4 closed (2026-04-20) — `figma-execution-shell` merged; Dialog, AIToolsRow, and Sidebar (default-only) are all closed.
Phase 5 closed (2026-04-20) — BrowserResultPage + AssistantSidebarPanel composite family case merged and formally closed.
Phase 6 closed (2026-04-22) — WorkspacePage + TaskChatPanel Repeatability case complete. All 8 component cases closed.
Phase A closed (2026-04-23) — PR #6 (agentic-browser-ui WorkspacePage) and PR #17 (figma-use gotchas) both merged. No open PRs.
Phase B closed (2026-04-24) — Existing-rule capture validation complete. B.1: inventory enriched with code evidence (PR #31). B.2: Tab CloseIcon inline SVG → exported assets, rule-driven (agentic-browser-ui PR #7). B.3: figma-capture-design-system code-backed mode + execution-shell routing reference + inventory resolved-gap cleanup (PR #32).
Phase C closed (2026-05-01) — TaskResultPage running+completed validation chain + FileListCard + provisional cleanup. agentic-browser-ui PRs #10–#13 merged. figma-to-code-skills PRs #37–#38 merged. All provisional markers cleared.
Phase D closed (2026-05-07) — Official skills alignment (PR #39) + ui-motion-patterns skill (PR #40) merged. AssistantSidebarPanel composer/prompt area verified, no drift. All stale remote branches cleaned from both repos.
Phase E closed (2026-05-09) — NavigationMenu (pill-style nav, Figma 2080:42251 + full variant board 2080:42252) implemented and verified. agentic-browser-ui PRs #14–#15 + figma-to-code-skills PRs #43–#44 merged. Preflight hard-gate rules added (PRs #42 and #45).
Phase F closed (2026-05-09) — Sidebar icon-only/collapsed-like source confirmation. Figma `1708:30181` confirmed as the source frame and matched to the existing `Sidebar collapsed` implementation. figma-to-code-skills PR #46 merged.
Phase G closed (2026-05-09) — SearchBar component (Figma `2080:8086`, 240×32). agentic-browser-ui PR #16 + figma-to-code-skills PR #48 merged.
Phase H closed (2026-05-11) — ModelCard first slice from Card board `2080:40041`: 模型广场 Normal/Hover/loading/Selected (`2080:40042`, `2080:40051`, `2080:40064`, `2080:40079`). agentic-browser-ui PR #17 + figma-to-code-skills PR #50 merged.

## Active Repos

| Repo | Purpose |
|---|---|
| `figma-to-code-skills` | skill rules, gotchas, workflow inventory |
| `agentic-browser-ui` | implementation target (React + Tailwind) |

Local paths:
- `~/Documents/Codex/Mars/figma-to-code-skills`
- `~/Documents/Codex/Mars/agentic-browser-ui`

## Active Issues

- [#13 — Coordination Log (permanent)](https://github.com/ken417mar-sudo/figma-to-code-skills/issues/13) — never close, rolling action log

Closed:
- [#12 — InputBox implement→verify](https://github.com/ken417mar-sudo/figma-to-code-skills/issues/12) — closed, all 4 states verified
- [#4 — Phase 1 skill rewrite](https://github.com/ken417mar-sudo/figma-to-code-skills/issues/4) — all skills rewritten, Tab case closed

## Active Figma File

- File key: `iIbL9V4UrFeORPaM7KVji7`
- URL: `https://www.figma.com/design/iIbL9V4UrFeORPaM7KVji7`

Key node IDs:
| Component | Node ID |
|---|---|
| AIToolsRow | `1708:30180` |
| BrowserResultPage (assistant sidebar expanded) | `1708:30204` |
| InputBox | `1708:30342` |
| 页签 (8 variants) | `1714:977`, `1714:983`, `1714:990`, `1714:1001`, `1720:89968`, `1720:89980`, `1720:89992`, `1720:90000` |
| 关闭 Hover=off | `1714:1013` |
| 关闭 Hover=on | `1714:1017` |
| 侧边栏展开 board | `1708:30337` |
| Sidebar icon-only source | `1708:30181` |
| Dialog section | `1922:32133` |
| Dialog core block | `1922:31967` |
| TaskResultPage | `1708:30544` |
| FileListCard (列表卡片/展开) | `1708:30738` |
| AssistantSidebar collapsed launcher | `1708:30243` |
| AssistantSidebarPanel 输入框 | `1708:30323` |
| AssistantSidebarPanel 预设问题 | `1708:30311` |
| NavigationMenu (pill-style nav) | `2080:42251`, `2080:42252` |
| ModelCard / Card board | `2080:40041`; 模型广场 slice `2080:40042`, `2080:40051`, `2080:40064`, `2080:40079` |

## Current State

### Tab — closed
All 8 variants verified. close-off/close-on SVGs from source export wired. No gaps.

### InputBox — closed
All 4 states (default/focus/disabled/error) implemented and verified.
Geometry stable via inset box-shadow. Icons use inline SVG + currentColor.
Commits: `d6afa94`, `ef0099c` in agentic-browser-ui.
focus-shadow mismatch noted by Codex — accepted as-is, not a blocker.

### Toolbar — closed
All 5 states verified and pushed.
Commits: `eb13c90`, `dbd1136` in agentic-browser-ui.
Deferred non-blocker: `border border-[0.5px]` redundancy in `urlFocused`.

### Dialog — closed (2026-04-16)
All axes implemented. Deferred non-blocker: HYQiHei font loading.

### AIToolsRow — closed (2026-04-17)
All axes implemented. Deferred: active state remains proposal-level.

### Sidebar — verified (expanded + icon-only source)
Expanded/default pass closed (2026-04-17). Icon-only/collapsed-like rail source confirmed (2026-05-09): Figma `1708:30181` is a 240×816 rail with 16px padding, two 24×24 buttons, 12px gap, and 16px icons. Browser DOM measurement of the existing implementation matches those dimensions. This is a source-confirmed frame, not a Figma component-set variant; hover/active row states and animation remain deferred.

### BrowserResultPage / AssistantSidebarPanel — closed (2026-05-07)
Composite family case. Source node: `1708:30204`.
Implementation merged via PR #5 (agentic-browser-ui) and PR #27 (figma-to-code-skills).
Collapsed launcher (`1708:30243`) closed (2026-05-01): geometry fixed to 56×24 via agentic-browser-ui PR #13 (border → outline).
Panel-specific chip/composer states verified (2026-05-07): no drift found. Fully closed.

### WorkspacePage / TaskChatPanel — closed (2026-04-22)
Phase 6 Repeatability case. Composite family.

### TaskResultPage — closed (2026-05-01)
Running state: agentic-browser-ui PR #10 merged.
Completed state: agentic-browser-ui PR #11 merged.
Source nodes: `1708:30544` (main frame), `1708:30803–30806` (completed hidden layers).
Durable lessons: hidden layers as alternate-state source; 【H2】 annotation prefix handling.

### FileListCard (列表卡片/展开) — closed (2026-05-01)
Source node: `1708:30738` (TaskResultPage hidden layer, confirmed product state).
agentic-browser-ui PR #12 merged.
Durable lesson: static component strokes must be non-layout-affecting (outline/inset-shadow).

### NavigationMenu — closed (2026-05-08)
Source nodes: `2080:42251` (initial pill-style nav) and `2080:42252` (full variant board with 3–10 items, optional more, optional 管理 control).
agentic-browser-ui PR #14 merged the initial component; PR #15 merged full variant/manage-control coverage.
figma-to-code-skills PR #43 added the case card; PR #44 synced full variant evidence.
DOM evidence: 1162px full-width surface, 32px pills, 12px tab gap, 管理 button 16px left/right padding.
Durable lesson: preflight (scope note + asset inventory + state-geometry scan) must happen before code, not after. PR #42 made this a hard gate in figma-execution-shell.

### SearchBar — closed (2026-05-09)
Source node: `2080:8086` (instance in NavigationMenu spec board, 240×32).
agentic-browser-ui PR #16 merged: SearchBar component + showSearch slot in NavigationMenu.
DOM evidence: `h-[32px] w-[240px] rounded-[12px] border-[1.5px]`, search icon 18×18, clear button visible when value non-empty.

### ModelCard — closed (2026-05-11)
Source board: `2080:40041`.
First slice: 模型广场 Normal/Hover/loading/Selected (`2080:40042`, `2080:40051`, `2080:40064`, `2080:40079`).
Implementation merged via agentic-browser-ui PR #17.
Case card and coordination merged via figma-to-code-skills PR #50.
DOM evidence: all four cards `284 × 132`; Normal/Hover/loading outline `0.5px`; Selected outline `1px #000`; Hover button `88 × 32`; loading track `244 × 6`; loading fill `73 × 6`.
Scope intentionally excludes 写作助手, AI 搜索, AI Space, and optional local tag until the first slice is verified.

## Open PRs

No open PRs in either repo.

## Next Recommended Action

Phase H closed. Next: either expand the Card family to AI Space if overlay/progress
rules are worth broadening, or do the previously noted SearchBar micro-drift
cleanup. Keep ChatBubble as a reuse/formalization cleanup candidate only.

## Source-of-Truth Notes

- Skill rules live in `skills/*/README.md` — authoritative for agent behavior
- Workflow rules live in `inventory/workflow-outline.md`
- CSS tokens live in `agentic-browser-ui/src/index.css`
- Exported assets live in `agentic-browser-ui/src/assets/figma/`
- FIGMA_TOKEN is available in env (set in `~/.zshrc`) — export workflow is unblocked
