# figma-export-slices

Working folder for the Figma export slices skill.

## Required context

- tech-stack profile
- asset profile

## Key rule

Asset export settings should be platform-aware.

Examples:

- web: prefer `svg` plus modern raster formats when needed
- iOS: support scale-based exports such as `@1x`, `@2x`, `@3x`
- Android: support density buckets such as `mdpi` through `xxxhdpi`
