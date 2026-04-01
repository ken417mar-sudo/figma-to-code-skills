# figma-verify-implementation

## Goal

Compare implemented UI against Figma, annotate mismatches, and classify
which differences matter enough to fix or feed back into the skill set.

## When to use

- after an implementation pass
- when the team needs objective comparison instead of visual guessing
- when recurring drift between design and code should be captured as
  gotchas

## When not to use

- before there is a runnable or inspectable implementation surface
- when the design target itself is still unresolved

## Required context

- tech-stack profile
- verification surface
- design target
- implementation target

## Inputs

- Figma frame or node
- built implementation surface
- tech-stack profile
- optional project severity rubric for mismatch scoring

## Outputs

- annotated mismatch report
- severity or priority classification
- implementation feedback
- candidate gotchas for recurring failure patterns

## Key rule

Verification should follow a platform-specific path.

Examples:

- web: browser screenshot, local app, Storybook, or other web preview
- iOS: simulator screenshot or other iOS preview surface
- Android: emulator screenshot or other Android preview surface

## Workflow

1. Confirm the design target and implementation surface.
2. Collect platform-appropriate screenshots or inspection context.
3. Compare structure, spacing, typography, states, and component behavior.
4. Classify mismatches by impact.
5. Feed important findings back into code, rules, or skill gotchas.

## Clarification policy

- ask when the implementation surface does not clearly correspond to the
  target design
- ask when a difference may be intentional because of platform-specific
  conventions
- ask when the severity rubric is unclear

## Gotchas

- do not treat every visual delta as equally important
- do not ignore structural mismatches just because the screenshot looks
  close
- do not compare against the wrong state, breakpoint, or platform target

## Verification

- the comparison uses the correct platform path
- mismatches are prioritized instead of dumped as noise
- recurring failure patterns can be turned into skill gotchas
