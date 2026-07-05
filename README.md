# Enterprise AI Agent Governance Framework

This repository contains the master schemas required to govern AI coding agents (such as Google Antigravity, GitHub Copilot Workspace, or Azure AI Foundry agents).

By feeding these schemas into an orchestrator alongside a target codebase, you generate deterministic, repository-specific `AGENTS.md` files that lock down documentation, testing, security, and context management.

## 🏗️ The Five Pillars

This framework uses a composable architecture consisting of five master schemas:

1. `dox-agent-schema.md`: Decentralized context management via the DOX framework.
2. `diataxis-agent-schema.md`: Standardized technical documentation constraints.
3. `test-agent-schema.md`: Rules for unit, integration, and non-deterministic (LLM/GraphRAG) testing.
4. `security-agent-schema.md`: Zero Trust, identity inheritance, and credential redaction.
5. `iac-agent-schema.md`: Infrastructure as Code (Bicep/Terraform) and PowerShell idempotency rules.

## 🚀 Deployment Workflow (Google Antigravity 2.0)

To generate the `AGENTS.md` architecture for a specific codebase (e.g., a Python/Rust hybrid app or a PowerShell orchestration module), follow this two-step process:

### Prerequisites

- Open your Google Antigravity IDE/Session.
- Mount the target repository to the workspace (e.g., `/workspace/MyProject`).
- Ensure Antigravity has read access to these 5 schemas (either by mounting this templates folder locally or providing raw GitHub URLs).

### Step 1: Generate the Root Contract

Copy the contents of `step1-master-orchestrator.md` and paste it into the Antigravity prompt.

- Replace the `[INSERT PATH...]` placeholders with your actual workspace paths.
- **Action:** The agent will scan your repository, synthesize the 5 schemas, and output the master `AGENTS.md`.
- **Human-in-the-Loop:** Review the generated Markdown block. Ensure the rules match your architectural intent, then save it as `AGENTS.md` in the root of your target repository.

### Step 2: Propagate the DOX Tree

In the same Antigravity session, copy the contents of `step2-dox-propagation.md` and submit it.

- **Action:** The agent will read the Mermaid.js boundary map it just created in the root `AGENTS.md` and generate the localized, child `AGENTS.md` files for your subdirectories.
- **Human-in-the-Loop:** Review the child blocks and save them to their respective subdirectories (e.g., `control_plane/AGENTS.md`).

## ⚠️ Architectural Watch-Outs

- **Token Limits:** If the agent truncates its output during Step 1 or Step 2, simply prompt: _"Continue exactly from where you left off inside the markdown block."_
- **The Echo Chamber:** Treat the generated `AGENTS.md` files as a Pull Request from a junior developer. AI models can hallucinate constraints or misidentify frameworks. Always verify the rules before committing them to the repository's `main` branch.
