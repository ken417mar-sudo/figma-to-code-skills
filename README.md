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

## Start Here

- **New to this project?** Read [coordination/ONBOARDING.md](coordination/ONBOARDING.md) first.
- Current shared coordination:
  [coordination/INDEX.md](coordination/INDEX.md)
- Compact stable memory for new threads:
  [coordination/WORKING-MEMORY.md](coordination/WORKING-MEMORY.md)
- Current workflow baseline:
  [inventory/workflow-outline.md](/Users/markun/Documents/Codex/Mars/figma-to-code-skills/inventory/workflow-outline.md)
- Skill inventory:
  [skills/README.md](/Users/markun/Documents/Codex/Mars/figma-to-code-skills/skills/README.md)

## Repository Layout

- `skills/`: executable skill prompts used by agents
- `inventory/`: workflow rules, templates, and stack profiles
- `coordination/`: shared status, active case memory, and handoff context
- `experiments/`: case writeups, provisional findings, and workflow tests

## Current Focus

Phase 4 is in progress. `figma-execution-shell` is merged, Dialog is
closed, and `AIToolsRow` is the active shell-validation follow-up case.
