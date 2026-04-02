# figma-verify-implementation

## Goal

Compare implemented UI against the Figma design, annotate mismatches,
classify which differences matter enough to fix, and feed recurring
failure patterns back into the skill set as gotchas.

## When to use

- After an implementation pass — the code exists and can be inspected or
  rendered.
- The team needs an objective comparison instead of visual guessing.
- Recurring drift between design and code should be captured as gotchas
  for future runs.

## When not to use

- Before there is a runnable or inspectable implementation surface — there
  is nothing to compare against yet.
- The design target itself is still unresolved — verify the design first,
  then implement, then verify the implementation.

## Required context

- Tech-stack profile (`target`, `framework`, `verification_surface` — see
  `inventory/tech-stack-profile.md`).
- Design target: the Figma frame or node that was implemented.
- Implementation target: the rendered surface to compare against.

## Inputs

- Figma frame or node (URL, file key, or node id).
- Built implementation surface:
  - **web**: browser screenshot, local dev server URL, Storybook story, or
    other web preview.
  - **ios**: simulator screenshot or iOS preview surface.
  - **android**: emulator screenshot or Android preview surface.
- Tech-stack profile.
- Optional: project severity rubric for mismatch scoring (e.g. spacing
  delta threshold, color tolerance).

## Outputs

- Annotated mismatch report listing each difference with location and
  description.
- Severity or priority classification for each mismatch (blocking,
  significant, minor, intentional).
- Implementation feedback: specific changes needed to close each blocking
  or significant mismatch.
- Candidate gotchas: recurring failure patterns worth adding to the
  relevant skill's Gotchas section.

## Workflow

1. Confirm the design target and implementation surface. If either is
   ambiguous, ask before comparing.
2. Fetch the Figma design context:
   - Call `get_design_context` on the target node for layout, tokens, and
     component structure.
   - Call `get_screenshot` to get the reference design image.
3. Collect the implementation screenshot or inspection context using the
   platform-appropriate path (see Inputs).
4. Compare the two surfaces across these dimensions in order:
   - **Structure**: component hierarchy, nesting, element count.
   - **Spacing**: padding, margin, gap values against token or pixel spec.
   - **Typography**: font family, size, weight, line height, color.
   - **Color**: fills, borders, shadows against token values.
   - **States**: hover, focus, disabled, error, empty — are all required
     states present?
   - **Component behavior**: interactive elements, scroll, overflow.
5. Classify each mismatch:
   - **Blocking**: breaks functionality or violates a hard design rule.
   - **Significant**: visible and inconsistent with the spec, should fix.
   - **Minor**: small delta within acceptable tolerance.
   - **Intentional**: a known platform-specific deviation (document it).
6. Produce the mismatch report. For each blocking or significant item,
   include the specific fix needed.
7. Identify any recurring failure patterns across this and prior runs.
   For each pattern, propose a gotcha entry for the relevant skill's
   README.

## Clarification policy

Ask before proceeding when:
- The implementation surface does not clearly correspond to the target
  design (e.g. wrong breakpoint, wrong state, wrong platform build).
- A difference may be intentional because of platform-specific conventions
  (e.g. iOS safe area insets, Android status bar handling) — ask whether
  to classify it as intentional before marking it as a mismatch.
- The severity rubric is unclear and the project has not defined
  acceptable tolerances — ask what threshold separates minor from
  significant.

Do not ask when:
- The mismatch is clearly unintentional and the correct value is
  specified in the design or token system.
- The difference is structural (wrong component hierarchy) — always
  classify as blocking.

## Gotchas

- Do not treat every visual delta as equally important. A 1px spacing
  difference is not the same as a missing interactive state.
- Do not ignore structural mismatches just because the screenshot looks
  close. A wrong component hierarchy will break under real content and
  state changes.
- Do not compare against the wrong state, breakpoint, or platform target.
  Verify the correct build variant before starting.
- Platform-specific deviations (safe areas, status bars, density
  differences) are not bugs — classify them as intentional and document
  them.
- Token mismatches (wrong color value, wrong spacing unit) are always at
  least significant — they indicate the implementation is not using the
  design system correctly.

## Verification

- The comparison uses the correct platform path and the correct build
  variant.
- Mismatches are prioritized by severity, not dumped as an undifferentiated
  list.
- Intentional platform deviations are documented, not silently ignored.
- Recurring failure patterns are identified and proposed as gotcha entries
  for the relevant skill.
