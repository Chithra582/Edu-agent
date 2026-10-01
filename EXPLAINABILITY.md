# EXPLAINABILITY — Agentic AI Engineering Pedagogical Mentor

> **Admissibility & Transparency Report for OpenGAP / Agent Passport**  
> *Agent Name:* Agentic AI Engineering Pedagogical Mentor (`agentic-engineering-mentor`)  
> *Specification:* OpenGAP v0.1.0  
> *Domain:* Education / Agentic AI Engineering  

---

## 1. Overview & Operational Purpose

Agentic AI Engineering Pedagogical Mentor is an educational intelligence and curriculum guidance agent designed to mentor engineers through a rigorous 6-week hands-on journey in building autonomous AI systems. Its primary operational purpose is to scaffold learners through the core primitives of agentic engineering—covering OpenAI Agents SDK, CrewAI, LangGraph, Google ADK, and Model Context Protocol (MCP)—while teaching cost-effective local model alternatives.

By combining Socratic diagnostic hints, framework trade-off analysis, and safe exercise validation, the mentor ensures that students gain deep conceptual understanding of autonomous workflows without falling into copy-paste anti-patterns or incurring runaway API expenses.

---

## 2. How the Agent Decides (Decision-Making Logic)

Agentic AI Engineering Pedagogical Mentor operates across a deterministic, multi-stage decision pipeline:

```
[Stage 1: Query & Week Triage] ──> [Stage 2: Pedagogical Concept Match] ──> [Stage 3: Framework Pattern Contrast]
                                                                                               │
                                                                                               ▼
[Stage 6: Learning Summary Emit] <── [Stage 5: Exercise Hint Synthesis]  <── [Stage 4: Cost & Token Assessment]
```

### 2.1 Query & Curriculum Triage
- **Decision:** The mentor evaluates the student's inquiry, determining whether it represents an environment setup problem, conceptual question, framework comparison, or exercise bug.
- **Rules:** Route environment issues to setup guides. Identify the current curriculum week and prerequisites to prevent overwhelming learners with advanced concepts prematurely.

### 2.2 Pedagogical Concept Matching
- **Decision:** Align the question with foundational agent mechanics (react loops, state schemas, tool calling, memory persistence).
- **Rules:** Focus explanations on transferable agent primitives rather than framework-specific idiosyncrasies.

### 2.3 Framework Pattern Contrast & Evaluation
- **Decision:** When learners compare frameworks, evaluate structural trade-offs (e.g. CrewAI leader-worker delegation vs LangGraph cyclic graph control).
- **Rules:** Present objective trade-offs including learning curve, observability, and debugging complexity without vendor bias.

### 2.4 Cost Assessment & Exercise Hint Synthesis
- **Decision:** Check if the requested implementation can be completed using free local models (Ollama) and formulate Socratic guidance.
- **Rules:** Never output full assignment solutions directly. Provide targeted code snippets illustrating concepts, followed by diagnostic prompts that test student comprehension.

---

## 3. Data Flow & Boundary Privacy

The mentor operates within educational privacy boundaries, protecting student submissions and project code.

| Component / Boundary | Data Received | Processing & Retention | Destination / External Transmission |
|---|---|---|---|
| Student Chat Gateway | Student queries, code snippets, exercise drafts | Ephemeral in-memory parsing; session-scoped retention | Local mentor runtime |
| Curriculum Knowledge Base | Lesson notebooks, official guides, solution tests | Read-only static indexing; zero external telemetric reporting | Local knowledge index |
| Exercise Verifier | Student exercise code submissions | Isolated sandbox execution for assertion testing only | Local verification runner |
| Audit Logger | Lesson progression timestamps, question topics | Anonymized structured JSON logging for learning progress | Local disk audit trail |

Agentic AI Engineering Pedagogical Mentor complies with operational security and privacy standards:
- **No Cloud Data Exfiltration:** Student exercises, notes, and local files remain strictly on the student's machine with zero external exfiltration.
- **Epistemic Isolation:** Each student mentoring session operates in an independent context window to eliminate cross-session data contamination.
- **Sanitized Model Payloads:** API keys, local paths, and private student credentials are automatically scrubbed from prompt payloads.
- **Data Minimization:** Only code blocks and errors directly relevant to the student's current learning obstacle are processed.

---

## 4. Known Limitations & Failure Modes

Reviewers, auditors, and users should note the following operational constraints:

1. Rapid Framework API Churn
   - *Limitation:* Fast-paced version releases in third-party libraries (CrewAI, LangGraph) can occasionally introduce syntax deprecations.
   - *Mitigation:* The mentor anchors explanations to pinned curriculum versions and flags breaking updates with official migration guides.

2. Hardware Constraints for Local Model Execution
   - *Limitation:* Running 8B+ parameter models via Ollama on low-spec laptops may result in slow inference or memory crashes.
   - *Mitigation:* The mentor provides configuration guides for quantized models (e.g. Q4_K_M) and low-cost hosted alternatives (DeepSeek, Groq).

3. Misinterpretation of Student Bug Root Causes
   - *Limitation:* Incomplete error tracebacks shared by students can cause the mentor to formulate imprecise diagnostic advice.
   - *Mitigation:* Prompt students to provide full terminal tracebacks and active environment package versions before providing debugging hints.

4. Non-Deterministic Agent Exercise Behaviors
   - *Limitation:* Multi-agent exercises with temperature > 0 may occasionally produce non-deterministic output variations in tests.
   - *Mitigation:* Teach students to set temperature=0 during unit testing and use assertion ranges rather than exact string equality.

---

## 5. Verification, Safety & Human Oversight

Agentic AI Engineering Pedagogical Mentor incorporates robust verification, safety gates, and human oversight controls across every layer of execution:

- **Real-Time Human Approval Gate:** Any recommended terminal commands, package installations, or external script executions require direct learner review and execution.
- **Emergency Session Interrupt:** Students can halt mentoring discussions or code validation routines immediately at any point.
- **Step Quota Guardrails:** Strict session turn limits (maximum 25 turns) prevent recursive mentoring loops and encourage self-directed hands-on coding.
- **Structured Audit Logging:** Mentoring interactions, exercise diagnostic steps, and recommended patterns are logged in structured JSON formats for student self-review.
