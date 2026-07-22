# AI Open Source Trends 2026-07-22

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-07-22 01:56 UTC

---

# AI Open Source Trends Report — 2026-07-22

## 1. Today's Highlights

The open-source AI ecosystem is experiencing an explosion in **agent-centric tooling**, with multiple projects on today's trending list surpassing 1,000 daily stars. The standout is `ai-agent-book` (4,624 stars today) — a comprehensive Chinese-language book on AI Agent design principles, signaling strong global appetite for agent education. **Local-first and MCP (Model Context Protocol) integrations** dominate new releases: `code-review-graph` (1,925 stars), `OmniRoute` (2,034), and `wigolo` (642) each offer lightweight, client-side infrastructure that reduces dependency on cloud APIs. Meanwhile, `llmfit` and `outlines` address two critical pain points — hardware compatibility and structured output — further maturing the agent deployment pipeline. The topic search reveals continued dominance of established agent frameworks (AutoGPT, Hermes Agent, Dify) alongside a surge in **knowledge graph and memory projects** (Graphify, Claude-Mem, Mem0), reflecting the community's push toward persistent, context-rich AI agents.

## 2. Top Projects by Category

### 🔧 AI Infrastructure
*Tools, frameworks, inference engines, and developer utilities that power AI applications.*

- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐86,821 — High-throughput LLM inference engine; the de facto standard for serving large models efficiently.
- **[ollama/ollama](https://github.com/ollama/ollama)** ⭐176,606 — Run LLMs locally with one command; supports Kimi, DeepSeek, Qwen, and many more.
- **[diegosouzapw/OmniRoute](https://github.com/diegosouzapw/OmniRoute)** ⭐0 (+2,034 today) — Free MIT AI gateway unifying 268+ providers with quota-aware fallback and token compression.
- **[AlexsJones/llmfit](https://github.com/AlexsJones/llmfit)** ⭐0 (+129 today) — Quickly discover which LLMs run on your hardware among hundreds of models and providers.
- **[dottxt-ai/outlines](https://github.com/dottxt-ai/outlines)** ⭐0 (+65 today) — Structured output generation for LLMs; essential for reliable tool-calling and JSON responses.
- **[firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)** ⭐154,076 — Web search and scraping API tailored for AI agents, now a backbone for many agent workflows.
- **[langchain-ai/langchain](https://github.com/langchain-ai/langchain)** ⭐142,278 — The most widely adopted agent engineering platform, now includes deep MCP support.

### 🤖 AI Agents / Workflows
*Agent frameworks, automation tools, and multi-agent systems.*

- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐218,430 — "The agent that grows with you" — a highly customizable, open-source agent for CLI and GUI.
- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** ⭐185,643 — The original autonomous agent project, still the benchmark for general-purpose agent capabilities.
- **[TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents)** ⭐93,982 — Multi-agent LLM framework for financial trading, demonstrating vertical agent specialization.
- **[affaan-m/ECC](https://github.com/affaan-m/ECC)** ⭐231,911 — Agent harness performance optimization with skills, memory, and security layers.
- **[thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)** ⭐88,155 — Persistent context across sessions; compresses agent actions and injects relevant history.
- **[Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify)** ⭐93,186 — Turn codebases into queryable knowledge graphs; a /graphify skill for Claude Code and Cursor.
- **[bojieli/ai-agent-book](https://github.com/bojieli/ai-agent-book)** ⭐0 (+4,624 today) — Open-source book on AI Agent design; includes full text, PDF, and code — a must-read for builders.

### 📦 AI Applications
*Specific end-user applications and vertical solutions.*

- **[harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo)** ⭐98,509 — AI-generated short videos from keywords; a popular content-automation app.
- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** ⭐40,365 — AI that turns documents into native PowerPoint decks with animations and charts.
- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** ⭐58,165 — LLM-driven multi-market stock analysis with real-time news and decision dashboards.
- **[santifer/career-ops](https://github.com/santifer/career-ops)** ⭐60,891 — AI job-search agent that scans portals, scores listings, and tailors CVs — runs locally in your CLI.
- **[Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach)** ⭐59,161 — Give your agent eyes to read Twitter, Reddit, YouTube, GitHub — zero API fees.
- **[tradesdontlie/tradingview-mcp](https://github.com/tradesdontlie/tradingview-mcp)** ⭐0 (+114 today) — Connect Claude Code to TradingView Desktop for personal workflow automation.
- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐48,847 — AI productivity studio with smart chat, autonomous agents, and 300+ pre-built assistants.

### 🧠 LLMs / Training
*Model weights, training frameworks, fine-tuning tools, and evaluation platforms.*

- **[skyzh/tiny-llm](https://github.com/skyzh/tiny-llm)** ⭐4,385 — Build a tiny vLLM + Qwen for Apple Silicon; educational course on LLM inference serving.
- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** ⭐7,223 — Comprehensive LLM evaluation platform supporting 100+ datasets and 30+ models.
- **[genieincodebottle/generative-ai](https://github.com/genieincodebottle/generative-ai)** ⭐2,558 — Roadmap, projects, and interview prep for generative AI — community learning resource.
- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** ⭐290 — Minimal yet scalable library for pretraining foundation and world models.
- **[Hai-chao-Zhang/ThinkJEPA](https://github.com/Hai-chao-Zhang/ThinkJEPA)** ⭐46 — Vision-language world model using latent reasoning; pushes model-based RL and planning.
- **[R-D-BioTech-Alaska/Qelm](https://github.com/R-D-BioTech-Alaska/Qelm)** ⭐27 — Quantum-enhanced language model exploring hybrid classical-quantum LLM architectures.

### 🔍 RAG / Knowledge
*Vector databases, retrieval-augmented generation, knowledge management, and memory systems.*

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐85,597 — Leading RAG engine combining deep retrieval with agent capabilities for superior LLM context.
- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** ⭐45,310 — High-performance cloud-native vector database, now embracing hybrid search.
- **[HKUDS/LightRAG](https://github.com/HKUDS/LightRAG)** ⭐37,977 — Simple, fast RAG using graph structures for better retrieval quality — EMNLP2025 paper.
- **[qdrant/qdrant](https://github.com/qdrant/qdrant)** ⭐33,483 — Massive-scale vector database with filtering and cloud-native architecture.
- **[meilisearch/meilisearch](https://github.com/meilisearch/meilisearch)** ⭐58,694 — Lightning-fast search engine with AI-powered hybrid search, ideal for site-level RAG.
- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** ⭐61,402 — Universal memory layer for AI agents, enabling persistent, long-term context across sessions.
- **[topoteretes/cognee](https://github.com/topoteretes/cognee)** ⭐29,027 — Self-hosted knowledge graph engine that gives agents persistent long-term memory.
- **[VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex)** ⭐34,156 — Document index for "vectorless" reasoning-based RAG — challenges the assumption that vectors are always needed.

## 3. Trend Signal Analysis

**Agent orchestration and code intelligence** are receiving the most explosive community attention today. The top-gaining repositories (`ai-agent-book`, `code-review-graph`, `OmniRoute`, `i-have-adhd`) all center on making AI agents more reliable, efficient, and context-aware. Notably, **MCP (Model Context Protocol)** is emerging as a key integration pattern — projects like `code-review-graph`, `wigolo`, and `tradingview-mcp` implement MCP servers to give coding agents direct access to local codebases, web search, and financial dashboards without cloud intermediaries.

**New tech stacks appearing for the first time** include:
- **Token-compression agents**: `headroomlabs-ai/headroom` (20-95% token reduction) and the compression built into `OmniRoute` (15-95% savings) address the cost barrier for large-context workflows.
- **Hardware-aware LLM selection**: `llmfit` automates the decision of which model runs best on a given machine, a practical need as the model zoo expands.


---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*