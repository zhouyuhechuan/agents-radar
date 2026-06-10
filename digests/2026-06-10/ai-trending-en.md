# AI Open Source Trends 2026-06-10

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-10 02:43 UTC

---

# AI Open Source Trends Report — 2026-06-10

## Step 1: AI Relevance Filter

From 16 trending repos, the following 13 are clearly AI/ML-related (excluded: `refactoringhq/tolaria`, `TapXWorld/ChinaTextbook`, `francescopace/espectre`):

- mvanhorn/last30days-skill, RyanCodrai/turbovec, roboflow/supervision, opencv/opencv, aaif-goose/goose, Andyyyy64/whichllm, x1xhlol/system-prompts-and-models..., yikart/AiToEarn, phuryn/pm-skills, santifer/career-ops, openai/plugins, maziyarpanahi/openmed, addyosmani/agent-skills

From 81 topic-search repos, all are AI-related per query; non-AI repos were already excluded by topic tags.

---

## Step 2: Categorization

Projects are grouped into primary categories based on their core function. A project may fit multiple categories; the most representative is chosen.

---

# 📊 AI Open Source Trends Report — 2026-06-10

## 1. Today's Highlights

Three major themes dominate today's trending activity: **local LLM benchmarking**, **agent skill ecosystems**, and **computer vision tooling**. The standout project is `Andyyyy64/whichllm` (+633 today), which provides instant, hardware-aware benchmarking for local LLMs—a clear signal that the community is moving beyond parameter-count fetishism toward practical performance evaluation. Simultaneously, a new category of "agent skills" repositories is emerging: `addyosmani/agent-skills` (+443 today) and `phuryn/pm-skills` (+806 today) package reusable, production-grade capability modules for AI coding agents like Claude Code and Codex. In the computer vision space, `roboflow/supervision` continues its steady climb (+733 today) as the go-to library for reusable CV tools. The most explosive growth, however, belongs to `mvanhorn/last30days-skill` (+3,191 today), a grounded research agent that synthesizes multi-platform web data—suggesting strong demand for information-aggregation agents.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure
Projects providing foundational frameworks, inference engines, developer tooling, and CLI systems.

- **[ollama/ollama](https://github.com/ollama/ollama)** ⭐173,720 — The most widely adopted local LLM runner; now supports Kimi-K2.6, GLM-5.1, MiniMax, DeepSeek, and more.
- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐82,365 — High-throughput LLM inference engine, essential for production deployments.
- **[langchain-ai/langchain](https://github.com/langchain-ai/langchain)** ⭐138,910 — The leading agent engineering platform, now the backbone of countless agent systems.
- **[open-webui/open-webui](https://github.com/open-webui/open-webui)** ⭐140,876 — User-friendly AI interface supporting Ollama, OpenAI API, and local models.
- **[firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)** ⭐130,780 — The de facto API for web scraping, search, and page interaction at scale.
- **[browser-use/browser-use](https://github.com/browser-use/browser-use)** ⭐98,000 — Makes websites accessible for AI agents; essential for browser automation tasks.
- **[RyanCodrai/turbovec](https://github.com/RyanCodrai/turbovec)** ⭐0 (+1,801 today) — A vector index built on TurboQuant with Rust core and Python bindings; notable for its performance claims.
- **[googleworkspace/cli](https://github.com/googleworkspace/cli)** ⭐26,949 — Google Workspace CLI with built-in AI agent skills for Drive, Gmail, Calendar, and more.

### 🤖 AI Agents / Workflows
Agent frameworks, automation systems, and multi-agent orchestration tools.

- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** ⭐184,861 — The original autonomous agent framework, still the benchmark for accessible AI agent development.
- **[OpenHands/OpenHands](https://github.com/OpenHands/OpenHands)** ⭐76,338 — AI-driven development environment that plans, codes, and debugs autonomously.
- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐188,926 — "The agent that grows with you" — a self-improving agent system gaining massive traction.
- **[aaif-goose/goose](https://github.com/aaif-goose/goose)** ⭐0 (+489 today) — Extensible AI agent beyond code suggestions; installs, executes, edits, and tests with any LLM.
- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐47,137 — AI productivity studio with 300+ assistants, smart chat, and autonomous agents.
- **[bytedance/deer-flow](https://github.com/bytedance/deer-flow)** ⭐70,836 — Long-horizon SuperAgent harness for tasks lasting minutes to hours, with sandboxes and subagents.
- **[CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit)** ⭐34,467 — Frontend stack for agentic UIs; supports React, Angular, Mobile, Slack, and the AG-UI Protocol.
- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** ⭐41,543 — LLM-powered stock analysis system for A/H/US markets with multi-data-source integration.

### 📦 AI Applications
Specific applications and vertical solutions built on AI.

- **[Andyyyy64/whichllm](https://github.com/Andyyyy64/whichllm)** ⭐0 (+633 today) — Finds the best local LLM for your hardware using real, recency-aware benchmarks. A one-command tool solving a real friction point.
- **[mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)** ⭐0 (+3,191 today) — AI agent skill for researching any topic across Reddit, X, YouTube, HN, Polymarket, and the web with grounded summaries.
- **[santifer/career-ops](https://github.com/santifer/career-ops)** ⭐0 (+1,110 today) / ⭐51,776 — AI-powered job search system built on Claude Code with 14 skill modes, PDF generation, and batch processing.
- **[maziyarpanahi/openmed](https://github.com/maziyarpanahi/openmed)** ⭐0 (+191 today) — Open-source healthcare AI framework for clinical applications.
- **[yikart/AiToEarn](https://github.com/yikart/AiToEarn)** ⭐0 (+402 today) — Platform leveraging AI for income generation (content, automation, trading signals).
- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** ⭐25,629 — Generates real, editable PowerPoint presentations from documents with native shapes and animations.
- **[openai/plugins](https://github.com/openai/plugins)** ⭐0 (+284 today) — Repo of OpenAI-compatible plugins for extending LLM capabilities.

### 🧠 LLMs / Training
Model weights, training frameworks, fine-tuning, and evaluation infrastructure.

- **[huggingface/transformers](https://github.com/huggingface/transformers)** ⭐161,461 — The universal model-definition framework for state-of-the-art ML across text, vision, and audio.
- **[hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory)** ⭐72,035 — Unified efficient fine-tuning for 100+ LLMs and VLMs (ACL 2024).
- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** ⭐7,075 — LLM evaluation platform supporting Llama3, Mistral, GPT-4, Qwen, GLM, and 100+ datasets.
- **[ScrapeGraphAI/Scrapegraph-ai](https://github.com/ScrapeGraphAI/Scrapegraph-ai)** ⭐26,992 — AI-powered web scraper that uses LLMs to extract structured data.
- **[skyzh/tiny-llm](https://github.com/skyzh/tiny-llm)** ⭐4,264 — Educational LLM inference serving course: build a tiny vLLM + Qwen on Apple Silicon.
- **[0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig)** ⭐7,571 — Modular LLM application framework in Rust, gaining popularity for building scalable AI tools.

### 🔍 RAG / Knowledge
Vector databases, retrieval-augmented generation, knowledge management, and memory systems.

- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** ⭐44,706 — High-performance cloud-native vector database for scalable ANN search.
- **[qdrant/qdrant](https://github.com/qdrant/qdrant)** ⭐31,984 — Massive-scale vector database with cloud offering; core infrastructure for RAG.
- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐82,331 — Leading open-source RAG engine fusing cutting-edge retrieval with agent capabilities.
- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** ⭐58,208 — Universal memory layer for AI agents, enabling persistent context across sessions.
- **[Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm)** ⭐61,330 — Local-first agent experience with everything needed for powerful RAG workflows.
- **[thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)** ⭐81,500 — Persistent context across sessions for any agent; compresses session activity and reinjects relevant context.
- **[lancedb/lancedb](https://github.com/lancedb/lancedb)** ⭐10,556 — Embedded retrieval library for multimodal AI, developer-friendly and serverless.
- **[safishamsi/graphify](https://github.com/safishamsi/graphify)** ⭐64,299 — Turns any codebase, docs, or images into a queryable knowledge graph for AI coding assistants.

---

## 3. Trend Signal Analysis

**Explosive community attention is concentrated on two areas: local LLM benchmarking and agent skill ecosystems.** The 3,191-star surge for `last30days-skill` and 1,801-star surge for `turbovec` indicate that the community is hungry for tools that solve specific, painful problems—hardware-aware model selection and high-performance vector indexing. The simultaneous emergence of `addyosmani/agent-skills`, `phuryn/pm-skills`, and `x1xhlol/system-prompts-and-models-of-ai-tools` signals a market shift: developers no longer want monolithic agents—they want **interchangeable skill modules** that can be composed into custom agent workflows. This mirrors the transition from monolithic web frameworks to npm-like ecosystems.

**A new technical direction appearing for the first time** is the concept of a "skill marketplace" for AI coding agents. Projects like `pm-skills` and `agent-skills` package domain-specific capabilities (discovery, strategy, execution, launch) into discrete, versioned packages. This suggests the industry is converging on a standard interface for agent capabilities—a "plugin protocol" for coding agents.

**Connections to recent LLM releases are evident.** The trending list explicitly mentions support for Kimi-K2.6, GLM-5.1, MiniMax, DeepSeek, and gpt-oss in the ollama description, confirming that the open-source model ecosystem is diversifying rapidly. The rise of `whichllm` is a direct response to this fragmentation—users need help choosing among dozens of capable models. Furthermore, the `claude-mem` project's 81,500 stars reflect the growing focus on **persistent memory for agents**, a critical capability as agents transition from single-session demos to multi-day production workflows.

---

## 4. Community Hot Spots

- **`Andyyyy64/whichllm`** — The intersection of local LLM adoption and hardware diversity creates a massive pain point. This tool solves it with a single command. Expect forks and integrations with model hubs within weeks.
- **`aaif-goose/goose`** — An extensible agent that "goes beyond code suggestions," with Rust for performance. Its open extensibility model could make it the WordPress of AI agents—a base platform with plugins.
- **`addyosmani/agent-skills`** and **`phuryn/pm-skills`** — The battle for the "agent skill package" standard is happening now. These repos are the early contenders for becoming the npm/Docker Hub for AI agent capabilities.
- **`roboflow/supervision`** — Computer vision remains a bedrock AI application layer. With 733 new stars today, the ecosystem of reusable CV tools is expanding rapidly, driven by needs in manufacturing, security, and inspection.
- **`infiniflow/ragflow`** (82k stars) + **`mem0ai/mem0`** (58k stars) — RAG is evolving into **RAG + persistent memory + agents**. These two projects together represent the standard stack for building production-grade knowledge systems that remember and reason across sessions.

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*