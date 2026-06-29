```yaml
audience: {roles: [role, background, needs], prerequisites: [skills, APIs, environment], style: [avoid-jargon, define-abbreviations-on-first-use, clear-prose], culture: [avoid-idioms, avoid-metaphors]}
active_voice: {rule: agent-action-target, example: "Access granted by X -> X grants access"}
clarity: {verbs: "Strong verbs, avoid is/happen", avoid_existentials: "Avoid starting with 'There is/are'", modifiers: facts-only}
brevity: {length: "<=20 words", redundancy: {in order to: to, due to the fact that: because, at this point in time: now, in case: if, perform compilation: compile}}
paragraphs: {focus: 1-topic, length: 3-5-sentences, first_sentence: topic}
documents: {scope: [in-scope, out-of-scope], summary: 1-3-sentences, comparison: "like X except Y"}
lists_and_tables: {bullet: unordered, step: numbered, parallel: grammatical-structure, table: {headers: required, cells: "<=2 sentences"}}
punctuation: {comma: [intro, list], semicolon: link-related-sentences, colon: introduce}
terminology: {consistency: strict, pronouns: "Avoid ambiguous it/they/this/that"}
editing: {stages: [draft, edit, review], reviews: {structure: [audience, scope, flow], sentence: [active, short, remove-redundancy], polish: [grammar, links, code]}}
images: {diagram: conceptual, format: SVG}
large_documents: {navigation: H1-H4, split: ">5-7 pages", cross_links: true}
source_code: {rules: [runnable, secure, minimal], comments: explain-why, verification: show-results}
```
