# AI Open Source Trends 2026-07-14

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-07-14 01:49 UTC

---

# AI Open Source Trends Report — 2026-07-14

## 1. Today's Highlights

Today's GitHub trending reveals a powerful convergence: **AI agent skills and knowledge layers are the hottest categories**, with explosive community attention on tools that extend coding assistants (Claude Code, Codex, Gemini CLI) with specialized capabilities. **Graphify** (+1,095 stars today) leads the charge by turning any codebase or documentation into queryable knowledge graphs, while **awesome-llm-apps** (+996 stars) cements its position as the go-to collection of runnable agent and RAG applications. Meanwhile, **Vibe-Trading** (+1,153 stars) signals growing developer appetite for AI-powered financial automation, and **hallmark** (+794 stars) addresses a pain point many have felt — the need for anti-AI-slop design skills in coding tools. The broader AI topic landscape confirms that **agent frameworks, memory layers, and vector databases** remain the foundational infrastructure attracting the largest developer communities.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure
- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐86,166 — High-throughput inference engine for LLMs that has become the standard for efficient serving.
- **[langchain-ai/langchain](https://github.com/langchain-ai/langchain)** ⭐141,700 — The leading agent engineering platform for building LLM-powered applications in Python.
- **[open-webui/open-webui](https://github.com/open-webui/open-webui)** ⭐145,321 — User-friendly AI interface supporting Ollama, OpenAI API, and local models.
- **[firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)** ⭐150,455 — The API for web scraping and interaction at scale, essential for AI data pipelines.
- **[Nutlope/hallmark](https://github.com/Nutlope/hallmark)** ⭐0 (+794 today) — Anti-AI-slop design skill for Claude Code, Cursor, and Codex — a new category of "dev tool skills" emerging.

### 🤖 AI Agents / Workflows
- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐214,294 — "The agent that grows with you" — a massive-agent framework with self-evolving capabilities.
- **[Shubhamsaboo/awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps)** ⭐119,664 (+996 today) — 100+ AI Agent & RAG apps you can actually run — clone, customize, ship — today's most accessible agent resource.
- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** ⭐185,514 — The original autonomous agent vision remains a top project for accessible AI.
- **[CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit)** ⭐36,002 — Frontend stack for agents and generative UI, spanning React, Angular, and mobile.
- **[coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills)** ⭐0 (+299 today) — Marketing skills for Claude Code and AI agents — a new "skills as code" pattern.

### 📦 AI Applications
- **[HKUDS/Vibe-Trading](https://github.com/HKUDS/Vibe-Trading)** ⭐0 (+1,153 today) — Personal trading agent built for real-time market analysis and execution.
- **[moeru-ai/airi](https://github.com/moeru-ai/airi)** ⭐0 (+78 today) — Self-hosted, open-source Grok Companion with realtime voice chat and game-playing capabilities (Minecraft, Factorio).
- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** ⭐38,779 — AI generates editable PowerPoints from documents with native shapes, charts, and audio narration.
- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐48,523 — AI productivity studio with smart chat, autonomous agents, and 300+ assistants.

### 🧠 LLMs / Training
- **[ollama/ollama](https://github.com/ollama/ollama)** ⭐176,067 — The simplest way to run local LLMs including Kimi, GLM, DeepSeek, Qwen, and Gemma.
- **[rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch)** ⭐99,037 — Step-by-step PyTorch implementation of a ChatGPT-like LLM from scratch.
- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** ⭐285 — Reliable, scalable library for pretraining foundation and world models — an emerging research direction.

### 🔍 RAG / Knowledge
- **[Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify)** ⭐84,791 (+1,095 today) — Turn any folder of code, docs, images, or videos into a queryable knowledge graph for AI coding assistants.
- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐84,972 — Leading open-source RAG engine fusing retrieval-augmented generation with agent capabilities.
- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** ⭐45,213 — High-performance cloud-native vector database for scalable ANN search.
- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** ⭐60,758 — Universal memory layer for AI agents, enabling persistent context across sessions.
- **[thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)** ⭐87,115 — Persistent context injection for agent sessions — compresses and injects relevant history automatically.

---

## 3. Trend Signal Analysis

Three clear signals emerge from today's data:

**First, the "Skills for Agents" ecosystem is exploding.** Projects like *hallmark*, *marketingskills*, and *Graphify* all extend AI coding assistants (Claude Code, Codex, Gemini CLI) with pluggable capabilities. These aren't standalone agents — they are **augmentation layers** that provide design taste, marketing expertise, or knowledge graph creation to existing CLI agents. This represents a profound shift: the ecosystem is moving from building monolithic agents to composing swappable "skills" that any agent can consume. The star acceleration (+794 for hallmark, +299 for marketingskills in a single day) suggests this pattern is resonating deeply with developers who want to customize their toolchain rather than replace it.

**Second, knowledge graphs are having a renaissance as the RAG layer of choice.** *Graphify* (+1,095 today), *ragflow*, and *cognee* are all pushing beyond traditional vector search toward graph-augmented retrieval. The thesis: raw vector similarity loses structural relationships; knowledge graphs preserve the connections between code modules, database schemas, and documentation. This is particularly compelling for coding assistants that need to understand architecture, not just recall snippets.

**Third, financial AI applications are surging.** *Vibe-Trading* (+1,153 today) and *daily_stock_analysis* (⭐57,071) both target automated trading with LLM agents. The pattern combines market data ingestion, real-time news analysis, and decision frameworks — all powered by agents. This mirrors the broader trend of domain-specific agent applications moving beyond chat and coding into verticals like finance, healthcare, and gaming.

**Connection to industry events:** The emphasis on tools compatible with Claude Code, Codex, OpenCode, and Gemini CLI reflects the ongoing proliferation of LLM-native coding assistants. Each major vendor now has a CLI agent — and the open-source community is building the "batteries included" layer on top of them.

---

## 4. Community Hot Spots

- **🔗 [Shubhamsaboo/awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps)** — 100 runnable agent and RAG apps in one repo; the fastest path from idea to working prototype. A must-bookmark for anyone building agent workflows.

- **🔗 [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify)** — Turns any codebase into a queryable knowledge graph for AI assistants. If you're frustrated by LLMs that don't understand your project architecture, this is today's most practical solution.

- **🔗 [Nutlope/hallmark](https://github.com/Nutlope/hallmark)** — Anti-AI-slop design skills for Claude Code and Cursor. The first dedicated tool fighting "samey" AI-generated output — a sign that quality differentiation is becoming a priority.

- **🔗 [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** — At 214K stars, this is the most-starred "agent that grows with you." A benchmark project to study for anyone building self-evolving agent architectures.

- **🔗 [HKUDS/Vibe-Trading](https://github.com/HKUDS/Vibe-Trading)** — Personal trading agent with 1,153 stars in one day. Signals a new wave of AI-first financial tools that combine LLM reasoning with real market data — risky but rapidly popular.

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*