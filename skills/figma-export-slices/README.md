# figma-export-slices

Working folder for the Figma export slices skill.

## Required context

- tech-stack profile
- asset profile

## Key rule

Asset export settings should be platform-aware.

Implementation rule:

- If the design depends on real icons, raster images, or slices, route
  them through this asset workflow instead of substituting placeholders,
  fake SVGs, or ad hoc CSS shapes.
- All icon resources should default to this workflow. Prefer exporting
  the real asset as `svg` first, then fall back to raster exports only
  when SVG is not viable for the target platform or the source asset.
- Export and name the real asset first, then wire the code to that
  asset.

Examples:

- web: prefer `svg` for icons, plus modern raster formats when needed
- iOS: support scale-based exports such as `@1x`, `@2x`, `@3x`
- Android: support density buckets such as `mdpi` through `xxxhdpi`

## Gotchas

- Figma CDN image URLs returned by `get_design_context` and related tools are
  temporary signed links. They expire and must not be used as asset sources in
  code. Always export the asset through this workflow and commit it to the
  repository before wiring it into the implementation.
- Some Figma components are built from multiple vector sub-nodes (e.g. an X
  icon made of two separate rotated strokes). Exporting a single sub-node
  produces an incomplete asset. Inspect the component structure first and
  compose a single complete SVG from all constituent paths before committing
  the asset.
- SVG assets used as icons must use `currentColor` for stroke/fill so they
  inherit the surrounding text color. When inlining SVG into JSX, bind
  `stroke` or `fill` to `currentColor` and set the color via a CSS class on
  the SVG element. Do not use `<img>` for icons that need color theming —
  `img` does not inherit CSS `color`.
