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
| User (markun) | Final decision-maker on priorities, design decisions, provisional-state confirmation, and closeouts |
| Claude Code | Executes component cases, writes/edits code, manages coordination files, and contributes explicitly attributed suggestions |
| Codex | Reviews implementation, runs browser verification, proposes rule tightening, and contributes explicitly attributed suggestions |

Communication channel: GitHub issue [#13](https://github.com/ken417mar-sudo/figma-to-code-skills/issues/13) — permanent rolling log, never close.

Decision protocol:
- keep suggestion ownership explicit (`user`, `Claude Code`, `Codex`)
- when posting recommendations through the shared GitHub account, prefix
  them with the agent name, for example `Codex:` or `Claude Code:`
- do not collapse an individual recommendation into "the project thinks"
  until contributors have aligned on it
- once a recommendation or objection is raised, sync it to `#13` by
  default so the shared log reflects not just actions, but advice and
  pending decisions as well

## Project phases

| Phase | Status | Summary |
|---|---|---|
| Phase 1 | closed | Rewrote all skill READMEs from spec docs into executable agent prompts |
| Phase 2 | closed | Established tech-stack profile, workflow baseline, coordination structure |
| Phase 3 | closed (2026-04-13) | Tab, InputBox, Toolbar — all verified and committed |
| Phase 4 | closed (2026-04-20) | `figma-execution-shell` merged; Dialog, AIToolsRow, Sidebar (default-only) all closed |
| Phase 5 | closed (2026-04-20) | BrowserResultPage + AssistantSidebarPanel composite family case merged and formally closed |
| Phase 6 | planning | next step is capability validation beyond the proven web component loop |

## Current component status

| Component | Status | Notes |
|---|---|---|
| Tab | closed | 8 variants verified |
| InputBox | closed | 4 states verified |
| Toolbar | closed | 5 states verified |
| Dialog | closed | All axes verified, HYQiHei font deferred |
| AIToolsRow | closed | ToolPill family, hover/active, inline SVG icons |
| BrowserResultPage / AssistantSidebarPanel | closed | Composite family case; collapsed launcher deferred |

## Component Family Definition

Three historical validation cards were written and replay-validated
(2026-04-17). All passed Figma / code / verify three-segment validation.
The format is now formalized as the required component-scoped output of
`figma-create-design-system-rules` when the family boundary is clear.
The three samples remain in `experiments/` as validation evidence across
provisional-axis (AIToolsRow), pure-formal (Dialog), and
composite-formal (Sidebar) cases.

Cards: `experiments/trial-component-family-definition-aitoolsrow.md`, `experiments/trial-component-family-definition-dialog.md`, `experiments/trial-component-family-definition-sidebar.md`

## Current todo

1. Run an existing-rule capture pass first on `agentic-browser-ui`, because that real project baseline is already available
2. Run one more fresh component-scoped case to prove workflow repeatability
3. Reopen collapsed launcher (`1708:30243`) or another missing state as a provisional-promotion validation case
4. Validate sketch / low-fi gap-filling or non-web profile breadth only when a real project need appears
5. Shared typography pass for HYQiHei font remains a deferred cross-case non-blocker

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
