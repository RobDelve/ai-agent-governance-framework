# META-PROMPT: DOX Framework Schema

**Purpose:** This schema instructs an AI agent on how to initialize, read, and maintain a hierarchical DOX tree (`AGENTS.md` files) across a repository.
**Usage:** Feed this into the orchestrator alongside other domain schemas. This acts as the "Operating System" for the agent's context management, dictating how it distributes global vs. local rules.

---

## SYSTEM INSTRUCTIONS FOR DOX IMPLEMENTATION

You are operating under the DOX framework constraint. DOX is a highly performant, decentralized context management system. You must not rely on a single monolithic `AGENTS.md`. You must distribute instructions into local `AGENTS.md` files across the directory tree.

### STEP 1: The "Read Before Editing" Protocol

Before executing any code or documentation changes, you must establish context:

1. Read the root `AGENTS.md`.
2. Identify every file or folder you expect to touch.
3. Walk the directory tree from the repository root down to each target path. Read every `AGENTS.md` found along the route.
4. **The Resolution Rule:** Root/Parent docs provide global enterprise rules (e.g., overarching Diátaxis compliance, core testing frameworks). Child docs provide domain-specific rules (e.g., specific mocked payloads for a localized GraphRAG module). If instructions conflict, the closer (local) doc controls the details, but a child doc may **never** weaken global enterprise constraints.

### STEP 2: The Core DOX Contract (File Structure)

Whenever you create or refactor an `AGENTS.md` file within a subdirectory, it MUST contain the following sections in this exact order:

1. **Purpose:** Why does this specific folder boundary exist?
2. **Ownership:** Who (or what agent/process) maintains this boundary?
3. **Local Contracts:** What are the strict inputs, outputs, and dependencies of this domain?
4. **Work Guidance:** Local domain rules. _(Note: This is where you inject locally relevant rules synthesized from `diataxis-agent-schema.md` or `test-agent-schema.md`)._
5. **Verification:** How do we prove this folder's code works?
6. **Child DOX Index:** A recursive, linked index of any `AGENTS.md` files existing deeper in this directory branch.
   - **Visual Mapping Trigger:** The root `AGENTS.md` MUST include a Mermaid.js `flowchart TD` rendering the full DOX tree hierarchy so human architects can visually verify the agent's context boundaries.

### STEP 3: The "Update After Editing" Mandate

Every meaningful codebase change requires a DOX pass before the session closes. You are strictly forbidden from leaving stale documentation.

- **Trigger:** If your PR alters a folder's purpose, scope, dependencies, or adds a new architectural boundary, you MUST update the closest `AGENTS.md`.
- **Index Refresh:** If you add or remove a folder containing an `AGENTS.md`, you MUST traverse back up the tree and update the `Child DOX Index` in the parent `AGENTS.md`.
- **Pruning:** Delete stale notes immediately. DOX files are for current binding contracts, not historical explanations.

### STEP 4: Schema Distribution Rules

When the orchestrator provides you with multiple schemas (e.g., Testing, Documentation, DOX), distribute the generated rules intelligently:

- Place **global commands** (e.g., `pnpm test`, `cargo build`) and **universal constraints** (e.g., "All LLM outputs must use the LLM-as-a-judge pattern") in the **Root** `AGENTS.md`.
- Push **domain-specific details** (e.g., "The Python control plane requires these specific Azure mock objects") down into the **Child** `AGENTS.md` closest to the relevant code execution.
