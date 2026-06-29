```yaml
matrix: {learning: {doing: Tutorial, understanding: Explanation}, working: {doing: How-to, understanding: Reference}}
categories:
  Tutorial: {goal: Build confidence, rules: [reliable, linear, no-theory, immediate-feedback, repetitive, concrete, no-options], voice: we, style: "First do X. Next do Y."}
  How-to: {goal: Complete tasks quickly, rules: [user-perspective, realistic-goals, assume-basics, task-focused, no-setup], voice: you, style: "To do X, do Y."}
  Reference: {goal: Provide facts/specs, rules: [factual, accurate, complete, consistent, maps-to-source, no-explanation], voice: neutral}
  Explanation: {goal: Build mental model, rules: [reflective, multi-perspective, architecture, design, trade-offs, no-source-code], voice: analytical}
boundaries: {learning_vs_working: Sandbox_vs_Real-world, reference_vs_explanation: Facts_vs_Architecture, howto_vs_reference: Steps_vs_Syntax}
navigation: {item_count: 5-7, docs_readme: mandatory, cross_links: {Tutorial_Explanation: Concept, Howto_Reference: Specs, Reference_Howto: Task}}
anti-patterns: [mixing-types, hiding-specs, forced-structure, patching-bad-ux-with-docs]
```
