---
name: tal-documentor
description: Refactor docs to Diataxis standard. Triggered on writing docs/documentation.
---

goal: Refactor docs to Diataxis standard
quads:
  Tutorial: {type: learn-to-do, goal: practical experience, voice: we, rules: [reliable, linear, inline-explanations <= 1-sentence]}
  How-to: {type: how-to-do, goal: task completion, voice: you, rules: [goal-oriented-titles, action-steps, no-setup-info]}
  Reference: {type: how-to-know, goal: lookup specs, voice: neutral, rules: [technical-specs, no-pronouns]}
  Explanation: {type: learn-to-know, goal: understand context, voice: analytical, rules: [trade-offs, no-source-code]}
style:
  pronouns: {Tutorial/How-to: you/we, Reference: none}
  voice: active, present-tense
  verbs: {select: select/check, enter: enter, navigate: navigate/go-to, uncheck: uncheck}
  format: {bold: UI element, code: command/file/variable, title: Sentence-case}
refs:
  idx: references/technical_writing_resources_guide.md
  dx: references/1_diataxis_framework.md
  style: references/2_writing_style_rules.md
  ind: references/3_industry_style_guides.md
  gg: references/4_google_tech_writing.md
  gg_doc: references/5_google_documents.md
  layered: references/6_layered_architecture_rules.md
  domain_knowledge: references/7_domain_knowledge_rules.md
refs_mapping:
  when_writing_tutorial: [dx (categories.Tutorial), style (mechanics), gg (code)]
  when_writing_howto: [dx (categories.How-to), style (lists, code), ind (ui)]
  when_writing_reference: [dx (categories.Reference), ind (typography), gg (lists_and_tables)]
  when_writing_explanation: [dx (categories.Explanation), gg_doc (scope, comparison)]
  when_writing_domain_knowledge: [domain_knowledge (structure, cross_linking)]
  when_organizing_structure: [layered (layers, linking), dx (navigation)]
rules: [docs_readme, relative_links, domain_knowledge, no_mixing_types, no_setup_in_howto, no_pronouns_in_ref, no_unregistered_constructs]

# Workflow

Follow these 5 phases in order. Do not skip phases.

## Phase 1: Analyze
1. Read the project source code to understand its architecture, core concepts, and API surface.
2. Identify domain-specific jargon that requires definition.
3. Check if `docs/` directory already exists. If so, audit existing docs for Diataxis compliance.

## Phase 2: Plan
1. Propose the documentation structure:
   - `docs/README.md` (mandatory — see Rule: docs_readme).
   - `docs/tutorials/`, `docs/how-to/`, `docs/reference/`, `docs/explanation/` (Diataxis quadrants).
   - `docs/domain-knowledge/` (optional — see Rule: domain_knowledge).
2. List which pages will be created or modified.
3. Present plan to user for approval before writing.

## Phase 3: Write
1. Create `docs/README.md` first (project overview + navigation hub).
2. Write Diataxis pages, applying the correct voice/rules per quad type. Consult `refs_mapping` to load only the relevant references for each page type.
3. If domain-knowledge is needed: create `jargon_glossary.md` (index-only) and individual topic files (self-contained 4-dimension chapters).

## Phase 4: Citation Pass
After writing all pages:
1. Scan every page in the Diataxis quadrants (`docs/tutorials/`, `docs/how-to/`, `docs/reference/`, `docs/explanation/`).
2. Identify the first occurrence of any jargon term defined in `jargon_glossary.md` within each file.
3. Replace the first occurrence of that term with a relative markdown link to its dedicated topic file.
4. Link to the specific H2 section anchor if it provides critical context (e.g., link to `[mmap](../domain-knowledge/memory_mapping.md#explanation)` inside a design description, or `[mmap](../domain-knowledge/memory_mapping.md#reference)` inside an API spec). Otherwise, link to the topic file root (e.g. `[mmap](../domain-knowledge/memory_mapping.md)`).
5. Ensure the glossary index (`jargon_glossary.md`) itself is updated so all defined terms have deep links to their respective topic H2 sections.

## Phase 5: Validate
Run through this checklist after the citation pass:
- [ ] `docs/README.md` exists and links to all quadrant directories.
- [ ] All links are relative paths (no `file:///` or absolute URLs).
- [ ] No Diataxis page mixes content types (e.g., tutorial containing reference tables).
- [ ] How-to pages have no setup/installation preamble (belongs in Tutorial).
- [ ] Reference pages use no personal pronouns (you/we/I).
- [ ] Each domain-knowledge topic file has all 4 H2 sections (Tutorial, How-to, Reference, Explanation).
- [ ] Glossary (`jargon_glossary.md`) is index-only: 1-sentence definitions + deep links.
- [ ] Voice is correct per section (Tutorial=we, How-to=you, Reference=neutral, Explanation=analytical).
- [ ] All first occurrences of glossary jargon are correctly hyperlinked to their domain-knowledge files.

# Example: How-to Guide
```markdown
# [Task Title]
Brief context description.
## Prerequisites
- `prerequisite_item`
## Steps
1. Action: `command`
1. Configure `/file`:
   ```ext
   k: v
   ```
1. Verify: `command`
```

# Example: Domain-knowledge Topic File
```markdown
# [Concept Name]
One-to-two sentence summary of what this concept is and why it matters to the project.

## Tutorial
We explore [concept] hands-on through a minimal working example.
1. First, we create...
2. Next, we observe...
3. We verify the result by...

## How-to
### Diagnose [concept] issues
1. Check `command_or_file`...
2. If condition, do action...

### Tune [concept] performance
1. Adjust parameter...
2. Verify with `command`...

## Reference
| Property | Value |
|----------|-------|
| Syscall  | `mmap(2)` |
| Flags    | `MAP_SHARED`, `PROT_READ` |
| Limits   | Platform-dependent |

## Explanation
[Concept] solves [problem] by [mechanism]. Unlike [alternative A] which [trade-off], [concept] chooses [design decision] because [rationale].

A common misconception is that [myth]. In reality, [correction with evidence].
```

# Rule: docs_readme
A project MUST have a `README.md` file in its `docs/` directory. This file serves as both:
1. The documentation's main introduction (describing the project's purpose, features, architecture, and mission).
2. The central Diataxis navigation hub (linking to pages in `docs/tutorials/`, `docs/how-to/`, `docs/reference/`, and `docs/explanation/`).
Do not create a redundant `docs/index.md` file.

# Rule: relative_links
All links in the documentation files MUST be relative paths (e.g., `[Title](tutorials/getting-started.md)` or `[Title](../reference/disk-layout.md)`) instead of absolute URLs (`file:///...`), ensuring documentation portability across different platforms and root folders.

# Rule: domain_knowledge
A project may include a `docs/domain-knowledge/` directory (outside the 4 standard Diataxis quadrants). It contains two types of files:

1. **Glossary index** (`jargon_glossary.md`): Each term is a 1-sentence definition linking to a dedicated topic file. No inline explanations — the glossary is a map, not an encyclopedia.
2. **Self-contained topic files** (e.g., `memory_mapping.md`, `copy_on_write.md`): Each file covers a single concept through all 4 Diataxis dimensions using H2 sections with standardized anchors:
   - `## Tutorial` (#tutorial) — voice: we, linear hands-on practice.
   - `## How-to` (#how-to) — voice: you, task-oriented steps.
   - `## Reference` (#reference) — voice: neutral, specs/tables/error codes.
   - `## Explanation` (#explanation) — voice: analytical, trade-offs/comparisons/misconceptions.
   All 4 H2 sections are mandatory. Do not mix voices across sections.

# Rule: no_mixing_types
A single documentation page MUST belong to exactly one Diataxis type. Do not embed reference tables inside tutorials, how-to steps inside explanations, or theory blocks inside how-to guides. If content from another type is needed, cross-link to the appropriate page instead.

# Rule: no_setup_in_howto
How-to guides MUST NOT contain installation or environment setup instructions. Assume the reader has a working setup. Setup content belongs in a Tutorial or a dedicated "Getting started" page. A How-to guide may link to setup docs in a Prerequisites section.

# Rule: no_pronouns_in_ref
Reference pages MUST use impersonal, neutral voice. Avoid personal pronouns (you, we, I, they). Use passive voice or noun-subject sentences. Example: "The function returns an error" instead of "You will get an error."

# Rule: no_unregistered_constructs
Every jargon term, abbreviation, or domain-specific concept used in Diataxis pages MUST be either:
1. Defined inline on first occurrence (in parentheses or a brief clause), OR
2. Linked to the `domain-knowledge/jargon_glossary.md` entry on first occurrence.
Do not use undefined acronyms or assume the reader knows project-specific terminology.
