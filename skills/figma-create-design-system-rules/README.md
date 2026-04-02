# figma-create-design-system-rules

## Goal

Generate or extend an implementation-oriented rule set when a project does
not already have a complete usable spec. The output is an editable draft
for human review — not a final spec to implement against directly.

## When to use

- A project has no formal design-system rules and implementation is about
  to start.
- A spec exists but does not cover enough detail to implement safely
  (missing token values, undefined component states, etc.).
- A draft rule set needs to be extracted from Figma for human review
  before implementation begins.

## When not to use

- A strong existing spec already covers the implementation target — use it
  directly and skip this skill.
- The task is only to capture undocumented rules that already exist in the
  team's heads — use `figma-capture-design-system` instead.

## Required context

- Tech-stack profile (`target`, `framework`, `token_format` — see
  `inventory/tech-stack-profile.md`).
- Existing spec status: what is already documented vs. what is missing.
- Target Figma design context (file key, relevant frames or components).

## Inputs

- Figma frames or components to extract rules from.
- Any existing design-system notes or partial spec.
- Tech-stack profile.
- Known project conventions (naming, token format, component API style).

## Outputs

- Editable rule draft covering: layout, spacing, typography, color,
  component structure, and implementation conventions.
- Inferred patterns extracted from the Figma design.
- Explicit list of unknowns or low-confidence inferences, marked clearly.

## Workflow

1. Confirm the tech-stack profile. If `target`, `framework`, or
   `token_format` are missing, ask before proceeding — rules are
   platform-specific.
2. Check whether an existing spec already covers the needed scope. If it
   does, identify only the gaps rather than regenerating the whole spec.
3. Call `figma` skill tools to read the target frames and components:
   - `get_design_context` for layout, component structure, and code hints.
   - `get_variable_defs` for token values (colors, spacing, typography).
   - `get_metadata` if the node tree structure is needed to understand
     component hierarchy.
4. Extract patterns from the design context. For each inferred rule,
   classify it as:
   - **Confirmed**: directly readable from the design (e.g. a token value,
     a consistent spacing unit).
   - **Inferred**: a repeated pattern that looks like a rule but has not
     been confirmed by the team.
   - **Unknown**: a gap where the design does not provide enough
     information.
5. Produce the rule draft from the context collected in step 3. Mark all
   inferred rules as provisional. List all unknowns explicitly at the end.
   If `create_design_system_rules` is available in the session, use it as
   a supplemental template or structural reference — it does not consume
   the node-specific context directly, so the primary draft must come from
   `get_design_context` and `get_variable_defs`.
6. Hand the draft to the user or team for review before passing it to
   `figma-implement-design` or `figma-verify-implementation`.

## Clarification policy

Ask before proceeding when:
- The tech-stack profile is missing and it changes implementation
  conventions (e.g. CSS vars vs Tailwind theme vs Swift tokens).
- An inferred rule may conflict with a known project standard — ask which
  takes precedence.
- A repeated visual pattern might be a one-off exception rather than a
  true rule — ask before promoting it to a standard.

Do not ask when:
- A rule is directly readable from a token value or a consistent pattern
  across multiple components.
- The gap is acknowledged and will be listed as unknown — record it and
  move on.

## Gotchas

- Do not replace a valid existing spec with a guessed one. Preserve
  confirmed rules and only fill the gaps.
- Do not silently promote accidental visual repetition into a standard.
  Two components that look similar may have different intended rules.
- Keep inferred rules explicitly provisional in the output. The draft is
  for human review — it is not ready to implement against directly.
- Token values extracted from `get_variable_defs` are authoritative.
  Values inferred from screenshots or pixel inspection are not — mark them
  as low-confidence.
- Platform-specific rules must stay separated. Do not merge web and iOS
  conventions into a single rule.

## Verification

- The rule set is profile-aware and references the correct platform
  conventions.
- Existing confirmed rules are preserved, not overwritten.
- Inferred rules are specific enough to guide implementation.
- All inferred rules are marked as provisional.
- Unknowns and low-confidence inferences are listed explicitly.
