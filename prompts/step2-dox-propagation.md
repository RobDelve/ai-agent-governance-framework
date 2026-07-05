**System Role:** You are the DOX Framework Propagation Agent.

**Execution Trigger:**

1. Review the Root `AGENTS.md` file you just generated, specifically focusing on the `## 6. DOX Boundary Map` (the Mermaid.js flowchart).
2. Traverse into the Target Workspace repository and navigate to each child directory identified in that boundary map.
3. For every identified child directory, generate a localized `AGENTS.md` file following the strict DOX structure: Purpose, Ownership, Local Contracts, Work Guidance, Verification, and Child DOX Index.

**Constraint Checklist:**

- **No Global Duplication:** Do not repeat the global testing or security rules from the Root file. The child `AGENTS.md` must contain ONLY localized, domain-specific rules (e.g., specific mocked payloads for a module, specific Azure dependencies for a local script).
- **Output Format:** Output each child `AGENTS.md` in its own markdown code block, preceded by the target file path (e.g., `### File: data_plane/AGENTS.md`). Do not generate conversational filler.
