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
- Prefer exporting and naming the real asset first, then wire the code
  to that asset.

Examples:

- web: prefer `svg` plus modern raster formats when needed
- iOS: support scale-based exports such as `@1x`, `@2x`, `@3x`
- Android: support density buckets such as `mdpi` through `xxxhdpi`

## Gotchas

- Figma CDN image URLs returned by `get_design_context` and related tools are
  temporary signed links. They expire and must not be used as asset sources in
  code. Always export the asset through this workflow and commit it to the
  repository before wiring it into the implementation.
