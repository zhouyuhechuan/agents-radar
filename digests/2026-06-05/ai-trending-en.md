# AI Open Source Trends 2026-06-05

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-05 02:43 UTC

---

# AI Open Source Trends Report — June 5, 2026

## 1. Today’s Highlights

The open-source AI ecosystem saw explosive growth in agent‑related infrastructure, with **ECC** (+1,750 today) and **hermes‑agent** (+1,913) emerging as the day’s stars—both are systemic agent harnesses designed to optimise performance and memory for coding assistants like Claude Code and Copilot. A new class of “pre‑LLM compression” tool, **headroom** (+3,142), attracted the most new stars by offering 60–95% token reduction on RAG chunks and tool outputs. On the application side, **open‑notebook** (+212) and **Open‑LLM‑VTuber** (+581) signal a surge in consumer‑facing AI experiences, while NVIDIA’s **cosmos** platform (steady +133) reinforces the push toward Physical AI for robotics and autonomous vehicles.

## 2. Top Projects by Category

### 🔧 AI Infrastructure (frameworks, SDKs, inference engines, dev tools)

| Project | Stars | Why it matters today |
|--------|-------|----------------------|
| [chopratejas/headroom](https://github.com/chopratejas/headroom) [Python] | 0 (+3,142 today) | A novel compression proxy/MCP server that cuts tokens by up to 95% before LLM processing—could become a standard layer in RAG pipelines. |
| [github/copilot-sdk](https://github.com/github/copilot-sdk) [Java] | 0 (+38 today) | The official multi‑platform SDK for embedding GitHub Copilot Agent into third‑party services, lowering the barrier for agent‑enabled apps. |
| [openclaw/openclaw-windows-node](https://github.com/openclaw/openclaw-windows-node) [C#] | 0 (+411 today) | Windows companion suite for the OpenClaw agent platform—includes system tray, shared libraries, and PowerToys integration, extending agent harness to desktop ecosystems. |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) [Python] | 81,957 | High‑throughput LLM inference engine—still the go‑to for self‑hosted serving of large models. |
| [Firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) [TypeScript] | 128,753 | Scalable web‑scraping API purpose‑built for AI agents; essential for grounding LLMs in live data. |

### 🤖 AI Agents & Workflows (agent frameworks, automation, multi‑agent systems)

| Project | Stars | Why it matters today |
|--------|-------|----------------------|
| [affaan-m/ECC](https://github.com/affaan-m/ECC) [JavaScript] | 207,354 (+1,750 today) | “Agent harness” for Claude Code, Codex, Cursor, etc.—optimises skills, instincts, and memory across multiple coding agents, now exploding in popularity. |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) [Python] | 181,159 (+1,913 today) | A lightweight, growing agent designed for extensibility; its rapid star gain suggests strong community anticipation for the “agent that grows with you” vision. |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) [Python] | 184,767 | The original autonomous agent framework—still the most starred, now seeing renewed interest as agent architectures mature. |
| [langgenius/dify](https://github.com/langgenius/dify) [TypeScript] | 143,905 | Production‑ready platform for building agentic workflows, bridging the gap between prototyping and deployment. |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) [Python] | 97,218 | Enables AI agents to automate websites; increasingly critical for agent‑driven web interactions. |
| [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill) [Python] | 0 (+199 today) | Agent skill that researches any topic across Reddit, X, YouTube, HN, and the web—illustrates the growing demand for plug‑and‑play agent capabilities. |

### 📦 AI Applications (specific apps, vertical solutions)

| Project | Stars | Why it matters today |
|--------|-------|----------------------|
| [NVIDIA/cosmos](https://github.com/NVIDIA/cosmos) [Jupyter Notebook] | 0 (+133 today) | Open‑source world models for Physical AI—robotics, autonomous vehicles, smart infrastructure. Backed by NVIDIA, it bridges generative AI and real‑world simulation. |
| [lfnovo/open-notebook](https://github.com/lfnovo/open-notebook) [TypeScript] | 0 (+212 today) | An open‑source, flexible alternative to NotebookLM—enables multi‑document AI notebooks with custom knowledge grounding. |
| [Open-LLM-VTuber/Open-LLM-VTuber](https://github.com/Open-LLM-VTuber/Open-LLM-VTuber) [Python] | 0 (+581 today) | Hands‑free voice interaction with any LLM plus Live2D avatars—showcases the convergence of LLMs, voice, and virtual character animation. |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) [TypeScript] | 46,882 | AI productivity studio with smart chat, autonomous agents, and 300+ assistants—a “super‑app” for daily AI use. |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) [Python] | 82,966 | Multi‑agent LLM framework for financial trading—highly topical given the intersection of agents and quantitative finance. |

### 🧠 LLMs / Training (model weights, training frameworks, fine‑tuning)

| Project | Stars | Why it matters today |
|--------|-------|----------------------|
| [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) [Jupyter Notebook] | 96,665 | Step‑by‑step implementation of a ChatGPT‑like LLM in PyTorch—essential educational resource for new model builders. |
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) [Python] | 51,143 | Train a 64M‑parameter LLM from scratch in 2 hours—democratises LLM training for hobbyists and researchers. |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) [Python] | 7,060 | Comprehensive LLM evaluation platform with 100+ datasets—critical for model comparison and quality assurance. |
| [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) [Rust] | 7,528 | Modular LLM application framework in Rust—signals growing interest in performant, type‑safe agent infrastructure. |

### 🔍 RAG / Knowledge (vector databases, retrieval‑augmented generation, knowledge management)

| Project | Stars | Why it matters today |
|--------|-------|----------------------|
| [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) [Python] | 79,950 (+141 today) | OCR toolkit that converts PDFs/images into structured data for LLMs—a key pipeline for document‑grounded RAG, now with 100+ language support. |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) [Python] | 81,933 | Leading open‑source RAG engine with agent capabilities—blends retrieval, reasoning, and tool use. |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) [Python] | 57,731 | Universal memory layer for AI agents—enables persistent context across sessions, a critical missing piece for many agent deployments. |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) [TypeScript] | 80,688 | Captures and compresses agent sessions, injects relevant context into future sessions—another memory solution gaining massive traction. |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) [Go] | 44,629 | High‑performance cloud‑native vector database—remains the backbone for scalable similarity search in RAG stacks. |
| [topoteretes/cognee](https://github.com/topoteretes/cognee) [Python] | 17,673 | “Memory platform for AI Agents in 6 lines of code”—simplifies persistent knowledge. |

## 3. Trend Signal Analysis

The most explosive community attention today is squarely on **agent‑centric infrastructure and memory management**. Two of the top three trending repos—**ECC** and **hermes‑agent**—are not consumer apps but systems that optimise how coding agents (Claude Code, Codex, OpenCode, etc.) operate, store memory, and manage skills. This reflects a maturation of the agent ecosystem: the initial rush of “agent frameworks” is giving way to specialised tools for performance, persistence, and multi‑agent coordination.

A new category emerging for the first time is **pre‑LLM token compression** (e.g., **headroom**). Rather than modifying the LLM itself, projects like headroom compress tool outputs, logs, and RAG chunks before they reach the model, achieving 60–95% token reductions with identical answers. This is a pragmatic response to the high cost of context windows and API tokens, and could become a standard layer in agent and RAG pipelines.

There is also a clear connection to recent industry events: the prominence of **agent harnesses** (ECC, hermes‑agent) aligns with the early‑2026 release of **Claude Code** and the expansion of **GitHub Copilot Agent**. Developers are rushing to build scaffolding that makes these commercial agents more efficient, portable, and memory‑aware. The simultaneous popularity of **claude-mem** (80k stars) and **mem0** (57k stars) underscores that memory is the key unsolved challenge for agents that need to maintain long‑term context.

Finally, **Physical AI** (NVIDIA cosmos) and **multimodal interaction** (Open‑LLM‑VTuber) show that the open‑source community is not limiting itself to text—vision, voice, and simulation are becoming first‑class citizens in the AI toolbox.

## 4. Community Hot Spots

- **Agent Harnesses** — Projects like **ECC** (+1,750 today) and **hermes-agent** (+1,913) are the fastest‑growing repos. Developers are actively seeking ways to boost agent performance and integrate memory. Worth diving into the “skills, instincts, memory” architecture they introduce.
- **Token Compression** — **headroom** (+3,142) is the day’s top star‑getter. Its approach of compressing inputs before LLM calls could reshape how RAG and agent tools are built. Consider experimenting with its MCP server integration.
- **Agent Memory & Persistence** — **thedotmack/claude-mem** (80k stars) and **mem0** (57k stars) are both solving context retention. Their rapid adoption indicates a major pain point in production agents.
- **Open‑Source NotebookLM Alternatives** — **open‑notebook** (+212 today) offers a flexible, self‑hosted version of Google’s NotebookLM. With privacy concerns growing, this could become a cornerstone for enterprise knowledge management.
- **Physical AI Platforms** — NVIDIA’s **cosmos** is still early but its steady star growth signals developer interest in world models for robotics and autonomous systems. Worth monitoring for upcoming model releases and tooling.

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*