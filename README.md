# Figma to Code Skills

This repository holds the executable prompts, workflow rules, gotchas,
and coordination memory for the Figma-to-code system we are refining
across real component cases.

## What This Repo Does

The project is built to make messy or non-standard design files
implementable in code without pretending the design draft is already a
clean source of truth.

Default operating model:

- prefer an existing project spec or design-system rule set when one
  exists
- treat the active Figma file as implementation input, not automatic
  canonical truth
- extract and confirm missing rules before broad implementation
- route real assets through export instead of hand-drawing substitutes
- verify implemented UI against Figma and record recurring failures as
  reusable gotchas

## Decision Protocol

This repo is built collaboratively by the user, Claude Code, and Codex.

- attribute every recommendation to its source unless it has already
  become an explicit team consensus
- when posting recommendations or opinions under the shared GitHub
  account, prefix them with the agent name, for example `Codex:` or
  `Claude Code:`
- treat agent suggestions and reviews as inputs, not final decisions
- only mark something as shared consensus after the contributors have
  aligned on it
- the user makes the final decision on priority, scope, and closeout
- sync recommendation or opinion changes into issue `#13` by default so
  advice does not stay trapped in a single chat or PR

## Start Here

- **New to this project?** Read [coordination/ONBOARDING.md](coordination/ONBOARDING.md) first.
- Current shared coordination:
  [coordination/INDEX.md](coordination/INDEX.md)
- Compact stable memory for new threads:
  [coordination/WORKING-MEMORY.md](coordination/WORKING-MEMORY.md)
- Current workflow baseline:
  [inventory/workflow-outline.md](inventory/workflow-outline.md)
- Skill inventory:
  [skills/README.md](skills/README.md)

## Repository Layout

- `skills/`: executable skill prompts used by agents
- `inventory/`: workflow rules, templates, and stack profiles
- `coordination/`: shared status, active case memory, and handoff context
- `experiments/`: case writeups, provisional findings, and workflow tests

## Current Focus

Phase 6 Repeatability complete (2026-04-22). All 8 component cases closed: Tab, InputBox, Toolbar, Dialog, AIToolsRow, Sidebar, BrowserResultPage/AssistantSidebarPanel, WorkspacePage/TaskChatPanel.

Phase B next — Existing-rule capture validation:

1. merge agentic-browser-ui PR #6 (WorkspacePage) to close the implementation side
2. decide figma-to-code-skills PR #17 (figma-use write-path gotchas): merge or close as superseded
3. run existing-rule capture on agentic-browser-ui as baseline — turn implicit rules into an explicit rule artifact, then run one implementation task that must use those captured rules
4. validate provisional-to-formal promotion path (collapsed launcher `1708:30243`) when ready
5. validate sketch / low-fidelity gap-filling or platform breadth only when a real project need appears
