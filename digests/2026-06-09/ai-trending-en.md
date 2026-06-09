# AI Open Source Trends 2026-06-09

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-09 02:30 UTC

---

# AI Open Source Trends Report — 2026-06-09

## 1. Today's Highlights

Agent skill ecosystems are exploding: two skill marketplaces (`last30days-skill`, `pm-skills`) and Google’s official `google/skills` all rocketed onto the trending list, signaling a shift from monolithic agents to modular, composable capabilities. A new vector index `turbovec` built on TurboQuant in Rust with Python bindings gained 1,729 stars in a day, highlighting demand for high-performance local retrieval. The open-source memory layer `MemPalace` claims best-benchmarked performance and also trended, while `Mem0` continues to dominate topic searches with 58k+ stars. The agent harness race continues: `goose` (Rust, 699 stars today) and `Agent-Reach` (zero-fee web access) show that the community wants lightweight, extensible agents that go beyond code completion.

## 2. Top Projects by Category

### 🔧 AI Infrastructure
| Project | Stars | Why It Matters Today |
|---------|-------|---------------------|
| [ollama/ollama](https://github.com/ollama/ollama) | 173,630 | Dominant local model runner; now supports Kimi-K2.6, GLM-5.1, and more. |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 82,260 | High-throughput LLM serving; essential for production deployments. |
| [RyanCodrai/turbovec](https://github.com/RyanCodrai/turbovec) | 0 (+1,729 today) | Rust-based vector index with Python bindings – new contender for local RAG. |
| [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit) | 34,182 (+378 today) | Frontend stack for agents & generative UI; powers AG-UI protocol. |
| [roboflow/supervision](https://github.com/roboflow/supervision) | 0 (+1,288 today) | Reusable computer vision tools; bridges CV and LLM workflows. |
| [aaif-goose/goose](https://github.com/aaif-goose/goose) | 0 (+699 today) | Extensible AI agent in Rust – install, execute, edit, test with any LLM. |
| [Andyyyy64/whichllm](https://github.com/Andyyyy64/whichllm) | 0 (+143 today) | One-command local LLM benchmark; helps users pick the best model for their hardware. |

### 🤖 AI Agents / Workflows
| Project | Stars | Why It Matters Today |
|---------|-------|---------------------|
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 184,849 | Pioneer of autonomous agents; continues to inspire new harnesses. |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 187,522 | The “agent that grows with you” – trending long-term. |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | 76,273 | AI-driven development agent; remains a go-to for coding tasks. |
| [bytedance/deer-flow](https://github.com/bytedance/deer-flow) | 70,758 | Long-horizon super-agent harness; researches, codes, creates. |
| [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill) | 0 (+3,558 today) | Multi-platform research agent skill – synthesizes Reddit, X, YouTube, HN, Polymarket. |
| [google/skills](https://github.com/google/skills) | 0 (+461 today) | Official Google Agent Skills (first-party). |
| [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) | 0 (+679 today) | CLI agent that reads & searches Twitter, Reddit, YouTube, GitHub, etc., zero API fees. |
| [santifer/career-ops](https://github.com/santifer/career-ops) | 50,599 (+308 today) | AI-powered job search system built on Claude Code – 14 skill modes. |

### 📦 AI Applications
| Project | Stars | Why It Matters Today |
|---------|-------|---------------------|
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 47,083 | AI productivity studio with smart chat and 300+ assistants. |
| [zhayujie/CowAgent](https://github.com/zhayujie/CowAgent) | 45,161 | Lightweight super-assistant harness; multi-model, multi-channel. |
| [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) | 41,402 | LLM-powered stock analysis with real-time news and push notifications. |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | 25,312 | AI generates real PowerPoints from any document – native shapes & audio. |

### 🧠 LLMs / Training
| Project | Stars | Why It Matters Today |
|---------|-------|---------------------|
| [huggingface/transformers](https://github.com/huggingface/transformers) | 161,421 | De facto model definition framework; supports text, vision, audio. |
| [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) | 72,005 | Unified fine-tuning for 100+ LLMs & VLMs (ACL 2024). |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,068 | Large-scale LLM evaluation platform over 100+ datasets. |

### 🔍 RAG / Knowledge
| Project | Stars | Why It Matters Today |
|---------|-------|---------------------|
| [langgenius/dify](https://github.com/langgenius/dify) | 144,452 | Production RAG + agentic workflow platform. |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 82,232 | Leading open-source RAG engine with agent capabilities. |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 58,084 | Universal memory layer for AI agents – highly active. |
| [MemPalace/mempalace](https://github.com/MemPalace/mempalace) | 0 (+170 today) | Open-source AI memory system; claims best-benchmarked performance. |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 44,686 | Cloud-native vector database for scalable ANN search. |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | 31,939 | High-performance vector search engine; widely used in RAG. |
| [Microsoft/synthetic-rag-index](https://github.com/microsoft/synthetic-rag-index) | 37 | Serverless Azure service that reduces index size by 90%+ for RAG. |

## 3. Trend Signal Analysis

**Skill-based agent ecosystems are the explosive trend.** Three projects in today’s trending list (`last30days-skill`, `pm-skills`, `google/skills`) are built around the concept of “skills” – reusable, composable capabilities that an agent can load on demand. This mirrors the MCP (Model Context Protocol) momentum and suggests the community is moving away from monolithic agent code toward modular skill marketplaces. The 3,558 one-day stars on `last30days-skill` indicate that developers are eager for curated, multi-platform research agents.

**A new high-performance vector index stack is emerging.** `turbovec` (Rust + Python bindings, +1,729 today) joins the trend of low-level, efficient retrieval engines. Combined with `MemPalace`’s claim of “best-benchmarked” memory, and `microsoft/synthetic-rag-index` (shrinking index size 90%), the RAG sector is doubling down on performance and storage efficiency rather than just feature count.

**Agent harnesses are becoming language-agnostic.** `goose` (Rust), `aaif-goose/goose`, and `rig` (Rust LLM framework) signal that Rust is gaining traction for agent infrastructure. Meanwhile, Python remains dominant for agent logic, and TypeScript for frontends (CopilotKit). The “Claude Code” ecosystem is particularly hot: multiple projects (`career-ops`, `claude-howto`, `claude-context`, `claude-mem`) explicitly build on or guide Claude Code, reflecting Anthropic’s growing influence in the open-source agent space.

**Coinciding with recent LLM releases** – ollama now supports Kimi-K2.6, GLM-5.1, etc. – the trend toward local, private, and customizable models continues. The focus on benchmarks (`whichllm`, `opencompass`) shows users demand real-world performance data, not just parameter counts.

## 4. Community Hot Spots

- **Skill marketplaces (e.g., `mvanhorn/last30days-skill`, `pm-skills`, `google/skills`)** – The modular agent skill layer is the most active new direction. Watch for cross-platform skill standards.

- **Rust-based AI infrastructure (`turbovec`, `goose`, `rig`)** – Rust is moving beyond vector databases into agent runtimes and LLM application frameworks. Expect more performance-critical tools to appear in Rust.

- **Memory and context persistence (`mem0`, `MemPalace`, `claude-mem`)** – Giving agents long-term memory across sessions is a key unsolved problem. These projects are competing on benchmarked accuracy and efficiency.

- **Claude Code ecosystem (`career-ops`, `claude-howto`, `zilliztech/claude-context`)** – The “Claude Code” plugin/agent ecosystem is exploding, fueled by Anthropic’s excellent developer experience. Developers are building vertical solutions (job search, code search, guide books).

- **Zero-fee web access agents (`Agent-Reach`, `firecrawl`, `browser-use`)** – Agents that can read and search across platforms without bloated API fees are highly sought after. Integration with Twitter, Reddit, YouTube, etc., is becoming a standard requirement.

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*