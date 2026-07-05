Enterprise AI Agent Governance FrameworkThis repository contains the master schemas required to govern AI coding agents (such as Google Antigravity, GitHub Copilot, Claude Enterprise, or Cursor).By feeding these schemas into an orchestrator alongside a target codebase, you generate deterministic, repository-specific AGENTS.md files that lock down documentation, testing, security, and context management.🏗️ The Five PillarsThis framework uses a composable architecture consisting of five master schemas:dox-agent-schema.md: Decentralized context management via the DOX framework.diataxis-agent-schema.md: Standardized technical documentation constraints.test-agent-schema.md: Rules for unit, integration, and non-deterministic (LLM/GraphRAG) testing.security-agent-schema.md: Zero Trust, identity inheritance, and credential redaction.iac-agent-schema.md: Infrastructure as Code (Bicep/Terraform) and PowerShell idempotency rules.🚀 Platform-Specific Deployment WorkflowsDifferent AI platforms handle context windows, file ingestion, and system instructions differently. Choose your platform below and follow the two-step initialization sequence to generate your repository's AGENTS.md files.1. Google Antigravity 2.0Context Prep: Mount the target repository to the workspace (e.g., /workspace/MyProject) and ensure Antigravity has read access to the /schemas folder.Step 1: Root Contract Generation**System Role:** You are the Lead AI Governance Orchestrator operating within Google Antigravity. Your objective is to compile a master `AGENTS.md` file.

**Target Workspace Context:**

- **Repository Path:** [INSERT MOUNTED LOCAL FOLDER PATH]
- **Schemas Source:** [INSERT LOCAL PATH OR RAW GITHUB URLs to the 5 schemas]

**Phase 1: Ingestion & Assessment**
Silently read and internalize the 5 schemas. Scan the Target Workspace to identify primary languages, declarative IaC patterns, and current testing frameworks.

**Phase 2: Synthesis & Compilation**
Generate a single, unified `AGENTS.md` file designed to sit at the root. Obey the routing logic in the schemas (e.g., drop rules for languages not present). Structure exactly as follows:

1. Enterprise Setup & Execution Commands
2. Infrastructure & Deployment (IaC)
3. Security & Identity
4. Testing & Validation Standards
5. Documentation Standards (Diátaxis)
6. DOX Boundary Map (Mermaid.js `flowchart TD` mapping the folder structure).

Output ONLY the synthesized `AGENTS.md` content inside a single markdown code block.
Step 2: DOX PropagationReview the `## 6. DOX Boundary Map` you just generated in the Root AGENTS.md. Traverse into the Target Workspace and navigate to each child directory identified in that map.

For every identified directory, generate a localized `AGENTS.md` file following the strict DOX structure from the schema. Do not duplicate global rules. Output each file in a separate markdown block prefixed by its target path. 2. GitHub Copilot (VS Code / Workspace)Context Prep: Open the target repository in VS Code. Ensure the schemas are available in a local folder (e.g., /schemas).Step 1: Root Contract Generation@workspace You are a Lead AI Governance Orchestrator. Read the 5 schema files located in #folder:schemas.

Phase 1: Scan this entire workspace. Identify the primary languages, infrastructure patterns (like Bicep/Terraform), and current testing frameworks.

Phase 2: Generate a single master `AGENTS.md` file to sit at the root of this repository. Synthesize the rules from the schemas based ONLY on the languages you detected. Structure the output exactly like this:

1. Enterprise Setup & Execution Commands
2. Infrastructure & Deployment (IaC)
3. Security & Identity
4. Testing & Validation Standards
5. Documentation Standards (Diátaxis)
6. DOX Boundary Map (Generate a Mermaid.js `flowchart TD` mapping the directory structure).

Output ONLY the markdown block.
Step 2: DOX Propagation@workspace Look at the DOX Boundary Map in #file:AGENTS.md (at the root).
Traverse to each child directory identified in that Mermaid.js map. For each directory, generate a localized `AGENTS.md` file following the strict DOX structure defined in #file:schemas/dox-agent-schema.md.

Do not duplicate global rules from the root file. Output each child `AGENTS.md` in its own markdown block with the target file path above it. 3. Claude Desktop EnterpriseContext Prep: Upload the 5 schemas into the "Project Knowledge" section.Step 1: Root Contract GenerationRole: Lead AI Governance Orchestrator.
Context: The 5 enterprise schemas are attached in Project Knowledge.

Action: I will attach my repository files (or you can read the mounted directory).

1. Assess the codebase to determine the tech stack.
2. Synthesize the Project Knowledge schemas into a single Root `AGENTS.md` file. Discard rules that don't apply to this stack.
3. Include these exact headers: Setup Commands, Infrastructure (IaC), Security & Identity, Testing Standards, Documentation (Diátaxis), and a DOX Boundary Map (Mermaid flowchart).

Output only the markdown block. If you hit your output limit, stop cleanly and I will ask you to continue.
Step 2: DOX PropagationReview the Mermaid flowchart you just created in the Root AGENTS.md.
For every child directory listed in that map, generate the localized `AGENTS.md` file. Strictly follow the "Local Contracts" DOX structure from Project Knowledge. Output each file in a separate code block prefixed by its path. 4. Cursor IDE / Aider (OpenAI Ecosystem)Context Prep: Open the target repository. Cursor and Aider have direct file-write permissions, allowing for autonomous file generation in Step 2.Step 1: Root Contract GenerationRead @schemas/
Analyze the current codebase to detect the language stack and infrastructure.
Generate a Root `AGENTS.md` file that synthesizes the rules from the schemas, strictly tailored to the detected stack.
Sections required:

1. Setup
2. IaC & Deployment
3. Security
4. Testing
5. Documentation
6. DOX Boundary Map (Mermaid.js)

Do not run bash commands or write files yet. Just output the markdown block for me to review.
Step 2: DOX PropagationRead the Mermaid map in @AGENTS.md.
Generate the child `AGENTS.md` files for those directories based on the DOX schema rules. You have permission to write these files directly to the file system in their respective folders. 5. Microsoft Copilot Studio (M365)Context Prep: Load the 5 schemas as "Knowledge" within a custom Declarative Agent.Step 1: Root Contract Generation (System Instructions)You are the Enterprise Architecture Orchestrator.
Your Knowledge Base contains 5 master schemas (DOX, Diátaxis, Security, Testing, IaC).

When a user provides a link to an Azure DevOps repository or a local codebase, you must:

1. Scan the codebase to detect the primary languages (e.g., PowerShell, C#, Python) and infrastructure patterns (e.g., Bicep).
2. Synthesize a master `AGENTS.md` file. Filter the rules from your Knowledge Base so you only output constraints relevant to the detected stack.
3. Structure the output into 6 sections: Setup, IaC, Security, Testing, Diátaxis, and a DOX Boundary Map (using Mermaid.js).

Return the final file in a single markdown block.
Step 2: DOX Propagation (User Prompt)Read the Root `AGENTS.md` file we just generated. Using the DOX Boundary Map in Section 6, generate the specific child `AGENTS.md` files for each subdirectory. Ensure they follow the local DOX contract structure from your knowledge base and do not inherit global enterprise rules.
⚠️ Architectural Watch-OutsToken Limits: If the agent truncates its output during Step 1 or Step 2, do not restart. Simply prompt: "Continue exactly from where you left off inside the markdown block."The Echo Chamber: Treat the generated AGENTS.md files as a Pull Request from a junior developer. AI models can hallucinate constraints or misidentify frameworks. As the Human-in-the-Loop, always verify the rules before committing them to the repository's main branch.Schema Versioning: AI models evolve rapidly. Always pin your schemas to a specific version locally so that behavior remains deterministic as underlying LLMs change.
