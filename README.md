# Agent Skills Repository

This repository is a curated collection of advanced developer agent skills, styles, rules, and customizations. These components are designed to extend the capabilities of AI coding assistants (such as Antigravity IDE) to perform specialized technical research, architecture audit, and educational writing.

---

## Repository Structure

### 📁 `feynman-documentor/`
This module contains customizations and custom skills adopting the analytical rigor and pedagogical style of Nobel Laureate physicist Richard Feynman.

*   **[`core-engine-detector`](feynman-documentor/skills/core-engine-detector/SKILL.md)**: A custom skill that audits raw codebases or documentation sets. It strips away secondary wrapper files to identify the fundamental core engine (algorithms, data structures) and overlays physical hardware constraints (Disk I/O latency, Memory footprints, Thread lock contention).
*   **[`feynman-discovery-documentor`](feynman-documentor/skills/feynman-discovery-documentor/SKILL.md)**: A custom skill that generates structured, 4-layered technical tutorials following the **Feynman Discovery Loop (FDL)** framework (Physical Analogy, Active Sandbox with prediction check, Mechanical hardware breakdown with Mermaid diagram overlays, and Stress tests with concrete Before/After database ORM/API comparisons).
*   **[`feynman-perspective`](feynman-documentor/skills/feynman-perspective/SKILL.md)**: Rules and reasoning style guidelines defining the Richard Feynman persona, prioritizing physical demonstrations over academic jargon.

---

## Installation & How to Use

1.  **Clone this repository**:
    ```bash
    git clone https://github.com/p1rkr41n/agents_skills.git
    ```
2.  **Register the skills**:
    *   Copy the target skill folders from `feynman-documentor/skills/` into your IDE customizations root directory (e.g., `.agents/skills/` in your workspace, or `.gemini/config/skills/` globally).
    *   IDE agents will automatically discover and load the skills based on their names.
3.  **Execute the skills**:
    *   Call the slash commands (e.g., `/core-engine-detector` or `/feynman-discovery-documentor`) directly in the agent chat interface to trigger the execution pipelines.
