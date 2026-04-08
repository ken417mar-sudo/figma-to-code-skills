# figma-capture-design-system

## Goal

Turn undocumented design-system knowledge into an explicit, reusable
implementation reference by interviewing the user or team. Run this skill
before broad implementation work starts on a partially documented system.

## When to use

- A project already has design rules, but they are mostly implicit or
  spread across team members' heads.
- Implementation quality depends on team knowledge that is not written
  down anywhere.
- A new contributor (human or agent) is about to implement against a
  design system they have not seen before.

## When not to use

- A complete, high-quality spec already exists — use it directly.
- The main problem is messy Figma structure rather than missing team
  knowledge — use `figma-use` to normalize the file first.

## Required context

- Tech-stack profile (`target`, `framework`, `token_format` — see
  `inventory/tech-stack-profile.md`).
- Project or product scope (which surfaces, which components).

## Inputs

- Tech-stack profile.
- Team answers from interview or structured prompts.
- Any existing docs, component notes, or code references the team can
  point to.

## Outputs

- Explicit rule summary covering tokens, components, layout conventions,
  and naming.
- Implementation conventions per platform where they differ.
- Clarified component expectations (states, variants, edge cases).
- List of unresolved questions or gaps — visible, not smoothed over.

## Workflow

1. Confirm the tech-stack profile. If `target`, `framework`, or
   `token_format` are missing, ask for them before proceeding — the
   interview questions branch by platform.
2. Confirm the project scope: which surfaces and components are in scope
   for this capture session.
3. Run the interview. Cover these areas in order, branching by platform:
   - **Tokens**: colors, spacing, typography, radius, shadow — how are
     they defined and consumed? (CSS vars, Tailwind theme, Swift tokens,
     Compose tokens, etc.)
   - **Components**: which components exist, what variants and states do
     they have, what are the edge cases?
   - **Layout conventions**: grid, breakpoints, spacing rules, alignment
     patterns.
   - **Naming**: file naming, layer naming, class/token naming conventions.
   - **Platform-specific rules**: anything that only applies to one target
     (e.g. SF Symbols on iOS, Material alignment on Android, utility-class
     conventions on web).
4. For each answer, classify it as: confirmed standard, tentative
   preference, or unresolved gap. Do not collapse these into one category.
5. Produce the implementation reference. Separate platform-specific
   sections where the rules differ. List unresolved gaps at the end.
6. Hand the reference to `figma-create-design-system-rules`,
   `figma-implement-design`, or `figma-verify-implementation` as the next
   step.

## Clarification policy

Ask follow-up questions when:
- A rule is described differently for different platforms — ask which
  platform the rule applies to and whether the others have a different
  rule.
- A team member describes a taste or preference ("we like it to feel
  light") rather than an enforceable standard — ask what the concrete
  implementation rule is.
- Component behavior is implied but not clearly defined (e.g. "the button
  has a hover state" without specifying the exact visual change) — ask for
  the specific value or behavior.
- The product appears to need interaction states that the current
  component board does not fully show (e.g. hover-close, focus, pressed,
  disabled, error, loading) — ask which states are truly required and
  whether they belong in a provisional validation layer.

Do not ask when:
- The rule is already specific and platform-unambiguous.
- The gap is acknowledged and will be listed as unresolved — record it
  and move on.

## Gotchas

- Do not collapse platform-specific rules into a fake universal rule.
  Web flex conventions are not the same as SwiftUI stack conventions even
  if they look similar at a glance.
- Do not treat a loose preference as a hard standard. Mark it as
  tentative and flag it for the team to confirm.
- Capture unresolved differences instead of smoothing them over. A hidden
  gap will surface as a bug during implementation.
- If the team has existing code, ask to see a representative component
  file — actual code reveals conventions that people forget to mention in
  interviews.
- Do not assume that common product affordances belong in the canonical
  component set just because they are common elsewhere. Confirm whether a
  missing interaction state is intentionally absent, or should be added as
  a provisional validation state first.

## Verification

- The captured rules are specific enough to guide implementation without
  further guessing.
- Platform-specific conventions are separated where the platforms differ.
- Unresolved gaps are listed explicitly at the end of the reference.
- No tentative preference has been promoted to a hard standard without
  explicit team confirmation.

## Platform notes

The interview flow branches by `target` from the tech-stack profile.

- **web**: CSS token format, utility-class conventions (Tailwind, CSS
  modules, etc.), component API patterns, breakpoint rules.
- **ios**: Apple platform conventions, SF Symbols usage, SwiftUI vs UIKit
  token mapping, safe area and dynamic type handling.
- **android**: Material alignment, Compose vs XML token mapping, density
  bucket rules, adaptive layout conventions.
