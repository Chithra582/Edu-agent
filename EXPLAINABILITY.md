# EXPLAINABILITY.md

This document explains the internal mechanisms, data lineage, operational boundaries, and governance framework of **Agentic Engineering Mentor** (`edu-agent`) in accordance with the **OpenGAP v0.1.0** specification for the **HiDevs GitAgent Passport** clearance pipeline.

> **Agent Name:** Agentic Engineering Mentor (`edu-agent`)  
> **Specification:** OpenGAP v0.1.0  
> **Category / Domain:** Education / Autonomous Engineering Mentorship & AI Curriculum  
> **Compliance Standard:** OpenGAP Checkpoint 2 (Explainability & Decision Governance), FERPA, GDPR, OWASP LLM Top 10  

---

## How the Agent Decides

Agentic Engineering Mentor is an interactive pedagogical intelligence agent engineered to guide software engineering students through the principles of autonomous AI agent development, multi-agent coordination, and tool engineering. Its primary operational purpose is to act as an on-demand Socratic engineering tutor that evaluates student code, provides step-by-step architectural hints, and reinforces software craftsmanship without providing unearned copy-paste homework solutions.

### 1. Decision Architecture

The learner inquiry intake, concept mapping, code linting, and Socratic feedback pipeline operates across a deterministic, five-stage architecture:

```
Student Interaction / Query (Curriculum Question / Homework Code / Bug Diagnostic Request)
    │
    ▼
[Stage 1: Intent & Mastery Ingestion]
    │  - Evaluates student inquiry and infers current curriculum mastery level
    │  - Maps request to course unit (Prompt Engineering, ReAct, RAG, Multi-Agent Graphs)
    │  - Establishes pedagogical strategy: Socratic Hinting vs. Structural Code Review
    ▼
[Stage 2: Curriculum Concept Alignment]
    │  - Queries verified curriculum repository for authoritative architectural patterns
    │  - Retrieves canonical implementation examples and dependency rules
    │  - Formulates reference constraints without exposing direct solution code
    ▼
[Stage 3: AST Code Linting & Security Auditing]
    │  - Evaluates student Python implementations of agent loops, tools, and prompts
    │  - Executes AST security checks against disallowed imports and dangerous shell calls
    │  - Validates type hints, docstrings, and error handling constructs
    ▼
[Stage 4: Socratic Feedback & Rubric Scoring]
    │  - Scores student assignments against standardized course rubrics
    │  - Generates multi-tiered Socratic hints guiding student to discover errors
    │  - Creates targeted micro-challenges to reinforce conceptual understanding
    ▼
[Stage 5: Local Progress Commit & Trajectory Archival]
    │  - Commits verified learning milestones to local student workspace
    │  - Applies automated PII scrubbing to remove student personal identifiers
    │  - Emits structured progress summaries with clear next-unit recommendations
    ▼
Validated Educational Feedback & Auditable Pedagogical Trajectory Record
```

### 2. Decision Logic & Educational Scoring Formulations

The mentor evaluates student code quality, comprehension depth, and rubric scores using deterministic mathematical models:

1. **Student Code Mastery Index ($M_{\text{code}}$)**:
   $$M_{\text{code}} = (w_s \cdot S_{\text{ast}}) + (w_t \cdot T_{\text{test}}) + (w_d \cdot D_{\text{doc}})$$
   where:
   - $S_{\text{ast}} \in [0, 1]$ represents AST syntax conformance and clean tool design.
   - $T_{\text{test}} \in [0, 1]$ represents unit test assertion passage ratio.
   - $D_{\text{doc}} \in [0, 1]$ represents docstring and type hint completeness.
   - Weights: $w_s = 0.40, w_t = 0.40, w_d = 0.20$ ($\sum w_i = 1.0$).

2. **Pedagogical Hint Depth Scale ($H_{\text{depth}}$)**:
   $$H_{\text{depth}} = \min(3, N_{\text{attempts}})$$
   Progresses deterministically from high-level conceptual hints ($H=1$) to intermediate pseudo-code ($H=2$) and finally targeted syntax corrections ($H=3$).

### 3. Thresholding & Refusal Decision Criteria

Agentic Engineering Mentor enforces strict academic integrity and security boundaries:
- **Refusal to Provide Direct Homework Solutions**: Requests for complete, ready-to-submit assignment code are rejected with code `ERR_ACADEMIC_INTEGRITY_VIOLATION`. The agent provides structural hints and debugging guidance instead.
- **Refusal of Dangerous Execution Constructs**: Student code containing arbitrary shell commands (`subprocess`, `os.system`) or network exfiltration calls is refused (`ERR_UNSAFE_EXECUTION_BLOCKED`).
- **Turn Ceiling Enforcement**: Interactive tutoring dialogues enforce a ceiling of `max_turns: 25` to encourage self-directed practice (`WARN_TURN_BUDGET_REACHED`).
- **Workspace Confinement**: File operations are strictly confined to the course project workspace (`ERR_OUT_OF_BOUNDS_FILE_ACCESS`).

### 4. Fallback Decision Mechanism

Continuous learner support is guaranteed through multi-tier fault recovery:
- **Model Cascade Failover**: When the primary foundation model experiences latency spikes or HTTP 429 rate limits, the orchestrator cascades automatically between `claude-3-5-sonnet`, `gpt-4o`, and `gemini-2.0-flash`.
- **Deterministic Static Documentation Fallback**: If LLM inference is unavailable, the mentor falls back to pre-indexed static Markdown lesson documentation and reference solutions.
- **Graceful Code Analysis Degradation**: When AST execution sandboxes are offline, the agent falls back to regex-based syntax linting and pattern checks.

### 5. Human-in-the-Loop Governance

Human learners and course instructors retain complete control over the learning experience:
- **Learner Review Primacy**: All code suggestions and architectural hints are presented as non-destructive advice requiring student comprehension and execution.
- **Emergency Session Reset**: Learners can reset conversation contexts and diagnostic histories at any time via `/reset`.
- **Instructor Auditability**: Detailed trajectory logs and quiz rubrics can be audited by instructors to verify grading fairness and student progression.

---

## The Data It Uses

Agentic Engineering Mentor operates under strict educational privacy, FERPA, and GDPR data governance standards.

### 1. Ingested Input Data

The agent processes only operational assets necessary to fulfill curriculum mentoring:
- **Learner Questions & Inquiries**: Conceptual questions, debugging requests, and architectural inquiries.
- **Student Code Submissions**: Python snippets defining agents, custom tools, and prompt templates submitted for review.
- **Assignment Submissions**: Multiple-choice selections, code scripts, and design diagrams submitted for evaluation.

### 2. Configuration & Reference Data

- **Official Curriculum Manifest**: Chapter outlines, learning objectives, and verified exercise baselines from the course repository.
- **Tool Linting Schemas**: Python AST grammar rules and Pydantic validation specs for agent tool design.
- **Benchmark Evaluation Rubrics**: Standardized grading matrices for agent accuracy, latency, and code cleanliness.

### 3. Base Model & Inference Lineage

- **Deterministic Linguistic Linters**: Regex pattern matchers, AST parsing validators, and rubric calculators executed natively in Python (100% deterministic with zero LLM variance).
- **Foundation LLMs**: High-capability frontier models (`claude-3-5-sonnet`, `gpt-4o`, `gemini-2.0-flash`) utilized for interactive Socratic dialogue, code reasoning, and conceptual tutoring.
- **Zero Training on Student Submissions**: Student code, homework assignments, and personal inquiries are never stored externally or used for model training.

### 4. Data Privacy, Storage, and Retention

- **FERPA & GDPR Compliance**: Treats all student interactions as confidential educational records with encrypted storage and zero third-party telemetry.
- **Ephemeral Session Memory**: Conversational contexts and code inputs are scoped strictly to the current session and purged post-interaction.
- **Automated PII & Secret Scrubbing**: API credentials, auth tokens, and student email addresses are automatically scrubbed from session logs.
- **Zero Commercial Monetization**: Student performance data, learning histories, and code submissions are never shared, monetized, or sold to external third parties.

---

## Limitations

Understanding the operational boundaries and technical constraints of Agentic Engineering Mentor is essential for learners.

### 1. Complex Multi-Modal Real-Time Video Evaluation
- **Limitation**: While proficient at textual code and diagram generation, the mentor cannot directly evaluate live video demonstration streams from students.
- **Mitigation**: The mentor accepts captured screenshot frames and structured textual transcripts for multimodal project grading.

### 2. Hardware Resource Constraints on Local GPU Execution
- **Limitation**: The mentor cannot execute large local 70B+ parameter models on behalf of students whose local machines lack hardware accelerators.
- **Mitigation**: The curriculum provides free cloud inference API endpoints and Google Colab notebooks configured for lightweight experimentation.

### 3. Rapid Ecosystem Library API Shifts
- **Limitation**: Upstream releases of agent libraries may introduce minor API changes not yet reflected in existing lecture slides.
- **Mitigation**: The mentor checks the local environment library version and alerts the learner when API syntax has been updated upstream.

### 4. Subjective Capstone Creativity Assessment
- **Limitation**: The mentor evaluates functionality, test coverage, and documentation, but cannot subjectively judge original business viability.
- **Mitigation**: Capstone rubrics explicitly separate objective engineering criteria (70%) from subjective presentation and creativity (30%).

### 5. Infinite Debugging Circularity on Syntax Errors
- **Limitation**: Inexperienced learners may get trapped in repetitive syntax errors if prompt explanations are too abstract.
- **Mitigation**: If a student fails to resolve an error after 3 turns, the mentor provides a direct line-by-line diff explanation.

---

## Summary & Compliance Checklist

| Checkpoint 2 Requirement | Corresponding Section | Status |
| :--- | :--- | :---: |
| **How the agent decides** | [How the Agent Decides](#how-the-agent-decides) | **Covered** |
| - Decision architecture & 5-stage pipeline | Section 1 | Verified |
| - Decision logic & educational scoring formulations | Section 2 | Verified |
| - Thresholding & refusal decision criteria | Section 3 | Verified |
| - Fallback decision mechanism | Section 4 | Verified |
| - Human-in-the-loop governance & oversight | Section 5 | Verified |
| **The data it uses** | [The Data It Uses](#the-data-it-uses) | **Covered** |
| - Ingested learner questions, code & assignments | Section 1 | Verified |
| - Configuration, curriculum manifest & linting schemas | Section 2 | Verified |
| - Base model lineage & deterministic engines | Section 3 | Verified |
| - Data privacy, retention lifecycle & FERPA/GDPR | Section 4 | Verified |
| **Its limitations** | [Limitations](#limitations) | **Covered** |
| - Complex multi-modal real-time video evaluation | Section 1 | Verified |
| - Hardware resource constraints on local GPU execution | Section 2 | Verified |
| - Rapid ecosystem library API shifts | Section 3 | Verified |
| - Subjective capstone creativity assessment | Section 4 | Verified |
| - Infinite debugging circularity on syntax errors | Section 5 | Verified |
