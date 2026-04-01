# figma-create-design-system-rules

## Goal

Generate or extend an implementation-oriented rule set when a project
does not already have a complete usable spec.

## When to use

- when a project has no formal design-system rules
- when a spec exists but does not cover enough detail to implement safely
- when we need a draft rule set extracted from Figma for human review

## When not to use

- when a strong existing spec already covers the implementation target
- when the task is only to capture undocumented rules that already exist
  in the team

## Required context

- tech-stack profile
- existing spec status
- target Figma design context

## Inputs

- Figma frames or components
- any existing design-system notes
- tech-stack profile
- known project conventions

## Outputs

- editable rule draft
- inferred patterns for layout, spacing, typography, color, component
  structure, and implementation conventions
- explicit list of unknowns or low-confidence inferences

## Workflow

1. Check whether an existing spec already covers the needed scope.
2. Preserve confirmed rules and identify only the missing areas.
3. Infer a first-pass rule set from the design draft and project context.
4. Mark ambiguous or low-confidence rules clearly.
5. Produce a draft meant for human revision before implementation.

## Clarification policy

- ask when inferred rules may conflict with known project standards
- ask when a repeated pattern may be a one-off exception instead of a
  true rule
- ask when platform profile is missing and it changes implementation
  conventions

## Gotchas

- do not replace a valid existing spec with a guessed one
- do not silently promote accidental visual repetition into a standard
- keep inferred rules editable and explicitly provisional

## Verification

- the rule set is profile-aware
- existing confirmed rules are preserved
- inferred rules are specific enough to guide implementation
- ambiguity is surfaced instead of hidden
