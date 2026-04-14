# Video Know-How Notes

Source transcript:

- [_downloads/Figma x Claude Code Live： Roundtrip workflows with Figma MCP [1DxleEbZoYgKL].transcript.txt](/Users/markun/Documents/Codex/Mars/_downloads/Figma%20x%20Claude%20Code%20Live%EF%BC%9A%20Roundtrip%20workflows%20with%20Figma%20MCP%20%5B1DxleEbZoYgKL%5D.transcript.txt)

## High-Value Know-How To Borrow

### 1. Skills should encode how we want tools to be used, not just what tools exist

The video draws a distinction between:

- access to Figma
- knowledge of how to use Figma well for our workflow

Takeaway:

- foundational skills teach the raw tool
- project skills teach structure, standards, readability, and intent

Why it matters for us:

- our workflow should not stop at "agent can call Figma"
- we need skills that encode implementation-friendly structure

Reference:

- transcript around line 128 to 155

### 2. If the project already has a system, capture it before broad implementation

The video explicitly suggests creating a skill that describes the design
system by interviewing the user in depth.

Takeaway:

- undocumented team knowledge is still a source of truth
- we should turn that into a reusable skill or rule doc first

Why it matters for us:

- this strongly supports our "existing rules first" principle

Reference:

- transcript around line 203 to 217

### 3. Incomplete designs can be expanded from sketches, but inside the system

The video shows using a sketch or low-fidelity idea as input and asking
the model to flesh it out in the existing design system.

Takeaway:

- sketch expansion is valid
- it should be constrained by the system, not used to reinvent it

Why it matters for us:

- this is useful for missing states, cards, and sections
- this should remain a gap-filling path, not the primary path

Reference:

- transcript around line 269 to 272

### 4. Structural correctness matters even when visual cleanup is still needed

One strong point in the video is that the model generated a component,
with variants and properties, even though some visual cleanup was still
needed.

Takeaway:

- successful output is not only about pixel-perfect visuals
- component architecture, variants, and editable properties are major wins

Why it matters for us:

- our evaluation should score both visual fidelity and structural quality

Reference:

- transcript around line 292 to 315

### 5. Exploration is cheap, but ambiguity should still be resolved

The video suggests both of these can be true:

- agents are good for trying multiple directions quickly
- specificity is still better than vague prompts

Takeaway:

- ask for multiple options when exploring
- ask clarifying questions when ambiguity affects meaning

Why it matters for us:

- this complements our clarification policy

Reference:

- transcript around line 472 to 505

### 6. Verification should be a first-class skill, not an afterthought

The video gives an example of comparing a Figma frame against a built app
screen, categorizing differences, and identifying component overrides.

Takeaway:

- implementation should be checked against design
- the output should be annotated and triaged, not just visually eyeballed
- the verification surface will differ by target platform

Why it matters for us:

- we should add a verification capability to the workflow

Reference:

- transcript around line 472 to 505

### 7. Skills can capture tacit expert taste that is not present in code or the design system

The speakers point out that a lot of useful implementation knowledge is
not fully captured in code or design files, and skills are a way to
package that knowledge.

Takeaway:

- skills are not only for API instructions
- skills can encode review standards, layout heuristics, and team taste

Why it matters for us:

- our skills should include judgment and review logic, not only commands

Reference:

- transcript around line 540 to 606

### 8. Smaller composable skills are valuable

The video discusses making smaller skills that can be combined, rather
than only relying on large monolithic skills.

Takeaway:

- split the workflow into reusable parts when possible
- allow bigger orchestrating skills on top

Why it matters for us:

- this matches our current folder strategy
- it argues for cleanup, capture, implement, and verify as separate units

Reference:

- transcript around line 553 to 606

### 9. Add a gotcha section and keep revising it from failure patterns

The video suggests that when output is consistently wrong in a certain
way, that pattern should be added to a skill's gotcha section.

Takeaway:

- skills should evolve from mistakes
- repeated failure modes deserve explicit warnings and examples

Why it matters for us:

- every mature skill should probably have a `gotchas` section

Reference:

- transcript around line 658 to 676

### 10. Use Figma to resolve ambiguity, not only to store final designs

One subtle but powerful point is that Figma itself helps resolve
ambiguity. Instead of only asking the model to "make it better", you can
tweak the design in Figma first and then hand the clarified version back
to the model.

Takeaway:

- Figma can be part of the reasoning loop
- clarify visually first, then implement

Why it matters for us:

- we should treat Figma as an ambiguity-resolution surface, not only as a
passive source file

Reference:

- transcript around line 742 to 770

## Priority Recommendations

Most important to adopt now:

1. existing rules first, and capture undocumented rules
2. explicit tech-stack profile before implementation
3. clarification over invention when ambiguity changes meaning
4. verification as a dedicated step
5. gotcha sections for each mature skill
6. composable skill design