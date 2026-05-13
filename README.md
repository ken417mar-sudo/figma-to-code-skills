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

Phase K closed (2026-05-13). All PRs merged — no open PRs in either repo.

Completed phases: A–K. Components closed: Tab, InputBox, Toolbar, Dialog,
AIToolsRow, Sidebar, BrowserResultPage/AssistantSidebarPanel, WorkspacePage,
TaskResultPage, FileListCard, NavigationMenu, SearchBar, ModelCard,
TopTabBar (Phase I+J), UpgradeDialog.

No active track. Next candidates:
- BookmarkItem (`1708:30231~30233`) — lightweight layout case, low priority
- UpgradeDialog default/complete states

See [coordination/INDEX.md](coordination/INDEX.md) for full phase history
and [coordination/WORKING-MEMORY.md](coordination/WORKING-MEMORY.md) for
compact current state.
