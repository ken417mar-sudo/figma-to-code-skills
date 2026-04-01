# figma-ai-implementation-cleanup

## Goal

Reduce noise in messy Figma files so later rule extraction and code
implementation are more stable.

## When to use

- when a design file has inconsistent naming, hidden legacy frames, or
  confusing structure
- when implementation quality is suffering because the Figma file is too
  noisy
- before extracting rules from a draft that has no clean design system

## When not to use

- when the file is already clean and implementation-ready
- when the user only needs direct implementation from a trusted spec

## Required context

- Figma file or node reference
- cleanup target scope
- optional tech-stack profile if naming or structure should align with a
  delivery platform

## Inputs

- active frames or target pages
- known problem patterns
- optional examples of what should be treated as current vs. legacy

## Outputs

- cleaner layer structure
- more reliable naming and grouping
- reduced hidden or legacy noise
- clearer implementation surface for later skills

## Workflow

1. Identify active design targets and likely noise sources.
2. Separate current design content from hidden, legacy, or duplicate
   content.
3. Normalize naming and grouping where it improves implementation
   clarity.
4. Preserve meaningful structure while removing avoidable ambiguity.
5. Hand the cleaned result to rules or implementation skills.

## Clarification policy

- ask when it is unclear which frames are active versus historical
- ask before deleting or deeply restructuring content that may still be
  meaningful

## Gotchas

- do not over-clean until meaningful variants disappear
- do not convert one-off exceptions into shared standards during cleanup
- cleanup should prepare implementation, not redesign the product

## Verification

- the active implementation target is easier to identify
- legacy and hidden noise is reduced
- repeated patterns are easier to read without losing necessary detail
