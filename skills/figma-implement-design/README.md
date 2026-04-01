# figma-implement-design

## Goal

Turn Figma design context plus confirmed rules into implementation code
for the declared platform and framework.

## When to use

- when a target design or component should be translated into production
  code
- when implementation should follow both the design and the project rule
  set
- when platform profile is known and downstream code output is the goal

## When not to use

- when the main task is still clarifying rules or cleaning the Figma file
- when the platform profile is missing and would materially change the
  output

## Required context

- tech-stack profile
  - `target`: `web` | `ios` | `android`
  - `framework`: for example `react`, `swiftui`, `compose`
  - `token_format`: for example `css-vars`, `swift-tokens`,
    `compose-tokens`
- design context
- rule source

## Inputs

- Figma frame, component, or node
- project spec or captured rules
- tech-stack profile
- optional codebase conventions or existing component references

## Outputs

- implementation code
- explicit mapping notes for major layout or component choices
- unresolved questions when design meaning is still ambiguous

## Workflow

1. Confirm the target platform profile and rule source.
2. Read the smallest useful Figma context for the target.
3. Map layout, tokens, and components to platform-appropriate code
   patterns.
4. Prefer existing code components and rules where available.
5. Produce implementation output and surface any unresolved ambiguity.

## Clarification policy

- ask when platform profile is missing or incomplete
- ask when component boundaries are unclear
- ask when interaction behavior or content hierarchy changes the code
  shape
- ask when an implementation choice would be expensive to undo

## Gotchas

- do not silently default to web
- do not output code that ignores the declared framework conventions
- do not invent reusable rules during implementation when they should be
  confirmed first
- do not optimize only for pixel similarity if the structural component
  model becomes worse

## Key rule

This skill should not guess the target platform when platform changes the
implementation shape.

## Verification

- the output matches the declared target platform and framework
- the code respects existing rules before inferred rules
- the result is structurally sane, not only visually similar
