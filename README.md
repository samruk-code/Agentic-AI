# Agentic AI — Production Patterns in Python

![Agentic AI](Agentic-AI.png)

Three working AI systems that implement production-grade agentic design patterns: self-reflection loops, tool-augmented reasoning, and multi-agent coordination. Built end-to-end in Python using the OpenAI function-calling API and live external data sources.

---

## Projects

### 1. Reflection Loop — Self-Improving Essay Writer
**[`M2 Assignment/C1M2_Assignment.ipynb`](M2%20Assignment/C1M2_Assignment.ipynb)**

An LLM that critiques and rewrites its own output in a closed loop — the core building block behind iterative agents.

| Step | What happens |
|---|---|
| Draft | Model generates an initial essay from a topic prompt |
| Reflect | A separate reasoning pass critiques structure, coherence, and gaps |
| Revise | Model rewrites using the critique as a feedback signal |

The interesting engineering challenge here is designing the reflection prompt so it produces *actionable* critique rather than generic feedback — the quality of revision is entirely determined by the specificity of the reflection step.

**Stack:** `aisuite`, `openai:gpt-4o`, `python-dotenv`

---

### 2. Tool-Augmented Research Agent
**[`M3 Assignment/C1M3_Assignment.ipynb`](M3%20Assignment/C1M3_Assignment.ipynb)**

A research agent that decides *when* to call external tools, executes them, then reflects on the gathered information to produce a structured HTML report.

- Wired **arXiv** and **Tavily** as callable tools via OpenAI's function-calling API
- The agent autonomously decides which tool to use and how to query it based on the research question
- A reflection step critiques the draft report and drives a second revision pass
- Final output rendered as a styled, human-readable HTML report

The key design decision was keeping tool definitions narrow and typed — broad tool signatures caused the model to hallucinate arguments. Tight schemas eliminated that failure mode entirely.

**Stack:** `openai` (tool-calling API), `arxiv`, `tavily`, `IPython.display`

---

### 3. Multi-Agent Research System
**[`M5 Assignment/C1M5_Assignment.ipynb`](M5%20Assignment/C1M5_Assignment.ipynb)**

A fully coordinated pipeline of three specialized agents that collaborate to produce a research report — each with a distinct role and access to different tools.

```
Planning Agent (Writer)
    │── decomposes the topic, creates outline, writes final report
    │
Research Agent
    │── queries arXiv, Tavily, and Wikipedia in parallel
    │── returns structured results back to the planner
    │
Editor Agent
    └── reflects on the draft, returns structured improvement feedback
```

The non-trivial part was designing agent handoffs — each agent receives only the context it needs, not the full conversation history. This keeps token usage predictable and prevents earlier agents from polluting later reasoning.

**Stack:** `aisuite`, `arxiv`, `tavily`, `wikipedia`, `python-dotenv`

---

## Skills Demonstrated

- Agentic pipeline design: reflection loops, tool use, multi-agent coordination
- OpenAI function-calling API — tool schema design, argument validation, error handling
- Prompt engineering for multi-step LLM workflows
- Integrating live external APIs: arXiv, Tavily, Wikipedia
- Role decomposition and context management in multi-agent systems

---

## Run It Yourself

```bash
git clone https://github.com/samruk-code/Agentic-AI.git
cd Agentic-AI
pip install aisuite openai arxiv tavily wikipedia python-dotenv
```

Create a `.env` file with your API keys:

```
OPENAI_API_KEY=your_key_here
TAVILY_API_KEY=your_key_here
```

Then open any notebook in Jupyter and run all cells.

---

## Course

Built as part of **[Agentic AI with Andrew Ng](https://www.deeplearning.ai/courses/agentic-ai/)** (DeepLearning.AI) — an intermediate course on production agentic design patterns.
