```yaml
concept: "domain-knowledge is a 5th branch outside Diataxis. It contains self-contained topic files that cover all 4 Diataxis dimensions within a single document."

structure:
  glossary:
    file: "docs/domain-knowledge/jargon_glossary.md"
    role: index-only
    rules:
      - "Each term: 1-sentence definition + deep links to the topic file sections."
      - "Format: **[Term](./topic_file.md)**: One-sentence definition."
      - "Sub-links: [Tutorial](./topic_file.md#tutorial) | [How-to](./topic_file.md#how-to) | [Reference](./topic_file.md#reference) | [Explanation](./topic_file.md#explanation)"
      - "No inline explanations. Glossary is a map, not an encyclopedia."

  topic_file:
    location: "docs/domain-knowledge/<topic_name>.md"
    role: self-contained-chapter
    heading_structure:
      H1: "Topic title and 1-2 sentence summary of its role in the project."
      H2_Tutorial:
        anchor: "#tutorial"
        voice: we
        goal: "Build confidence through hands-on practice with this specific concept."
        rules: [linear, reliable, concrete-example, no-theory-blocks]
      H2_Howto:
        anchor: "#how-to"
        voice: you
        goal: "Solve real-world tasks related to this concept."
        rules: [goal-oriented-titles, action-steps, assume-basics]
      H2_Reference:
        anchor: "#reference"
        voice: neutral
        goal: "Provide lookup specs: syscalls, structs, flags, limits, error codes."
        rules: [tables, no-pronouns, maps-to-source]
      H2_Explanation:
        anchor: "#explanation"
        voice: analytical
        goal: "Build deep mental model: design rationale, trade-offs, comparisons, failure modes."
        rules: [trade-offs, contrast-alternatives, common-misconceptions, no-source-code]

  cross_linking:
    - "Diataxis docs (tutorials/, how-to/, reference/, explanation/) link to domain-knowledge on first occurrence of complex jargon."
    - "Topic files may link back to Diataxis docs for extended procedures or full API specs."
    - "All links MUST be relative paths."

anti_patterns:
  - "Glossary containing long explanations (glossary is index-only)."
  - "Topic file missing any of the 4 H2 sections (all 4 are mandatory)."
  - "Mixing voices within an H2 section (e.g., using 'we' inside Reference)."
```
