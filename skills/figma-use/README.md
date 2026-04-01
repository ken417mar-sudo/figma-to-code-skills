# figma-use

## Goal

Provide the base write-oriented Figma capability for creating, editing,
organizing, and normalizing canvas content.

## When to use

- when a workflow needs to create or edit pages, frames, components, or
  variables
- when cleanup or normalization must happen inside the Figma file
- when another higher-level skill needs structured canvas writes

## When not to use

- when the task only needs read-only design context
- when the user wants code output without changing the Figma file

## Required context

- Figma file reference
- write intent
- relevant node or page target

## Inputs

- Figma file key or URL
- node ids or page targets when applicable
- desired write operation
- optional tech-stack profile if the write supports platform-specific
  cleanup or organization

## Outputs

- modified Figma file structure
- created or updated frames, components, pages, variables, or layout
  settings

## Workflow

1. Identify the exact write target.
2. Confirm the minimum safe write scope.
3. Apply the structured change in Figma.
4. Re-check the affected nodes or screenshots if needed.
5. Hand the updated result to the next workflow step.

## Clarification policy

- ask when a write could affect multiple candidate nodes or shared
  components
- ask when the requested change might alter the source of truth instead
  of only preparing it

## Gotchas

- never make broad structural edits without a clear target
- avoid using write actions when a read-only inspection is enough
- treat component and variable edits as high-impact changes

## Verification

- the intended node or page was changed, not a neighboring one
- the edit reduced ambiguity or moved the workflow forward
- no unintended broad canvas changes were introduced
