```yaml
concept: Avoid hybrid (Frankenstein) Diataxis structures in complex systems.
scope: "Organizational rules for structuring docs/ directories. This governs WHERE content lives, not HOW content is written inside each file."
layers:
  L1_sys: {scope: [features, configuration, commands, operations], rules: [no-theory, exact-context, link-to-L2]}
  L2_dom: {scope: [concepts, algorithms, protocols], rules: [define-essence, progressive-disclosure, no-source-code]}
linking: {syntax: "L1 -> L2", pattern: "First occurrence of [Term](path/to/L2.md)", anchors: subheadings}
relation_to_domain_knowledge:
  note: "L2_dom describes the organizational principle (concepts go in a separate layer). domain-knowledge/ (ref 7) defines the file-level template (each concept file uses 4 H2 Diataxis sections). These are complementary: L2 = where, domain-knowledge = how."
```
