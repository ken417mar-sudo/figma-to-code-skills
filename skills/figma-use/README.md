# figma-use

## Goal

Execute write operations inside a Figma file — create, edit, organize, and
normalize canvas content. Use this skill whenever a workflow needs to
modify the Figma file, not just read from it.

## When to use

- A workflow needs to create or edit pages, frames, components, or
  variables in the Figma canvas.
- Cleanup or normalization must happen inside the Figma file (e.g.
  renaming layers, fixing auto-layout, applying tokens).
- A higher-level skill (generate-design, implement-design, etc.) needs
  structured canvas writes as a sub-step.

## When not to use

- The task only needs read-only design context — use `figma` instead.
- The user wants code output without changing the Figma file.

## Required context

- A Figma file key or URL.
- A clear write intent (what to create, edit, or normalize).
- The target node id, page name, or frame reference when the write is
  scoped to a specific location.

## Inputs

- Figma file key or URL.
- Node ids or page targets when the write is not at the root level.
- Description of the desired write operation.
- Optional: tech-stack profile when the write supports platform-specific
  cleanup or organization (e.g. naming conventions tied to a component
  library).

## Outputs

- Modified Figma file structure.
- Created or updated frames, components, pages, variables, or layout
  settings.

## Workflow

1. Identify the exact write target — resolve the node id or page name
   before writing. If the target is ambiguous, call `get_metadata` to
   inspect the tree first.
2. Determine the minimum safe write scope. Prefer scoped edits over
   broad canvas operations.
3. Execute the write via `use_figma` with a JavaScript snippet targeting
   the resolved node.
4. Verify the result: call `get_screenshot` or `get_metadata` on the
   affected node to confirm the change landed correctly.
5. Hand the updated node reference or file state to the next workflow
   step.

## Clarification policy

Ask before proceeding when:
- The write could affect multiple candidate nodes with similar names —
  ask the user to confirm the correct target.
- The requested change would alter a shared component or master style
  that other frames depend on — ask whether the intent is to change the
  source or only a local instance.
- The write scope is unclear (e.g. "clean up the file" without a
  specified frame) — ask for a specific target.

Do not ask when:
- A single unambiguous node id is provided and the write intent is clear.
- The write is purely additive (creating a new frame or page) with no
  risk of overwriting existing content.

## Gotchas

- `use_figma` executes JavaScript via the Figma Plugin API. Syntax errors
  in the snippet will silently fail or produce partial results — always
  verify after writing.
- For the font "Inter", the style name is `"Semi Bold"` (with a space),
  not `"SemiBold"`. Wrong font style names cause silent fallback to the
  default weight.
- `figma.currentPage` cannot be set directly. Use
  `await figma.setCurrentPageAsync(page)` to switch pages.
- Component and variable edits are high-impact — they propagate to every
  instance. Confirm scope before editing a master component.
- Do not use write actions when a read-only inspection is enough. Writes
  that touch shared components can break other frames in the file.
- Before creating new components, call `search_design_system` to check
  whether an existing component can be reused via
  `importComponentByKeyAsync`.

## Verification

- The intended node or page was changed, not a neighboring one (confirm
  via screenshot or metadata check).
- No unintended broad canvas changes were introduced.
- The edit moved the workflow forward — reduced ambiguity, created the
  required structure, or normalized the target correctly.
