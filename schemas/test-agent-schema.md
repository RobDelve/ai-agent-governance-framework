# META-PROMPT: Testing Agent Schema

**Purpose:** This schema instructs an AI agent on how to generate the `## Testing Standards` section for a repository-specific `AGENTS.md` file.
**Usage:** Combine this schema with a target codebase and other domain schemas (e.g., Diátaxis docs, security) to compile a unified, context-aware `AGENTS.md`.

---

## SYSTEM INSTRUCTIONS FOR AGENTS.MD GENERATOR

When generating the `## Testing Standards` section of the target repository's `AGENTS.md` file, you must strictly follow the execution steps below. Output only terse, machine-readable constraints.

### STEP 1: Execute Repository Framework Assessment

Analyze the repository to detect the primary languages and testing frameworks. Inject strict routing rules into the `AGENTS.md` dictating which framework the agent MUST use based on the file type:

- **IF [Python]:** Enforce `pytest`. Mandate the use of `@pytest.fixture` for state setup and `unittest.mock` strictly for external I/O. Ban the use of the legacy `unittest.TestCase` class structures unless modifying legacy files.
- **IF [Rust]:** Enforce native `cargo test`. Mandate that unit tests reside in the same file as the source code within a `#[cfg(test)]` module, and integration tests reside in the `/tests` directory.
- **IF [PowerShell]:** Enforce `Pester` (v5+). Mandate the strict use of `Describe`, `Context`, and `It` blocks. Enforce the use of `Mock` for all Azure/Active Directory cmdlets.

### STEP 2: Enforce the Unit vs. Integration Boundary

Inject the following strict definitions into the final `AGENTS.md` to prevent agents from writing hybrid, flaky tests:

#### 1. Unit Tests (Isolated & Fast)

- **Scope:** Testing a single pure function, struct implementation, or PowerShell filter.
- **The Zero-I/O Rule:** Unit tests are strictly forbidden from hitting the network, reading from disk (outside of mock fixtures), or querying a live database/cloud provider.
- **Mocking Mandate:** All stateful dependencies must be mocked or stubbed.

#### 2. Integration Tests (Stateful & Orchestrated)

- **Scope:** Testing the boundaries between modules, data/control plane IPC (e.g., gRPC calls), or infrastructure-as-code deployments.
- **The Lifecycle Contract:** Integration tests MUST include explicit teardown/cleanup blocks. The agent must guarantee that the environment state is identical before and after the test runs (e.g., deleting temporary Azure resource groups, rolling back database transactions).

### STEP 3: Define The "Mocking Contract"

AI agents frequently hallucinate mocks that mask underlying architectural flaws. Inject this constraint to govern how agents write mocked tests:

- **The Mocking Contract:** Whenever generating a test that utilizes a mock, the agent must include a preceding comment block explicitly defining the boundary of the mock.

  > **Mock Boundary:** [State exactly what is being bypassed, e.g., "Mocking the Azure Graph API response to simulate a throttled 429 error. The underlying retry logic is the actual target of this test."]

### STEP 4: CI/CD & Determinism Constraints

Inject these rules to ensure the agent writes tests that survive automated pipelines:

- **Ban Time-Based Asserts:** The agent is strictly forbidden from using `sleep()` or timeout-based assertions to handle asynchronous operations. It must use explicit polling, await structures, or event-driven checks.
- **Ban Hardcoded Paths:** The agent must never use hardcoded local machine paths (e.g., `C:\temp\` or `/home/user/`). It must use environment variables, relative paths, or framework-native temporary directory generators (like Pytest's `tmp_path`).

### STEP 5: Define Non-Deterministic & GraphRAG Testing Standards

Inject strict rules for evaluating LLM generations and GraphRAG retrieval pipelines to prevent flaky tests and false positives in the CI/CD pipeline:

- **Ban Exact String Matching:** The agent is strictly forbidden from using exact string assertions (e.g., `assert response == "Expected"`) on LLM outputs. It must evaluate outputs using structural validation (e.g., strict JSON schema adherence), property checks (e.g., `assert "entity_id" in response.keys()`), or semantic similarity thresholds.
- **The RAG Triad Isolation:** The agent must never write a single end-to-end test that conflates a retrieval failure with a generation failure. Tests must be isolated into three distinct categories:
  - **Context Precision (Retrieval):** Test if the GraphRAG engine extracts the correct nodes, communities, or subgraphs for a given query, completely independent of the final LLM response.
  - **Faithfulness (Groundedness):** Test if the LLM's output is completely derived from the retrieved graph context. The test must fail if the model hallucinates claims outside the provided context boundary.
  - **Answer Relevance:** Test if the final generation actually addresses the user's initial prompt, regardless of the retrieval quality.
- **LLM-as-a-Judge Pattern:** For qualitative assessments (like summarization quality, tone, or complex reasoning), the agent must scaffold tests that utilize an evaluator model (LLM-as-a-Judge) returning a deterministic float score or boolean, rather than relying on brittle regex patterns.
- **Graph Extractor Determinism:** When testing the knowledge extraction phase (parsing unstructured text into graph triplets), the agent must test for topological equivalence (e.g., verifying the existence of the `Subject-Predicate-Object` relationship array) rather than the exact natural language phrasing of the extracted nodes.
