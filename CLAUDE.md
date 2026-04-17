# CLAUDE.md

Instructions for Claude Code working in this repository.

## Before touching any file

1. Run `git status` to confirm you are on a feature branch, not `main`.
2. Check open PRs with `gh pr list` to confirm no one else owns the skill
  you are about to edit.
3. Read `coordination/INDEX.md`, `coordination/WORKING-MEMORY.md`, and
  issue `#13` before starting so you have the current shared state.
4. If the skill or area is free, start work. If taken, stop and tell the
  user.

## Branch and commit rules

- Never commit directly to `main`.
- One skill per branch. Name it `skill/<skill-name>`.
- After finishing a skill, push and open a PR immediately so ownership
is visible to Codex and the user.
- Use `gh pr create` to open the PR from the terminal.

## Reading other contributors' work

- To read a PR Codex opened: `gh pr view <number> --comments`
- To read the diff: `gh pr diff <number>`
- To leave a review comment: `gh pr review <number> --comment -b "<text>"`

Use GitHub Issues and PR comments as the communication channel.
Do not ask the user to relay messages to Codex manually.

## Rewriting skill READMEs

This was the main task in Phase 1 and remains the baseline for any skill
README rewrite work.

The goal is to turn each skill README from a specification document into
an executable prompt that Claude or another agent can follow directly.

Rules:

- Write in first-person imperative. The reader is an agent running the
skill.
- Every required section from `inventory/skill-template.md` must be
present.
- The Workflow section must be a numbered list of concrete actions, not
descriptions of intent.
- The Clarification policy must list specific triggers for asking, not
general principles.
- The Gotchas section must contain real failure warnings, not placeholders.
- Platform-aware skills must reference the tech-stack profile explicitly.

## Editing inventory/

Do not edit strategy documents (`skills-strategy-overview.md`,
`workflow-outline.md`) without opening an issue first.

Small updates to `skill-template.md` or `tech-stack-profile.md` are
allowed inside a skill PR when the change is directly required by the
skill you are writing. Include a one-line rationale in the PR description
explaining why the template or profile needed to change.

## Coordination

Cross-skill and cross-PR feedback now lives in issue `#13`, the permanent
coordination log. Check it at the start of each session before claiming a
skill or resuming a case.

Treat issue `#4` as historical context for the Phase 1 rewrite, not as the
current coordination board.

## Skill ownership

Use open PRs plus the shared coordination files to determine ownership.
If a skill has no open PR and issue `#13` does not indicate active work on
it, the skill is available to claim.

- `figma`
- `figma-use`
- `figma-capture-design-system`
- `figma-ai-implementation-cleanup`
- `figma-create-design-system-rules`
- `figma-implement-design`
- `figma-verify-implementation`

Check `gh pr list` before claiming any of these.
