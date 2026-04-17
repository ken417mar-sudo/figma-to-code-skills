# Onboarding

Quick-start for a new thread, new contributor, or any agent picking up this project mid-stream.

## What this project is

A system for turning messy, non-standard Figma design files into production-quality code — reliably, across multiple agents and sessions.

The core problem: most Figma files are not clean sources of truth. States are missing, rules are implicit, assets are inconsistent. This project builds the workflow, rules, and skill prompts needed to handle that reality instead of pretending it away.

## Why we're building it

The goal is a reusable, agent-executable skill set that any Claude or Codex session can pick up and run a Figma-to-code component case through — with consistent quality, explicit checkpoints, and recoverable failures.

Secondary goal: every real component case teaches us something. Recurring failures get promoted into skill gotchas so the next case doesn't repeat them.

## How the three contributors work together

| Contributor | Role |
|---|---|
| User (markun) | Owns design decisions, confirms provisional states, approves closeouts |
| Claude Code | Executes component cases, writes/edits code, manages coordination files, syncs issue #13 |
| Codex | Reviews implementation, runs browser verification, proposes rule tightening, opens PRs |

Communication channel: GitHub issue [#13](https://github.com/ken417mar-sudo/figma-to-code-skills/issues/13) — permanent rolling log, never close.

## Project phases

| Phase | Status | Summary |
|---|---|---|
| Phase 1 | closed | Rewrote all skill READMEs from spec docs into executable agent prompts |
| Phase 2 | closed | Established tech-stack profile, workflow baseline, coordination structure |
| Phase 3 | closed (2026-04-13) | Tab, InputBox, Toolbar — all verified and committed |
| Phase 4 | in progress | `figma-execution-shell` merged; Dialog, AIToolsRow, Sidebar (default-only) all closed |

## Current component status

| Component | Status | Notes |
|---|---|---|
| Tab | closed | 8 variants verified |
| InputBox | closed | 4 states verified |
| Toolbar | closed | 5 states verified |
| Dialog | closed | All axes verified, HYQiHei font deferred |
| AIToolsRow | closed | ToolPill family, hover/active, inline SVG icons |
| Sidebar | closed | Default-only, 6 formal states verified; hover/active/collapsed deferred |

## Component Family Definition

Three trial cards written and replay-validated (2026-04-17). All passed Figma / code / verify three-segment validation. Format confirmed general across provisional-axis (AIToolsRow), pure-formal (Dialog), and composite-formal (Sidebar) cases.

Cards: `experiments/trial-component-family-definition-aitoolsrow.md`, `experiments/trial-component-family-definition-dialog.md`, `experiments/trial-component-family-definition-sidebar.md`

## Current todo

1. Formalize Component Family Definition into `figma-create-design-system-rules` output format (pending user decision on timing)
2. Decide whether Sidebar expands into confirmed interaction / collapsed states
3. Commit / push `codex/sidebar-phase4` in `agentic-browser-ui` (Codex)
4. Shared typography pass for HYQiHei font (deferred non-blocker)

## Quick entry points

| What | Where |
|---|---|
| Component status + node IDs | `coordination/INDEX.md` |
| Execution rules + component status table | `coordination/WORKING-MEMORY.md` |
| Coordination log | [issue #13](https://github.com/ken417mar-sudo/figma-to-code-skills/issues/13) |
| Skill prompts | `skills/*/README.md` |
| Workflow baseline | `inventory/workflow-outline.md` |
| Agent instructions | `CLAUDE.md` (Claude Code) / `AGENTS.md` (Codex) |
| Implementation repo | `/Users/markun/Documents/Codex/Mars/agentic-browser-ui` |
| Figma file | `https://www.figma.com/design/iIbL9V4UrFeORPaM7KVji7` |
