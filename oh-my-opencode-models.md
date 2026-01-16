## oh-my-opencode Agent Model Guide

Below are the recommended agent "roles," their current default models, and strong alternatives by use case.

---

### 1. **Sisyphus (The Orchestrator)**
- **Role:** Task decomposition, aggressive parallel planning, reasoning loops.
- **Current Model:** `anthropic/claude-opus-4-5`
- **Mix of Alternatives:**
  - **openai/o3-high (Reasoning):** Specialist for pure logic and planning; excels at complex dependency graphs during the planning phase.
  - **deepseek/deepseek-v3.2-speciale:** Open-weight champion, on par with Gemini 3 Pro for agentic reasoning at a much lower cost; great for sub-loops to save budget.
  - **moonshot/kimi-k2-thinking:** Excels at "Chain of Thought" (CoT) reasoning over long horizons; ideal for maintaining agent focus.

---

### 2. **Oracle (The Architect)**
- **Role:** Code review, deep logic, architectural strategy.
- **Current Model:** `openai/gpt-5.2`
- **Mix of Alternatives:**
  - **anthropic/claude-opus-4.5:** Superior for reviewing huge diffs; often catches subtle bugs in large PRs.
  - **google/gemini-3-pro:** Massive 2M+ token context window for whole-architecture reasoning and cross-module understanding.
  - **meta/llama-4-405b-instruct:** Best local/privacy-focused architect for sensitive IP within a VPC.

---

### 3. **Librarian (The Researcher)**
- **Role:** Multi-repo analysis, doc lookup, evidence-based answers.
- **Current Model:** `anthropic/claude-sonnet-4-5`
- **Mix of Alternatives:**
  - **google/gemini-3-flash:** Huge, cheap context window—ideal for massive doc reading.
  - **cohere/command-r7-plus:** RAG-optimized; reduces hallucinations in citation-heavy "vector search" workflows.
  - **perplexity/sonar-huge-online:** Real-time web access, great for live research (e.g., recent GitHub issues).

---

### 4. **Explore (The Scout)**
- **Role:** Fast file traversal, pattern matching, low latency.
- **Current Model:** `opencode/grok-code` (likely Grok 3/4 based)
- **Mix of Alternatives:**
  - **meta/llama-4-scout:** Ultra-fast specialized model (8B–15B param) for "grep-like" intelligence.
  - **anthropic/claude-haiku-4.5:** Speedster with superior code understanding in complex languages (Rust/C++).
  - **mistral/ministral-8b-code:** Runs locally for low-latency, edge-based agentic exploration.

---

### 5. **Frontend-UI-UX-Engineer (The Designer)**
- **Role:** Visual code generation, React/Tailwind expertise, aesthetic judgment.
- **Current Model:** `google/gemini-3-pro-high`
- **Mix of Alternatives:**
  - **anthropic/claude-sonnet-4.5:** The "artifact" specialist—great at CSS/layout reasoning and UI spatial awareness.
  - **openai/gpt-5.2-vision:** More "pixel-perfect" than Gemini for converting visuals to code.
  - **blackbox/flux-coder-v2:** Trained specifically on frontend frameworks (Next.js, Vue, etc.), up-to-date with latest APIs.

---

### 6. **Document-Writer (The Wordsmith)**
- **Role:** Technical prose, release notes, READMEs.
- **Current Model:** `google/gemini-3-flash`
- **Mix of Alternatives:**
  - **anthropic/claude-opus-4 (Legacy):** Preferred "voice" for documentation—less robotic, warmer tone.
  - **qwen/qwen-3-creative:** Leaderboard topper for creative/DevRel style writing.
  - **openai/gpt-4.5-pro-creative:** The go-to for branded, witty, and professional documentation.

---

### 7. **Multimodal-Looker (The Visionary)**
- **Role:** Analyze diagrams, PDFs, architecture flowcharts.
- **Current Model:** `google/gemini-3-flash`
- **Mix of Alternatives:**
  - **openai/gpt-5-omni:** First-class simultaneous audio/video/text input; can handle complex multimodal tasks (e.g., fix-from-video-bug reproducibility).
  - **qwen/qwen-2.5-vl-72b:** Open-weight OCR giant; outperforms in technical document/diagram understanding.
  - **xai/grok-vision-beta:** Especially strong at "dense" information: server log screenshots, dashboards, etc.

---

## **Summary Table: The 2025 Agent Mix**

| Agent Role      | Primary Model             | Best High-IQ Alternative      | Best Speed/Cost Alternative    |
|-----------------|--------------------------|------------------------------|-------------------------------|
| **Sisyphus**    | Claude Opus 4.5          | OpenAI o3 (Reasoning)        | DeepSeek V3.2 (Budget)        |
| **Oracle**      | GPT-5.2                  | Gemini 3 Pro (Context)       | Llama 4 405B (Privacy)        |
| **Librarian**   | Claude Sonnet 4.5        | Gemini 3 Flash (Context)     | Command R7+ (RAG)             |
| **Explore**     | Grok Code                | Claude Haiku 4.5             | Llama 4 Scout                 |
| **Frontend**    | Gemini 3 Pro             | Claude Sonnet 4.5            | GPT-5.2 Vision                |
| **Writer**      | Gemini 3 Flash           | Claude Opus 4 (Legacy)       | Qwen 3 Creative               |
| **Multimodal**  | Gemini 3 Flash           | GPT-5 Omni                   | Qwen 2.5-VL                   |
