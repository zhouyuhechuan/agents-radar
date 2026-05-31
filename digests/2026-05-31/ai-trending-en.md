# AI Open Source Trends 2026-05-31

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-05-31 06:56 UTC

---

# AI Open Source Trends Report — 2026-05-31

## 1. Today’s Highlights

The open-source AI community is experiencing an explosive wave of **agent-centric tooling**, with Anthropic’s **Claude Code** and the newly public **anthropics/skills** repository driving a surge in agent harnesses, plugin ecosystems, and skill-marketplaces. **MoneyPrinterTurbo** continues its viral run, adding +2,768 stars today for one-click AI video generation. Meanwhile, a new breed of **world model** and **speech synthesis** projects (VoxCPM, MOSS-TTS, stable‑worldmodel) signal a maturing of generative audio and simulation research. The **RAG / vector‑database** domain remains steady, with lightweight parsers (liteparse) and memory layers (mem0, cognee) gaining traction. Overall, the trend is toward **narrow, ready‑to‑use AI agents** that wrap powerful foundational models into specialized workflows.

## 2. Top Projects by Category

### 🔧 AI Infrastructure
| Project | Stars | Why It Matters Today |
|---------|-------|----------------------|
| [ollama/ollama](https://github.com/ollama/ollama) | 172,691 total | The on‑ramp for local LLMs; now supports Kimi‑K2.5, GLM‑5, and more models. |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 81,460 total | High‑throughput inference engine for LLMs – the de‑facto serving layer. |
| [microsoft/markitdown](https://github.com/microsoft/markitdown) | +2,470 today | Python tool to convert any file/office doc to Markdown – critical for RAG pipelines. |
| [run-llama/liteparse](https://github.com/run-llama/liteparse) | +925 today | Fast, open‑source document parser written in Rust – a potential replacement for heavier OCR stacks. |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | 4,217 total | Educational course on building LLM inference serving on Apple Silicon – bridges systems engineering and AI. |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | 239 total | Minimal library for pretraining foundation & world models – research‑grade infrastructure. |
| [cursor/plugins](https://github.com/cursor/plugins) | +205 today | Cursor’s plugin specification – standardising how AI coding tools extend functionality. |
| [langchain4j/langchain4j](https://github.com/langchain4j/langchain4j) | 12,155 total | Java’s answer to LangChain: LLM‑powered apps with MCP, agents, and RAG for the JVM. |

### 🤖 AI Agents / Workflows
| Project | Stars | Why It Matters Today |
|---------|-------|----------------------|
| [anthropics/claude-code](https://github.com/anthropics/claude-code) | +592 today | Agentic coding tool in the terminal – the flagship product driving today’s agent ecosystem. |
| [anthropics/skills](https://github.com/anthropics/skills) | +454 today | Public repository for Agent Skills – a marketplace for reusable agent capabilities. |
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | 199,534 total (+908 today) | “Agent harness performance optimization” – a meta‑skill system for Claude Code, Codex, and Cursor. |
| [revfactory/harness](https://github.com/revfactory/harness) | +55 today | Designs domain‑specific agent teams and generates skills – a meta‑agent framework. |
| [EveryInc/compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin) | +349 today | Official plugin for Claude Code, Codex, Cursor, etc. – standardising agent orchestration. |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 173,985 total | “The agent that grows with you” – a popular personal agent framework. |
| [langgenius/dify](https://github.com/langgenius/dify) | 143,231 total | Production‑ready platform for agentic workflow development – low‑code agent building. |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 96,352 total | Makes websites accessible to AI agents – automating browser tasks via natural language. |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | 81,077 total | Multi‑agent LLM framework for financial trading – vertical agent specialization. |
| [shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) | 63,749 total | A nano agent harness from scratch – educational deep‑dive into building Claude‑Code‑like capabilities. |

### 📦 AI Applications
| Project | Stars | Why It Matters Today |
|---------|-------|----------------------|
| [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | +2,768 today | AI‑powered short‑video generation – one‑click content creation that’s still trending. |
| [OpenBMB/VoxCPM](https://github.com/OpenBMB/VoxCPM) | +779 today | Tokenizer‑free TTS for multilingual speech, voice cloning, and creative voice design. |
| [OpenMOSS/MOSS-TTS](https://github.com/OpenMOSS/MOSS-TTS) | +62 today | Family of speech/sound generation models – covers long‑form speech, dialogue, and real‑time streaming. |
| [ruvnet/RuView](https://github.com/ruvnet/RuView) | +655 today | Turns WiFi signals into spatial intelligence and vital‑sign monitoring – no cameras needed. |
| [Crosstalk-Solutions/project-nomad](https://github.com/Crosstalk-Solutions/project-nomad) | +469 today | Offline survival computer with AI – resilience and privacy in a self‑contained device. |
| [FareedKhan-dev/train-llm-from-scratch](https://github.com/FareedKhan-dev/train-llm-from-scratch) | +327 today | Straightforward guide for training your own LLM – from data to text generation. |
| [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) | 39,538 total | LLM‑driven stock analysis for A/H/US markets – zero‑cost, scheduled automation. |

### 🧠 LLMs / Training
| Project | Stars | Why It Matters Today |
|---------|-------|----------------------|
| [huggingface/transformers](https://github.com/huggingface/transformers) | 161,087 total | Still the de‑facto library for model definition across text, vision, audio, and multimodal. |
| [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) | 71,729 total | Unified fine‑tuning of 100+ LLMs & VLMs – the go‑to for efficient training. |
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) | 50,860 total | Train a 64M‑parameter LLM from scratch in 2 hours – democratising pretraining. |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,048 total | LLM evaluation platform supporting 100+ datasets – critical for benchmarking. |
| [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) | 7,468 total | Modular LLM application framework in Rust – performance‑first approach. |
| [galilai-group/stable-worldmodel](https://github.com/galilai-group/stable-worldmodel) | +318 today | Platform for reproducible world model research – connects reinforcement learning and generative modeling. |
| [thinkwee/AgentsMeetRL](https://github.com/thinkwee/AgentsMeetRL) | 1,467 total | Awesome list for Agentic RL – bridging reinforcement learning and agent workflows. |

### 🔍 RAG / Knowledge
| Project | Stars | Why It Matters Today |
|---------|-------|----------------------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 81,577 total | Leading open‑source RAG engine with agent capabilities – combines retrieval and action. |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 44,550 total | Cloud‑native vector database for scalable ANN search – the backbone of many RAG stacks. |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 57,172 total | Universal memory layer for AI agents – persistent context across sessions. |
| [HKUDS/LightRAG](https://github.com/HKUDS/LightRAG) | 35,987 total | Simple & fast RAG library (EMNLP 2025) – research‑grade retrieval made practical. |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | 79,796 total | Captures agent session context and injects it into future sessions – solves the memory problem for coding agents. |
| [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) | 79,099 total | Turns images/PDFs into structured data for AI – 100+ language OCR. |
| [StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN) | 11,829 total | MLsys 2026 paper: 97% storage savings for RAG on personal devices – efficient private retrieval. |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | 31,689 total | High‑performance vector database written in Rust – popular for real‑time AI search. |

## 3. Trend Signal Analysis

**Agent Harness Explosion**  
The most pronounced signal today is the rapid proliferation of “agent harness” projects – frameworks that sit on top of agentic coding tools like Claude Code, Codex, and Cursor. Repos such as **ECC** (199k total stars), **compound-engineering-plugin**, **revfactory/harness**, and **anthropics/skills** are creating a meta‑layer for skill definition, performance optimization, and plugin interoperability. This suggests the community is moving beyond single‑agent use cases toward coordinated agent teams and skill marketplaces.

**Vertical AI Applications Surge**  
Two contrasting verticals are generating high star velocities: **content generation** (MoneyPrinterTurbo at +2,768) and **speech/sound generation** (VoxCPM +779, MOSS‑TTS +62). The former confirms that short‑video AI remains a killer app; the latter signals growing demand for high‑fidelity, multilingual TTS with voice cloning, dialogue, and real‑time capabilities. Additionally, **RuView** (WiFi‑based sensing) and **project‑nomad** (offline AI computer) indicate interest in AI that works without traditional sensor inputs or cloud connectivity.

**Memory & Persistence as First‑Class Citizens**  
The RAG category is evolving into “memory for agents.” Projects like **claude‑mem** (79k stars), **mem0** (57k), and **cognee** (17.5k) are not just retrieval tools – they capture session context, compress it, and inject it into future interactions. This aligns with the agent harness trend: agents are only useful if they remember. **LEANN** (97% storage savings) shows that memory efficiency is a priority, especially for on‑device deployments.

**New Technical Directions**
- **World models** (stable‑worldmodel +318) and **stable‑pretraining** (+239) bring rigorous reproducibility to foundation‑model pretraining and RL‑based simulation.
- **Tokenizer‑free TTS** (VoxCPM) challenges the traditional text‑to‑speech pipeline.
- **Rust adoption** is spreading from parsers (liteparse) to vector databases (qdrant) and LLM frameworks (rig), reflecting a community push for performance without sacrificing safety.

**Industry Connections**  
Anthropic’s open‑sourcing of **Claude Code** and the **skills** repository is likely driving the agent harness boom. Combined with OpenAI’s Codex and Cursor’s plugin ecosystem, we are witnessing a multi‑vendor standardisation of how agent behavior is packaged and shared. The rapid star growth of **ECC** and **compound-engineering-plugin** suggests developers are eagerly adopting these cross‑platform agent tools.

## 4. Community Hot Spots

- **Agent Harnesses and Plugins** – Projects like **ECC**, **compound-engineering-plugin**, and **revfactory/harness** are defining the next layer of agent orchestration. Developers should explore them to build reusable skills and multi-agent teams.
- **Claude Code Ecosystem** – With **anthropics/skills** now public, contributing skills and learning how to extend Claude Code will become a valuable skill. Also check **learn-claude-code** for a tutorial.
- **Memory for Agents** – **claude‑mem**, **mem0**, and **LEANN** represent critical infrastructure for persistent, context‑aware agents. Expect further consolidation around these memory layers.
- **Speech & Sound Generation** – **VoxCPM** and **MOSS‑TTS** are pushing boundaries in voice cloning and real‑time streaming. Open‑source alternatives to proprietary TTS APIs are getting production‑ready.
- **Lightweight Document Parsing** – **liteparse** (Rust) and **markitdown** (Python) are making it trivial to bring real‑world documents into AI pipelines. Combining them with **PaddleOCR** or **LightRAG** enables end‑to‑end document‑to‑knowledge workflows.

---

*Report generated from GitHub trending (2026‑05‑31) and AI topic search results. All star counts are as observed on the retrieval date.*

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*