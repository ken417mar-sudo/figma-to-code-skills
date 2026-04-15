# figma-execution-shell

## Goal

Provide a stable execution shell for real Figma-to-code component cases.
Use it to force the same checkpoint order across sessions and agents:
load context, resolve source of truth, pass readiness gates, route to the
right implementation skills, verify, and close out. This skill is a
workflow wrapper — it should point to existing rules and skills instead
of duplicating them.

## When to use

- A real component case is starting and the team wants a consistent
  delivery protocol before implementation begins.
- Multiple agents or sessions may touch the same case and need the same
  readiness gates and closeout shape.
- The case should be run through existing Figma read, write,
  implementation, export, and verification skills in a fixed order.

## When not to use

- The task is only one narrow sub-step already covered by a lower-level
  skill (for example: just export slices, just clean a Figma board, or
  just verify an implementation).
- The work is still pure repo maintenance with no active component case.
- The team only wants to update one existing rule or one gotcha, not run
  a full component workflow.

## Required context

- Shared coordination state:
  - `coordination/INDEX.md`
  - `coordination/WORKING-MEMORY.md`
  - issue `#13`
- Tech-stack profile (`target`, `framework`, `token_format`,
  `verification_surface` when relevant).
- Active component target: node id, section id, or clearly named design
  target.
- Codebase target repo and any existing implementation surface if one
  exists.

## Inputs

- Component case identifier (component name, node id, or Figma URL).
- Current design status:
  - formal component board
  - approved provisional states
  - known missing states or gaps
- Code repo context and current ownership / PR status.
- Optional: prior review findings or deferred non-blockers from earlier
  runs.

## Outputs

- A checkpointed execution plan for the current case.
- The chosen downstream skill path for each phase.
- Explicit blockers when the case is not ready to implement.
- A standardized closeout summary covering:
  - actions taken
  - blockers cleared
  - deferred non-blockers
  - next step
  - whether any recurring failure should be promoted into skill gotchas

## Workflow

1. Load shared context before touching the case:
   - Read `coordination/INDEX.md`, `coordination/WORKING-MEMORY.md`, and
     recent issue `#13` updates.
   - Check `git status` and `gh pr list` so ownership is visible before
     claiming the case.
   - Confirm whether the case is new, already in progress, or being
     resumed.
2. Resolve the source of truth in this order:
   - confirmed project spec or confirmed workflow rules
   - approved formal Figma component board
   - explicitly approved provisional validation states
   - if the above are insufficient, stop and route to
     `figma-capture-design-system` or
     `figma-create-design-system-rules` before implementation
3. Run readiness gates for the case:
   - tech-stack profile is complete enough to shape implementation
   - component target and variant axes are identified
   - required states are either already present or explicitly approved
   - asset needs are known, and export is scheduled before code if real
     design-owned assets are required
   - verification surface is known, or the team explicitly accepts that
     the case cannot be closed yet
4. Route the case to the minimum required downstream skills:
   - use `figma` for read-only design inspection
   - use `figma-ai-implementation-cleanup` if the design file is too
     noisy to implement against safely
   - use `figma-use` for scoped writes such as provisional validation
     boards or canvas normalization
   - use `figma-export-slices` when real assets are needed
   - use `figma-implement-design` for code implementation
   - use `figma-verify-implementation` for post-implementation review
5. Keep the shell active during execution:
   - after each major step, restate whether the case is still blocked,
     implementation-ready, verification-ready, or closeout-ready
   - do not skip a blocked checkpoint just because another downstream
     skill can technically run
6. Close out the case in a fixed shape:
   - summarize what was done and against which design source
   - record blocking or significant mismatches still open
   - separate deferred non-blockers from true completion blockers
   - update `#13` with actions and conclusions
   - update `coordination/WORKING-MEMORY.md` only if the result changes
     stable project memory
   - propose a gotcha update only when the same failure mode looks
     reusable beyond the current component

## Clarification policy

Ask before proceeding when:
- The active component target is ambiguous.
- The case would rely on provisional states that are not explicitly
  approved.
- The formal component board appears incomplete and the missing detail
  changes implementation shape.
- The verification surface is missing, but the team expects the case to
  be closed in the same run.
- Multiple downstream skill paths are plausible and would produce
  materially different output.

Do not ask when:
- The source of truth is clear and the next downstream skill is obvious.
- A reversible, low-risk routing decision is already implied by the
  existing workflow rules.

## Gotchas

- Do not let this shell become a second rule system. It should point to
  existing rule sources, not restate every asset, state, or verification
  rule inline.
- Do not start implementation just because the design target looks
  understandable. The case must still pass readiness gates.
- Do not treat "we can verify later" as equivalent to "the case is
  ready to close." Missing verification may be acceptable for progress,
  but it is not a closed state.
- Do not update `coordination/WORKING-MEMORY.md` for every transient
  action. Only write back stable state that a new session would need.
- Do not promote every case-specific compromise into a shared gotcha.
  Only recurring failure patterns belong in skill maintenance.

## Verification

- The shell clearly identified the source of truth before implementation.
- The case passed or failed readiness gates explicitly; nothing important
  was left implicit.
- Downstream skills were invoked in a sensible order rather than by habit
  or guesswork.
- Closeout separated blockers, deferred non-blockers, and next actions.
- The run produced a reusable protocol shape the next component case can
  follow again.
