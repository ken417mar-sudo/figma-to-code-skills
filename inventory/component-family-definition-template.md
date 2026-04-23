# Component Family Definition — Template

> Formal output format. Use this template when a component family
> boundary is clear enough to define before implementation begins.
> Required output from `figma-create-design-system-rules` for
> component-scoped work when the family boundary is clear.
> Produce it before implementation begins and update it in place as
> definition or verification status changes.

---

## Granularity Rule

**Simple family:** one card covers one independently reusable and
independently verifiable unit. Use this for most components.

**Composite family:** one root card describes the composition and
sub-family relationships. Each sub-family that is independently reusable
or independently verifiable gets its own card. The root card does not
duplicate sub-family axes or slots — it only describes how sub-families
compose.

Rule of thumb: if a sub-component can be used outside the parent, or
verified independently, it is a sub-family and gets its own card.

---

## Status Fields

Every state or axis value carries two independent status dimensions:

**`definition_status`** — how settled is the design definition?
- `formal` — defined in a formal Figma component set, approved
- `provisional-confirmed` — user-confirmed, provisional board exists, not yet in formal component set
- `provisional-proposal` — direction agreed but not yet signed off

**`verification_status`** — how far has implementation been verified?
- `not-covered` — not yet implemented or verified
- `coverage-complete` — all cases implemented, visual verification pending
- `visual-verification-complete` — visually verified against Figma source

These two dimensions are independent. A state can be
`provisional-proposal` + `visual-verification-complete` (implemented and
verified, but definition not yet formally approved). Do not conflate them.

---

## Card Format

```markdown
# Component Family Definition — [Family Name]

> [simple | composite] family  
> definition produced: [date]  
> last updated: [date]

---

## Family Boundary

**Family name:** [name]  
**Family type:** simple | composite  
**[If composite] Sub-families:** list with brief description  
**[If composite] Root card scope:** composition and sub-family relationships only  
**Out of scope:** list what is explicitly excluded

---

## Semantic Slots

[Table or per-variant breakdown of named slots]

---

## Axes

### Formal axes

| Axis | Values | definition_status |
|---|---|---|
| [axis] | [values] | formal |

### Provisional axes

| Axis | Values | definition_status |
|---|---|---|
| [axis] | [values] | provisional-confirmed / provisional-proposal |

---

## Required States

| Component | State / Value | definition_status | verification_status |
|---|---|---|---|
| [component] | [state] | formal / provisional-confirmed / provisional-proposal | not-covered / coverage-complete / visual-verification-complete |

---

## Visual Tokens

[Token table per state/variant]

---

## Asset Slots

| Asset | File | Notes |
|---|---|---|
| [name] | [filename] | [inline SVG / img / currentColor rule] |

---

## Promotion Rule

[What must be true before any provisional axis can be promoted to formal.
If all axes are already formal, state that explicitly.]

---

## Code Prop API

[Interface definitions for each exported component]

---

## Verify Matrix

| Case | Component | Axis combo | definition_status | verification_status |
|---|---|---|---|---|
| V1 | [component] | [combo] | [status] | [status] |
```

---

## Notes for producers

- Fill `definition_status` and `verification_status` independently for
  every row. Never use a single combined status column.
- For composite families: write the root card first, then sub-family cards.
  Sub-family cards follow the same format as simple family cards.
- Do not promote a provisional axis to formal in this card — that requires
  a separate user sign-off action and a Figma component set update.
- This card is a snapshot. Update it when definition or verification status
  changes, rather than creating a new card.
- Do not add format-maturity labels such as `trial-run` or `controlled`
  to new live cards. The format itself is already formal at the repo level.
