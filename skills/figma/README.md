# figma

## Goal

Provide the base read-oriented Figma capability for fetching design
context, screenshots, variables, metadata, and assets.

## When to use

- when a workflow needs authoritative design context from Figma
- when another skill needs screenshots, metadata, variables, or node
  details
- when implementation should be grounded in a real Figma node instead of
  guesswork

## When not to use

- when the task needs to write or restructure the Figma file
- when the task is specifically about creating or editing nodes, pages,
  or variables in canvas

## Required context

- Figma file or node reference
- task goal for the read operation

## Inputs

- Figma URL, file key, or node id
- optional project context
- optional tech-stack profile if the read will directly support
  implementation

## Outputs

- design context
- screenshots
- variable definitions
- metadata and asset references

## Workflow

1. Resolve the file and node to inspect.
2. Pull the smallest useful amount of design context first.
3. Expand into screenshots, variables, or metadata only as needed.
4. Pass the findings to downstream cleanup, rules, implementation, or
   verification skills.

## Clarification policy

- ask when the target node or frame is ambiguous
- ask when multiple candidate frames exist and they imply different
  implementation targets

## Gotchas

- do not over-read huge parts of a file when a smaller node is enough
- do not treat a raw screenshot alone as the full source of truth if
  metadata or variables are available

## Verification

- the fetched context clearly matches the intended frame or component
- the result includes enough structure for the downstream task without
  adding unnecessary noise
