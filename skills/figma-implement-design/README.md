# figma-implement-design

## Goal

Turn Figma design context plus confirmed rules into implementation code
for the declared platform and framework. Do not guess the platform — if
the profile is missing and it changes the output shape, ask first.

## When to use

- A target design or component should be translated into production code.
- Implementation must follow both the design and the project rule set.
- The platform profile is known and code output is the goal.

## When not to use

- The main task is still clarifying rules — use
  `figma-create-design-system-rules` first.
- The Figma file is too noisy to implement against — use
  `figma-ai-implementation-cleanup` first.
- The platform profile is missing and it would materially change the
  output shape.

## Required context

- Tech-stack profile (required):
  - `target`: `web` | `ios` | `android`
  - `framework`: e.g. `react`, `vue`, `swiftui`, `uikit`, `compose`
  - `token_format`: e.g. `css-vars`, `tailwind-theme`, `swift-tokens`,
    `compose-tokens`
- Design context: the Figma frame, component, or node to implement.
- Rule source: confirmed project spec or output from
  `figma-create-design-system-rules`.

## Inputs

- Figma frame, component, or node (URL, file key, or node id).
- Project spec or captured rules.
- Tech-stack profile.
- Optional: existing codebase component references or naming conventions.

## Outputs

- Implementation code for the declared platform and framework.
- Mapping notes for major layout or component choices (why a specific
  pattern was chosen).
- Unresolved questions when design meaning is still ambiguous after
  reading the context.

## Workflow

1. Confirm the tech-stack profile. If `target`, `framework`, or
   `token_format` are missing, ask before writing any code.
2. Confirm the rule source. If no confirmed spec exists, ask whether to
   use `figma-create-design-system-rules` first or proceed with
   inferred rules marked as provisional.
3. Read the Figma context using the `figma` skill:
   - `get_design_context` for layout, component structure, and code hints.
   - `get_variable_defs` for token values.
   - Read only the target node — do not pull the entire file.
4. Check the codebase for existing components that match the design
   target. Reuse them rather than generating new code from scratch.
5. Check whether the design depends on real assets such as icons,
   raster images, or exported slices. If yes, route them through
   `figma-export-slices` (or the equivalent asset-export path) before
   final implementation. Do not replace design-owned assets with generic
   placeholders unless the workflow explicitly marks them as unresolved.
   For icons, default to exported `svg` assets rather than hand-coded
   replicas. Do not size the final icon directly from the exported SVG
   canvas dimensions; also inspect the icon's actual geometry in its
   parent component. Use semantic asset and variable names in code rather
   than copying temporary Figma layer names verbatim.
6. Map layout, tokens, and components to platform-appropriate patterns:
   - **web**: flexbox/grid, CSS vars or Tailwind tokens, JSX component
     API.
   - **ios**: SwiftUI stacks/modifiers or UIKit layout, Swift token
     references, Apple platform conventions.
   - **android**: Compose layout or XML, Material token mapping, density
     and adaptive layout rules.
7. Write the implementation. Prefer confirmed rules over inferred ones.
   Mark any inferred choices in comments or mapping notes.
8. Surface unresolved ambiguity explicitly — do not silently pick a
   default for anything that changes the component's behavior or
   structure.

## Clarification policy

Ask before proceeding when:
- The platform profile is missing or incomplete.
- Component boundaries are unclear (e.g. should this be one component or
  two?).
- Interaction behavior or content hierarchy changes the code shape (e.g.
  a list that could be static or dynamic).
- The product appears to need interaction states or affordances that the
  current component board does not explicitly show (e.g. hover-only close
  button, selected affordance, focus treatment). Confirm the required
  states before implementing them by default.
- An implementation choice would be expensive to undo (e.g. choosing a
  state management pattern or a layout approach that affects many
  components).

Do not ask when:
- The design context and rules together make the correct choice
  unambiguous.
- The choice is purely cosmetic and reversible.

## Gotchas

- Never silently default to web when the platform is unspecified. Ask.
- Do not output code that ignores the declared framework conventions
  (e.g. writing class-based React when the project uses hooks, or using
  UIKit patterns in a SwiftUI project).
- Do not invent reusable rules during implementation. If a pattern looks
  like it should be a shared rule, flag it for `figma-create-design-system-rules`
  rather than encoding it silently in the output.
- Do not optimize only for pixel similarity. A structurally wrong
  component that looks correct in a screenshot will break under real
  content and state changes.
- Do not fake design-owned icons or images with placeholder blocks,
  improvised SVGs, or ad hoc CSS shapes when the design expects an
  exported asset. Use the asset export workflow first. Icon resources
  should default to exported assets, preferably SVG.
- Code Connect snippets returned by `get_design_context` are the
  authoritative component reference. Use them instead of generating new
  component code from scratch.
- If a component-set property changes child structure across values (different
  icon, background presence, divider existence, etc.), implement it as a
  structural branch — not as a single template with minor prop tweaks. Treating
  structural variants as visual-only differences will produce incomplete or
  broken rendering for the missed variants.
- Do not add product-common interaction affordances by default when the
  formal component set does not include them. Confirm the required states
  first, then implement them as a product-layer behavior or a provisional
  validated state.
- Common interaction patterns may justify proposing a provisional state,
  but they do not justify silently treating that state as canonical.
- Stateful stroke or border treatments must not change box geometry between
  states. Reserve the same border/stroke space in all states (e.g. transparent
  border in default, colored border in selected), or use a non-layout-affecting
  layer such as inset box-shadow or outline. Geometry drift between states is a
  visible layout jump.
- Figma CDN image URLs returned by design-context tools are temporary signed
  links that expire. Download assets into the repository (or use the
  `figma-export-slices` workflow) immediately during implementation. Do not
  hardcode signed URLs in source code.
- Exported SVG canvas dimensions are not the source of truth for rendered
  icon size. Match the icon's in-component geometry from Figma (button size,
  icon-frame size, and actual glyph bounds), otherwise the asset will often
  render too large, too small, or visually off-center.
- When `get_design_context` returns a CSS transform (e.g. `-rotate-90`) on
  an icon or asset, verify whether the exported SVG already encodes the
  intended orientation before copying the transform. Figma may apply a
  rotation to a component wrapper while the exported asset is already
  rendered in the correct direction. Copying the transform blindly will
  produce a double-rotation and the wrong visual result.
- Do not preserve unresolved Figma layer names as final code identifiers.
  Generic names such as `ic_` or `icon` are acceptable as tracing clues in
  Figma, but code should use a semantic identifier based on the confirmed
  product role. If the role is still unclear, ask or mark it provisional
  instead of pretending the name is settled.

## Verification

- The output targets the declared platform and framework — not a default
  guess.
- The code respects confirmed rules before inferred ones.
- The result is structurally correct, not only visually similar.
- Mapping notes explain non-obvious choices.
- Unresolved ambiguity is listed, not hidden.
