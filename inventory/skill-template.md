# Skill Template

Use this template for every skill README so the whole system stays
comparable and easy to test.

## Suggested structure

### Goal

What the skill is trying to accomplish.

### When to use

The situations where this skill should be selected.

### When not to use

The situations where another skill or a manual step is a better fit.

### Required context

The minimum context this skill needs before it can run safely.

### Inputs

The concrete artifacts or references the skill expects.

### Outputs

What the skill should produce for downstream steps.

### Workflow

A short ordered sequence describing how the skill should operate.

### Clarification policy

What the skill must ask about instead of guessing.

### Gotchas

Recurring failure modes, easy mistakes, and warnings.

### Verification

How we decide whether the skill output is good enough.

## Notes

- Phase 1 skills should all use this structure.
- Platform-aware skills should explicitly mention the tech-stack profile.
- Mature skills should keep their `gotchas` section updated from real
  testing.
