# AI 开源趋势日报 2026-07-26

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-26 02:03 UTC

---

# AI 开源趋势日报（2026-07-26）

---

## 1. 今日速览

今日 AI 开源领域出现 **三大显性热点**：**Agent 技能与框架** 持续发酵，`affaan-m/ECC` 和 `mattpocock/skills` 等风格各异的“Agent 技能场”项目单日吸星超 2000；**AI 原生浏览器与代理容器** 成为新增长点，`citrolabs/ego-lite` 以 986 颗 star 证明“浏览器即 Agent 环境”的需求；**金融大模型** 首次登上 Trending 榜，`shiyu-coder/Kronos` 代表垂直领域 LLM 正在从概念走向可复现的开源项目。此外，阿里巴巴开源的 `alibaba/open-code-review`（+431 star） 验证了 **LLM + 确定性工程** 混合架构在企业级工具中的可行性。

---

## 2. 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、CLI）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [ollama/ollama](https://github.com/ollama/ollama) ⭐176,892 | 一键运行 K2.6、DeepSeek 等主流模型，已成为本地 LLM 部署的事实标准 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) ⭐87,153 | 高吞吐 LLM 推理引擎，支持 PagedAttention 和多种量化，生产级首选 |
| [andrewyng/aisuite](https://github.com/andrewyng/aisuite) ⭐ 总量未知 (+77 today) | Andrew Ng 出品，统一多 AI 提供商接口的轻量 Python 库，降低切换成本 |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) ⭐156,006 | 专为 Agent 设计的网页抓取与结构化提取 API，今日仍保持高人气 |
| [automattic/harper](https://github.com/Automattic/harper) ⭐ (+503 today) | 离线、隐私优先的 Rust 语法检查器，虽无明确 AI 标注但底层依赖 ML 模型 |
| [RyanCodrai/turbovec](https://github.com/RyanCodrai/turbovec) ⭐ (+86 today) | 基于 TurboQuant 的向量索引，Rust 核心 + Python 绑定，适合低延迟检索 |

### 🤖 AI 智能体 / 工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [affaan-m/ECC](https://github.com/affaan-m/ECC) ⭐233,328 (+377 today) | “Agent 技能性能优化系统”，集技能、记忆、安全于一体，支持 Claude Code / Codex 等主流 CLI |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) ⭐142,587 | Agent 工程平台，今日仍是 RAG 和 Tool Calling 的核心依赖 |
| [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph) ⭐38,139 | 构建弹性 Agent 工作流的图框架，与 LangChain 互补 |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) ⭐185,685 | 老牌自主 Agent，持续迭代，今日社区讨论活跃 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) ⭐106,770 | 让 AI Agent 能像人一样操作浏览器，实现网页自动化 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) ⭐220,486 | “随着你成长的 Agent”，强调记忆与自适应 |
| [obra/superpowers](https://github.com/obra/superpowers) ⭐ (+479 today) | 一套 Agent 技能框架与软件开发方法论，今日新晋 trending |

### 📦 AI 应用（具体产品、垂直场景解决方案）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [alibaba/open-code-review](https://github.com/alibaba/open-code-review) ⭐ (+431 today) | 阿里巴巴开源的 LLM + 确定性管道混合代码审查工具，支持 NPE、SQL 注入等规则 |
| [shiyu-coder/Kronos](https://github.com/shiyu-coder/Kronos) ⭐ (+319 today) | 金融领域基础模型，用语言模型建模金融市场，首次登榜 |
| [palmier-io/palmier-pro](https://github.com/palmier-io/palmier-pro) ⭐ (+412 today) | 面向 AI 的 macOS 视频编辑器，原生集成 AI 剪辑 |
| [OtterMind/Chat2DB](https://github.com/OtterMind/Chat2DB) ⭐ (+360 today) | AI 驱动的数据库客户端，支持自然语言查询多款数据库 |
| [MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) ⭐99,290 | AI 自动生成高清短视频工具，持续受到内容创作者追捧 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) ⭐48,985 | 多模型聚合的 AI 生产力工作室，支持智能体与 300+ 助手插件 |

### 🧠 大模型 / 训练（模型推理、微调、评估）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) ⭐53,841 | 从零训练 64M 参数 LLM，2 小时可复现，适合学习与研究 |
| [Lordog/dive-into-llms](https://github.com/Lordog/dive-into-llms) ⭐ (+408 today) | 《动手学大模型》系列编程实践教程，今日新增 star 408 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) ⭐4,408 | 在 Apple Silicon 上构建微型 vLLM + Qwen 的教学项目 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) ⭐7,236 | 开源 LLM 评测平台，支持 100+ 数据集与主流模型 |
| [Picovoice/picollm](https://github.com/Picovoice/picollm) ⭐315 | 设备端 LLM 推理引擎，采用 X-Bit 量化，适合边缘部署 |

### 🔍 RAG / 知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) ⭐85,993 | 领先的开源 RAG 引擎，融合 Agent 能力，提供强大上下文层 |
| [Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm) ⭐63,838 | 本地优先的 RAG 应用，支持多模型与文档管理 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) ⭐61,685 | 通用记忆层，为 AI Agent 提供持久化上下文 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) ⭐45,381 | 云原生高性能向量数据库，是大规模 RAG 的基石 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) ⭐33,585 | Rust 编写的高性能向量搜索引擎，支持过滤与混合检索 |
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) ⭐95,885 | 将代码库、文档转为可查询的知识图谱，专为 Claude Code 等 Agent 设计 |

---

## 3. 趋势信号分析

**Agent 技能场（Skill Harness）爆发**：`affaan-m/ECC`（+377）、`mattpocock/skills`（+1740）、`obra/superpowers`（+479） 三个项目均聚焦于 **为 CLI Agent 提供结构化技能与记忆管理**，且都明确针对 Claude Code、Codex 等流行 Agent 终端。这反映出社区正从“调用 API”转向“构建可复用、可组合的 Agent 技能库”，类似早期 npm 之于 Node.js。

**“AI 原生浏览器”新品类诞生**：`citrolabs/ego-lite`（+986） 被定位为“为 AI Agent 运行的最快浏览器”，主打共享登录态、零配置、不打扰用户。它直接服务于 Codex/Claude Code 等自动操作网页的场景，表明 **Agent 基础设施正在细分出独立的“Agent 操作系统”**。

**金融 + LLM 垂直化落地**：`shiyu-coder/Kronos`（+319） 是首个以“金融语言基础模型”身份登上 Trending 的项目，表明 LLM 在量化交易、市场分析领域的开源复现已获关注。同期 `ZhuLinsen/daily_stock_analysis`（⭐58,808） 也是 LLM 驱动的股票分析系统，说明金融 AI 正在成为独立赛道。

**混合架构在企业级工具中升温**：阿里巴巴的 `open-code-review` 采用“确定性管道 + LLM Agent”的混合设计，既保证规则检查的精确性，又利用 LLM 进行上下文理解。这种思路与近期大模型厂商强调的“可观测、可控制”趋势一致，可能成为未来代码审查、安全审计等工具的标配。

---

## 4. 社区关注热点

- **ECC / 技能场项目**：`affaan-m/ECC` 12 小时内获得超过 2000 star（结合两次数据），说明社区对 **Agent 性能、记忆、安全** 的整合方案极度渴求。该仓库同时出现在 Trending 和主题搜索中，是今日最热项目。
- **claude-cookbooks 与 awesome-claude-skills**：Anthropic 官方 `claude-cookbooks` 和社区 `awesome-claude-skills` 双双上榜，表明 **Claude 生态的工具化** 正在加速，开发者急需可复用的最佳实践。
- **browser-use 与 ego-lite**：两者均聚焦“Agent 操作网页”，但路线不同：前者是 Python 库，后者是独立浏览器。值得持续关注 **Agent 与浏览器交互的标准化** 方向。
- **金融大模型 Kronos**：如果你关注垂直领域 LLM，可以深入 Fork 研究其数据处理和训练方法，它代表了语言模型在量化场景的新尝试。
- **dive-into-llms 与 minimind**：两本“从零学 LLM”教程同时获得高热度，说明 **入门级实战资源** 缺口仍然巨大，适合教育类创作者和社区贡献者投入。

---

*报告生成时间：2026-07-26 20:00 UTC | 数据来源：GitHub Trending & Topic Search*

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*