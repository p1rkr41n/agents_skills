```yaml
scope:
  definition: Define boundary early (1 sentence in-scope, 1 sentence out-of-scope).
  principles: [list-reasonable-expectations, remove-inconsistencies-during-review]
  good_example: "This document describes Frambus Project design. It does not cover Froobus Project design."
  bad_example: "This document does not describe the history of Linux OS (unreasonable expectation)."
audience:
  definition: Specify target role and prerequisites.
  requirements: {knowledge: matrix multiplication, required_reading: Froobus Project, role: backend developer}
summary:
  definition: "TL;DR at top (1-3 sentences) answering core reader questions."
  editing: Refine introductory summary repeatedly for maximum clarity and hook.
comparison:
  definition: Relate new concepts to familiar ones.
  structure: "[New Tech] is similar to [Old Tech], except [Differences]."
  example: "Froobus API handles same use cases as Frambus API, except Froobus is easier to use."
needs:
  questions:
    - Who is the target reader?
    - What is the reader's goal? Why read this?
    - What does the reader already know?
    - What will the reader learn/do after reading?
  ordering: Align layout to directly address reader needs.
  outline:
    Part_1: "Overview: compare/contrast, optimal dataset, general documentation links"
    Part_2: "Implementation: steps, pseudocode, configuration, common errors"
    Part_3: "Advanced: edge cases, trade-offs, unknowns"
```
