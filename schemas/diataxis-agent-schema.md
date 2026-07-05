# META-PROMPT: Diátaxis Agent Schema

**Purpose:** This schema instructs an AI agent on how to generate the `## Documentation Standards (Diátaxis)` section for a repository-specific `AGENTS.md` file.
**Usage:** Combine this schema with a target codebase and other domain schemas (e.g., security, build rules) to compile a unified, context-aware `AGENTS.md`.

---

## SYSTEM INSTRUCTIONS FOR AGENTS.MD GENERATOR

When generating the `## Documentation Standards (Diátaxis)` section of the target repository's `AGENTS.md` file, you must strictly follow the execution steps below. Output only terse, machine-readable constraints. Do not output conversational filler.

### STEP 1: Execute Repository State Assessment

Analyze the `docs/` folder, `README.md`, and inline comments of the provided repository. Based on your assessment, output **ONLY ONE** of the following operational modes into the generated `AGENTS.md`:

- **IF [No existing documentation or minimal README]:** Output Mode A (Generation Rules). Instruct the target agent to scaffold the Diátaxis directory structure (`/docs/tutorials`, `/docs/how-to`, `/docs/explanation`) and write new content from scratch.
- **IF [Monolithic or unstructured legacy documentation]:** Output Mode B (Refactoring Rules). Instruct the target agent to aggressively split monolithic files into the correct Diátaxis quadrants without losing historical context.
- **IF [Mature Diátaxis documentation exists]:** Output Mode C (Review & Linting Rules). Instruct the target agent to act as a PR reviewer, rejecting commits that violate quadrant boundaries (e.g., rejecting PRs that mix "Explanation" into "Reference").

### STEP 2: Define Quadrant Constraints

Inject the following strict constraints for the four Diátaxis quadrants into the final `AGENTS.md`:

#### 1. Tutorials (Learning-Oriented)

- **Goal:** Guide a beginner through a successful end-to-end learning experience.
- **Tone:** Encouraging, pedagogical, step-by-step.
- **Constraint:** Do not explain the "why" (Explanation) or provide exhaustive API lists (Reference).

#### 2. How-To Guides (Problem-Oriented)

- **Goal:** Guide an experienced user to solve a specific, real-world problem.
- **Tone:** Direct, action-oriented, assuming baseline competence.
- **Constraint:** Strip all boilerplate. Focus only on the specific sequence of actions required to achieve the goal.

#### 3. Reference (Information-Oriented) [INLINE ONLY]

- **Goal:** Describe the machinery purely and accurately.
- **Location Constraint:** Markdown files are NOT to be used for technical reference. All reference documentation must be strictly maintained as inline code comments compatible with the repository's native parser (e.g., Rustdoc `///`, Python Sphinx/Google-style docstrings, PowerShell `<# .SYNOPSIS #>`).
- **The Austerity Mandate:** Inline comments must be purely factual. Ban all instructional phrasing (e.g., "This function helps you..."). State only inputs, outputs, panics, and state changes.
- **The Link-Out Rule:** If a function or class requires a tutorial or architectural explanation, you are forbidden from placing it in the docstring. You must write a pure reference comment and use the language's native linking directive (e.g., `.. seealso::`) to point to the relevant Markdown file in `/docs/how-to/` or `/docs/explanation/`.

#### 4. Explanation (Understanding-Oriented)

- **Goal:** Clarify architecture, historical context, design decisions, and system flows.
- **Tone:** Discursive, theoretical, high-level.
- **Constraint:** Ban all instructional steps and code snippets.
- **Architectural Trigger (Mermaid.js):** If the topic involves data pipelines, state changes, infrastructure topologies, multi-agent workflows, or sequence orchestrations, the agent MUST generate a corresponding Mermaid.js diagram (`graph TD`, `sequenceDiagram`, `classDiagram`, or `architecture`).

### STEP 3: Define Code Snippet Standards

Inject the following code snippet formatting rules for use in Tutorials and How-To Guides:

- **The Contract of State:** Code snippets should be lean and contextual, omitting excessive boilerplate (e.g., environment setup or repetitive imports). However, every fragmented code snippet MUST be wrapped in the following Markdown structure to prevent "magic variables":

  > **Assumed State:** [Define required authenticated contexts, instantiated objects, or prior environment variables here].

  ```[language]
  # Terse, focused code executing the specific action
  ```

  > **Expected Output:** [Define exactly what is returned or what state is mutated].
