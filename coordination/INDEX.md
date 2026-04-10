# Coordination Index

Single entry point for all three contributors (user, Claude, Codex).
Update this file when phase, repos, or active work changes.

## Current Phase

Phase 2 — component implement → verify loop (InputBox)

## Active Repos

| Repo | Purpose |
|---|---|
| `figma-to-code-skills` | skill rules, gotchas, workflow inventory |
| `agentic-browser-ui` | implementation target (React + Tailwind) |

Local paths:
- `/Users/markun/Documents/Codex/Mars/figma-to-code-skills`
- `/Users/markun/Documents/Codex/Mars/agentic-browser-ui`

## Active Issues

| Issue | Scope | Status |
|---|---|---|
| [#12 — InputBox implement→verify](https://github.com/ken417mar-sudo/figma-to-code-skills/issues/12) | InputBox component case | open |

Closed:
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

## Current State

### Tab — closed
All 8 variants verified. close-off/close-on SVGs from source export wired. No gaps.

### InputBox — in progress
- Initial implementation: `agentic-browser-ui/src/components/InputBox.tsx` (commit `0acbf47`)
- 4 icons exported: `inputbox-ic`, `inputbox-model-toggle`, `inputbox-voice`, `inputbox-send`
- Known gaps: interactive states (focus ring, button hover) not yet implemented
- Open questions: see issue #12

## Next Recommended Action

1. Codex: review InputBox visual vs Figma, answer 3 questions in issue #12
2. Claude: implement interactive states after Codex confirms layout is acceptable
3. Both: update this file when InputBox case closes

## Source-of-Truth Notes

- Skill rules live in `skills/*/README.md` — authoritative for agent behavior
- Workflow rules live in `inventory/workflow-outline.md`
- CSS tokens live in `agentic-browser-ui/src/index.css`
- Exported assets live in `agentic-browser-ui/src/assets/figma/`
- FIGMA_TOKEN is available in env (set in `~/.zshrc`) — export workflow is unblocked
