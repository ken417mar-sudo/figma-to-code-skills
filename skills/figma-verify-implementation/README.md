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
- Verification status for the case:
  - `coverage-complete`
  - `visual-verification-complete`
  - `partial`
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
   - Use the real implementation branch, not a handwritten stand-in built
     only for verification.
   - If the target variant depends on exported assets (especially images
     or media), verify with the real asset rather than a placeholder.
   - Do not rely on temporary signed Figma CDN URLs in the implementation
     or verification surface. Export the asset into the repo first so the
     check is stable and repeatable.
4. Compare the two surfaces across these dimensions in order:
   - **Structure**: component hierarchy, nesting, element count.
   - **Spacing**: padding, margin, gap values against token or pixel spec.
   - **Typography**: font family, size, weight, line height, color, and
     whether the intended font is actually loaded / registered in the
     runtime surface rather than silently falling back.
   - **Color**: fills, borders, shadows against token values.
   - **States**: hover, focus, disabled, error, empty — are all required
     states present?
   - **Combined variant matrices when present**: if the component set is
     organized as combinations such as `type × state`, verify the
     intended combinations explicitly instead of checking only one axis
     and assuming the cross-product is covered.
   - **Component behavior**: interactive elements, scroll, overflow.
   - **Media / overlays when present**: image fit, crop, mask, overlay
     controls, and any variant-specific shell differences from text
     versions.
5. Classify each mismatch:
   - **Blocking**: breaks functionality or violates a hard design rule.
   - **Significant**: visible and inconsistent with the spec, should fix.
   - **Minor**: small delta within acceptable tolerance.
   - **Intentional**: a known platform-specific deviation (document it).
6. Decide the verification status:
   - `coverage-complete`: all intended variant axes are rendered through
     real implementation branches or explicitly deferred, but a full
     visual check is still outstanding.
   - `visual-verification-complete`: the rendered implementation has been
     visually checked against the target node and no blocking or
     significant mismatches remain.
   - `partial`: required axes are still missing, a placeholder is still
     masking the real target, or blocking/significant mismatches are
     still open.
7. Produce the mismatch report. For each blocking or significant item,
   include the specific fix needed.
8. Identify any recurring failure patterns across this and prior runs.
   For each pattern, propose a gotcha entry for the relevant skill's
   README.

## Clarification policy

Ask before proceeding when:
- The implementation surface does not clearly correspond to the target
  design (e.g. wrong breakpoint, wrong state, wrong platform build).
- A difference may be intentional because of platform-specific conventions
  (e.g. iOS safe area insets, Android status bar handling) — ask whether
  to classify it as intentional before marking it as a mismatch.
- The implementation includes interaction states or affordances that are
  not present in the formal component board, and it is unclear whether
  they were explicitly approved as product-layer behavior — ask before
  classifying them as mismatches.
- The severity rubric is unclear and the project has not defined
  acceptable tolerances — ask what threshold separates minor from
  significant.
- The case is about to be marked as visually verified, but the current
  surface still uses placeholders, hand-built stand-ins, or otherwise
  avoids the real implementation branch.
- A combined matrix (for example `type × state`) is being treated as
  "implemented" or "deferred" in aggregate, but the exact combinations
  have not been named.

Do not ask when:
- The mismatch is clearly unintentional and the correct value is
  specified in the design or token system.
- The difference is structural — classify it based on impact: blocking if
  it affects reusability, state correctness, layout stability, or
  behavior; significant if it is a meaningful deviation without functional
  impact; intentional if it is a known platform-specific adaptation.

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
- Enumerate all variant axes from the component set before building the
  verification surface. A grid that covers only a subset of axes will miss
  entire classes of rendering bugs. A missing axis is itself a blocking
  mismatch.
- A variant axis is not actually covered until the verification surface
  drives the real implementation branch for that axis. Listing the axis
  in notes or drawing a lookalike verification card is not enough.
- Verify cards must render the real implementation path. Handwritten
  stand-ins can help explain intent, but they do not prove the component
  actually matches Figma.
- Media or image variants should be checked with the real exported asset,
  not a placeholder. Otherwise fit, crop, masking, or overlay-control
  bugs will stay hidden until later.
- A temporary signed Figma asset URL is not a stable verification asset.
  If the surface depends on an expiring CDN link, classify the case as
  partial until the asset is exported into the repo or another stable
  source.
- Do not assume a media/image variant can reuse the same spacing shell as
  a text variant. Re-check outer padding, internal wrappers, and overlay
  controls independently for the media branch.
- Overlay controls (for example a circular close button over an image) are
  easy to miss if verification only checks structure or text-based
  variants first. Inspect image/media branches explicitly.
- Stateful stroke or border treatments that change box geometry between
  states (e.g. adding a border only in selected state) are a significant
  mismatch. The default state must pre-allocate the same stroke space, or
  the implementation must use a non-layout-affecting layer such as inset
  shadow or outline.
- Do not approve icon sizing just because the exported SVG file "looks"
  correct in isolation. Verify the icon against its in-component geometry
  in Figma. If the implementation sized the icon from raw asset canvas
  dimensions instead of the component's icon frame and glyph bounds,
  classify that as a significant mismatch.
- Do not assume a font token in code means the typography hierarchy is
  correct in the rendered surface. If the intended font family is not
  actually loaded, the fallback rendering can collapse title/body
  contrast and should be classified as a significant mismatch.
- If the design defines a matrix such as `type × state`, do not mark the
  matrix verified unless each intended combination is either explicitly
  exercised or explicitly deferred. A vague note like "hover deferred" is
  not enough if some hover combinations are supposed to ship now.

## Verification

- The comparison uses the correct platform path and the correct build
  variant.
- The verification surface uses the real implementation branch and the
  real exported assets for the target variant where applicable.
- Typography verification confirmed real rendered hierarchy, not just
  token names present in source.
- Mismatches are prioritized by severity, not dumped as an undifferentiated
  list.
- The final result clearly distinguishes `coverage-complete` from
  `visual-verification-complete`.
- Intentional platform deviations are documented, not silently ignored.
- Recurring failure patterns are identified and proposed as gotcha entries
  for the relevant skill.
