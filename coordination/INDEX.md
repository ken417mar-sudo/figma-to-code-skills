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
| Dialog section | `1922:32133` |
| Dialog core block | `1922:31967` |

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
Provisional boards confirmed:
- NavIcon disabled (`1872:10395`): opacity 0.3 on button wrapper ✓
- Bookmark bookmarked + URLBar focused (`1873:10395`): icons correct ✓
Deferred non-blocker: `border border-[0.5px]` redundancy in `urlFocused`.

### Dialog — closed
Phase 4 validation case for `figma-execution-shell`. Closed 2026-04-16.
All axes implemented: CloseIcon × 4 variants, DialogButton × 3 types + hover (all 6 type×state combos), ButtonGroup × 3 layouts, DialogContent × 3 variants.
Fixes applied: close hover prop-driven, image-content branch, image spacing, image circle close, local asset (dialog-image-placeholder@1x.png), text button hover (#999→#333).
Commits: `b5c9f24`, `b167b79`, `763239b` in agentic-browser-ui (branch: `codex/dialog-phase4-closeout`).
Deferred non-blocker: HYQiHei font loading — shared typography pass, not Dialog-specific.
Provisional-state promotion: no provisional states were used; all implementation sourced from formal Figma component board.

### AIToolsRow — closed
Phase 4 shell follow-up case. Closed 2026-04-17.
All axes implemented: ToolPill (text) × 3 states, ToolPill (icon-only) × 3 states.
Provisional state frames rebuilt correctly at control level (not row-level).
Commits in agentic-browser-ui (merged via PR #3):
- `a97e009` — initial implementation
- `a922a91` — inline SVG icons for currentColor, verify surface 704px
- `7721405` — Skill icon BOOLEAN_OPERATION fix (stroke=currentColor)
Deferred: active state remains proposal-level (not yet formally confirmed).
Gotchas promoted: BOOLEAN_OPERATION mask SVG fix, verify surface width rule, promotion gate on user instruction.

### Sidebar — closed (2026-04-17)
Phase 4 follow-up case. Formal default-only pass completed by Claude Code.
All 6 formal states passed (V1 Sidebar expanded, V2 QuickActionItem default, V5 ProjectItem default, V7 HistoryItem default, V9 SidebarHeader default, V10 UserInfo default).
Section-header padding bug fixed: Projects `pl-[12px] pr-[4px]`, History `px-[12px]`.
Implementation is now committed, pushed, and visible in `agentic-browser-ui` PR #4 (`codex/sidebar-phase4`).
Deferred non-blockers: SVG icon color hardcoding (theme-reactive未确认); hover/active/collapsed states unconfirmed.
Verify card: `experiments/trial-component-family-definition-sidebar.md`

### BrowserResultPage / AssistantSidebarPanel — closed (2026-04-21)
Composite family case. Source node: `1708:30204`.
Implementation merged via PR #5 (agentic-browser-ui) and PR #27 (figma-to-code-skills).
Remaining provisional: collapsed launcher path (`1708:30243`); panel-specific chip/composer states deferred.

### WorkspacePage / TaskChatPanel — closed (2026-04-22)
Phase 6 Repeatability case. Composite family.
Implementation in agentic-browser-ui PR #6 (OPEN, MERGEABLE).
figma-to-code-skills PRs #28 and #29 merged into main (`7624dbe`).
Live cards:
- `cases/component-family-definition-workspace-page.md`
- `cases/component-family-definition-task-chat-panel.md`

## Open PRs

| Repo | PR | Branch | Status |
|---|---|---|---|
| agentic-browser-ui | #6 | codex/workspace-page-phase6 | OPEN, MERGEABLE |
| figma-to-code-skills | #17 | skill/figma-use-gotchas | OPEN — decide: merge or close as superseded |

## Next Recommended Action

1. Merge agentic-browser-ui PR #6 to close WorkspacePage implementation side.
2. Decide PR #17: if write-path gotchas are already in main, close as superseded; otherwise rebase and merge.
3. Start Phase B — Existing-rule capture validation using agentic-browser-ui as baseline.

## Source-of-Truth Notes

- Skill rules live in `skills/*/README.md` — authoritative for agent behavior
- Workflow rules live in `inventory/workflow-outline.md`
- CSS tokens live in `agentic-browser-ui/src/index.css`
- Exported assets live in `agentic-browser-ui/src/assets/figma/`
- FIGMA_TOKEN is available in env (set in `~/.zshrc`) — export workflow is unblocked
