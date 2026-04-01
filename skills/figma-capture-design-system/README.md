# figma-capture-design-system

## Goal

Interview the user or team and turn undocumented design-system knowledge
into an explicit reusable implementation reference.

## When to use

- when a project already has rules, but they are mostly implicit
- when implementation quality depends on team knowledge that is not
  written down
- before broad implementation work starts on a partially documented system

## When not to use

- when a complete high-quality spec already exists
- when the main problem is messy Figma structure rather than missing team
  knowledge

## Required context

- tech-stack profile
- project or product scope

## Inputs

- team answers from interview or structured prompts
- any existing docs, component notes, or code references
- tech-stack profile

## Outputs

- explicit rule summary
- implementation conventions
- clarified component expectations
- list of unresolved questions or gaps

## Workflow

1. Confirm the platform profile and project scope.
2. Interview for existing rules, tokens, components, conventions, and
   edge cases.
3. Separate confirmed team knowledge from tentative preferences.
4. Produce a reusable implementation reference.
5. Hand the result to rules, implementation, or verification skills.

## Clarification policy

- ask follow-up questions when a rule changes by platform or framework
- ask when team members describe taste but not an enforceable standard
- ask when component behavior is implied but not clearly defined

## Gotchas

- do not collapse platform-specific rules into a fake universal rule
- do not treat a loose preference as a hard standard
- capture unresolved differences instead of smoothing them over

## Verification

- the captured rules are specific enough to guide implementation
- platform-specific conventions are separated where needed
- unresolved gaps are visible rather than hidden

## Platform notes

The interview flow should branch by target platform.

Examples:

- web: CSS tokens, utility conventions, component API patterns
- iOS: Apple platform conventions, SF Symbols usage, Swift token mapping
- Android: Material alignment, Compose or XML token mapping
