# Coordination Index

Single entry point for all three contributors (user, Claude, Codex).
Update this file when phase, repos, or active work changes.

## Stable Memory

- Working summary for new threads:
  `/Users/markun/Documents/Codex/Mars/figma-to-code-skills/coordination/WORKING-MEMORY.md`

## Current Phase

Phase 3 closed (2026-04-13) — Tab, InputBox, Toolbar all verified and committed.
Phase 4 in progress (2026-04-15) — `figma-execution-shell` merged; Dialog case is in visual verify / fix.

## Active Repos

| Repo | Purpose |
|---|---|
| `figma-to-code-skills` | skill rules, gotchas, workflow inventory |
| `agentic-browser-ui` | implementation target (React + Tailwind) |

Local paths:
- `/Users/markun/Documents/Codex/Mars/figma-to-code-skills`
- `/Users/markun/Documents/Codex/Mars/agentic-browser-ui`

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
| InputBox | `1708:30342` |
| 页签 (8 variants) | `1714:977`, `1714:983`, `1714:990`, `1714:1001`, `1720:89968`, `1720:89980`, `1720:89992`, `1720:90000` |
| 关闭 Hover=off | `1714:1013` |
| 关闭 Hover=on | `1714:1017` |
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

### Dialog — in progress
Phase 4 validation case for the merged `figma-execution-shell`.
`figma-execution-shell` skeleton merged via PR `#18`; shell v2 gate tightening merged via PR `#19`.

Current implementation status:
- Dialog structure and variant axes are implemented in `agentic-browser-ui`
- close hover forcing and image-content branch bugs were fixed
- work has moved into visual fidelity verification against Figma

Current open gaps:
- horizontal image dialog still uses the text-dialog spacing shell; image variant spacing is too loose vs Figma
- button-type verify cards in `App.tsx` are still handwritten examples, not the real `DialogButton` implementation branches

Current status should be treated as:
- implementation-complete
- verification-partial

## Next Recommended Action

Finish Dialog visual verify / fix, then close the case and only after that decide whether shell / verify-quality needs one more focused patch.

## Source-of-Truth Notes

- Skill rules live in `skills/*/README.md` — authoritative for agent behavior
- Workflow rules live in `inventory/workflow-outline.md`
- CSS tokens live in `agentic-browser-ui/src/index.css`
- Exported assets live in `agentic-browser-ui/src/assets/figma/`
- FIGMA_TOKEN is available in env (set in `~/.zshrc`) — export workflow is unblocked
