# META-PROMPT: Security & Identity Schema

**Purpose:** This schema instructs an AI agent on how to generate the `## Security & Identity Standards` section for a repository-specific `AGENTS.md` file.
**Usage:** Feed this into the orchestrator alongside codebase contexts to enforce Zero Trust, credential redaction, and identity inheritance across multi-language architectures.

---

## SYSTEM INSTRUCTIONS FOR AGENTS.MD GENERATOR

When generating the `## Security & Identity Standards` section of the target repository's `AGENTS.md` file, you must strictly follow the execution steps below. Output only terse, machine-readable constraints.

### STEP 1: Execute Framework Security Assessment

Analyze the target repository to detect the languages in use. Inject strict routing rules into the `AGENTS.md` dictating exactly how the agent MUST authenticate based on the runtime context:

- **IF [Python]:** Mandate the exclusive use of `azure-identity` and `DefaultAzureCredential()`. The agent is strictly forbidden from using `ClientSecretCredential` with hardcoded strings.
- **IF [PowerShell]:** Mandate the use of `Connect-AzAccount -Identity` for production runbooks. Local debugging scripts must rely on inherited developer context or `Get-AzKeyVaultSecret`.
- **IF [Rust]:** Mandate the use of the `azure_identity` crate utilizing `DefaultAzureCredential`.

### STEP 2: The Credential Redaction Contract

Inject the following absolute constraints regarding secrets, keys, and tokens into the final `AGENTS.md`:

- **The Zero-Hardcode Mandate:** You are strictly forbidden from writing, suggesting, or retaining any plaintext passwords, API keys, SAS tokens, or connection strings in source code, configuration files, or documentation.
- **Environment Abstraction:** All runtime secrets MUST be requested dynamically via Azure Key Vault or loaded implicitly via injected environment variables.
- **Mocking Secrets in Tests:** When writing unit or integration tests (e.g., Pester or Pytest), all secrets must be mocked with obvious placeholder strings formatted as `<REDACTED_SECRET_NAME>`.

### STEP 3: Telemetry & Log Sanitization

AI agents and the code they write often leak data via error handling. Inject these logging constraints:

- **The stdout/stderr Firewall:** You must never write code that prints raw HTTP Request/Response objects to the console if they contain `Authorization` headers, Bearer tokens, or subscription IDs.
- **Exception Masking:** When writing `try/catch` or `except` blocks, you must parse the error and strip out underlying connection strings before passing the error message to the telemetry logger or console.
- **PII/GraphRAG Redaction:** For any data plane logs (especially within LLM generation or Graph extraction pipelines), you must ensure that user queries or document payloads are not logged in plaintext without explicit enterprise consent mapping.

### STEP 4: Privilege & Execution Boundaries

Inject rules to govern how the agent handles permissions and external inputs:

- **Identity Inheritance:** Code executed by this agent assumes the identity of its deployment context (e.g., an Azure Container App Managed Identity or a GitHub Actions Service Principal). You must not write code that attempts to elevate privileges beyond the assigned Role-Based Access Control (RBAC) scope.
- **Payload Sanitization (Prompt Injection Defense):** For any module that processes external text (like a GraphRAG prompt), the code must treat all input as hostile. You must not pass raw user text directly into a shell execution context (`os.system`, `Invoke-Expression`) or a direct SQL query.
