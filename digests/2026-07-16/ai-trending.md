# AI 开源趋势日报 2026-07-16

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-16 01:55 UTC

---

# AI 开源趋势日报 | 2026-07-16

## 1. 今日速览

- **AI Agent 技能包集中爆发**：Trending 榜上三个专门为 Claude Code、Cursor 等 AI 编码代理提供“技能”的仓库（`hallmark`、`skills`、`marketingskills`）今日合计新增近 3800 star，反映出社区正从“使用工具”转向“为工具定制行为规范与能力”。
- **AI Agent 安全与治理首次登榜**：`destructive_command_guard` 以 Rust 实现的危险命令拦截器，今日新增 471 star，表明开发者对 AI 代理执行系统级命令时的风险控制需求激增。
- **交易与教育垂直场景 Agent 热度高**：`Vibe-Trading`（个人交易 Agent）和 `DeepTutor`（终身个性化辅导）双双来自 HKUDS 实验室，合计新增超 1000 star，说明 AI Agent 在金融、教育等领域的落地尝试正获得早期关注。
- **开源 Copilot 替代生态持续壮大**：`awesome-llm-apps` 今日新增 1236 star，而主题搜索中 `CherryStudio`、`anything-llm`、`open-webui` 等本地优先的 AI 应用平台 star 总量均处高位，本地化 Agent 与 RAG 工具链已成主流。

## 2. 各维度热门项目

### 🔧 AI 基础工具（框架、推理引擎、CLI、开发工具）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|-----------|
| [ollama/ollama](https://github.com/ollama/ollama) | 176k | — | 开箱即用的本地 LLM 运行工具，支持数十种主流模型，今日更新提到支持 Kimi-K2.6 等最新模型。 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | 162k | — | 模型定义与训练框架，覆盖文本、视觉、音频、多模态，是 AI 开发者的核心基础设施。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 86k | — | 高吞吐低延迟的 LLM 推理引擎，PagedAttention 技术被广泛采用，支撑大量生产级部署。 |
| [openinterpreter/openinterpreter](https://github.com/openinterpreter/openinterpreter) | — | +299 today | 面向低成本模型的编码 Agent，强调轻量级、本地运行，适合开发测试环境。 |
| [Firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | 151k | — | 可扩展的网页搜索与抓取 API，专为 AI Agent 提供的互联网接口。 |
| [langchain4j/langchain4j](https://github.com/langchain4j/langchain4j) | 12.6k | — | Java 生态的 LangChain 替代，整合 MCP、工具调用、RAG，适合企业级 JVM 应用。 |

### 🤖 AI 智能体 / 工作流（Agent 框架、自动化、多智能体系统）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|-----------|
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 215k | — | 通用 AI Agent 框架，强调“与用户共同成长”，支持多工具、多模型、长期记忆。 |
| [langgenius/dify](https://github.com/langgenius/dify) | 149k | — | 生产级 Agent 工作流开发平台，可视化编排，内置 RAG、工具、插件生态。 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | 142k | — | Agent 工程平台，提供链、工具、记忆等抽象，是当前最流行的 LLM 应用开发框架。 |
| [AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 186k | — | 早期引爆 AI Agent 概念的开源项目，持续迭代支持多模态、长期目标规划。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 105k | — | 让 AI Agent 像人一样操作网页，自动化完成复杂在线任务。 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | 81k | — | 全栈 AI 编码代理，可自主完成 GitHub Issue 到 PR 的完整开发流程。 |
| [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit) | 36k | — | 前端 Agent 栈，支持 React、Angular、移动端，提供 AG-UI 协议。 |
| [mattpocock/skills](https://github.com/mattpocock/skills) | — | +2130 today | 真实工程师的 .claude 技能目录，教你如何让 Claude Code 写出更可靠的代码。 |

### 📦 AI 应用（具体产品场景、垂直领域解决方案）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|-----------|
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | 146k | — | 最受欢迎的自托管 AI 聊天界面，支持 Ollama、OpenAI 等后端，内置 RAG 与工具。 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 49k | — | AI 生产力工作室，集成智能聊天、自主 Agent、300+ 助手，统一访问主流 LLM。 |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 85k | — | 权威的开源 RAG 引擎，融合 Agent 能力，构建高质量上下文层。 |
| [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) | 86k | — | 将任意 PDF/图像转为结构化数据，多语言 OCR 工具，是 LLM 和文档管道的桥梁。 |
| [HKUDS/Vibe-Trading](https://github.com/HKUDS/Vibe-Trading) | 23.7k | +915 today | 个人交易 Agent，基于 LLM 进行市场分析、策略执行，今日热度极高。 |
| [moeru-ai/airi](https://github.com/moeru-ai/airi) | — | +110 today | 自托管的 Grok 风格伴侣 Agent，支持实时语音、Minecraft、Factorio 游戏互动。 |
| [HKUDS/DeepTutor](https://github.com/HKUDS/DeepTutor) | — | +172 today | 终身个性化辅导 Agent，可智能推送学习内容、评估掌握程度。 |

### 🧠 大模型 / 训练（模型权重、训练框架、微调工具）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|-----------|
| [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | 99k | — | 从零实现类 ChatGPT 模型的教学项目，PyTorch 代码清晰，适合深度学习。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7.2k | — | 全面的大模型评估平台，支持 100+ 数据集和数十个模型系列。 |
| [AarambhDevHub/aarambh-ai](https://github.com/AarambhDevHub/aarambh-ai) | 26 | — | 纯 Rust/Candle 实现的 Decoder-only LLM，支持多模态、MoE、DPO，开源教育价值高。 |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | 285 | — | 可靠、可扩展的基础模型预训练库，支持世界模型。 |
| [R-D-BioTech-Alaska/Qelm](https://github.com/R-D-BioTech-Alaska/Qelm) | 27 | — | 量子增强语言模型，探索量子计算与 LLM 结合的新方向。 |

### 🔍 RAG / 知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|-----------|
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 45k | — | 云原生高性能向量数据库，专为 ANN 搜索设计，是 RAG 链路的标配组件。 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | 33k | — | 高密度向量数据库，支持过滤、分组，提供云服务，性能优异。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 61k | — | 通用 Agent 记忆层，持久化跨会话上下文，内置压缩与检索。 |
| [NirDiamant/RAG_Techniques](https://github.com/NirDiamant/RAG_Techniques) | 28.6k | — | RAG 技术教程集合，每个技术附有 Jupyter Notebook 实现，是学习进阶宝典。 |
| [siyuan-note/siyuan](https://github.com/siyuan-note/siyuan) | 45k | — | 隐私优先的个人知识管理软件，支持双向链接、AI 助手，可本地部署。 |
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | 88k | — | 将任意代码/文档/图像转为知识图谱的 AI 编码助手技能，支持多种 Agent 环境。 |
| [langgenius/dify](https://github.com/langgenius/dify) | 149k | — | 虽已列入 Agent 类，但其核心能力之一是可视化 RAG 管道编排，同样适合本维度。 |

## 3. 趋势信号分析

### 🚀 AI 代理“技能市场”正在形成
`hallmark`、`skills`、`marketingskills` 三个仓库今日合计新增近 3700 star，它们并非完整的 Agent 框架，而是面向 Claude Code、Cursor 等的“行为指南”或“规则文件”。这标志着 AI 编码代理的生态从“用工具”进入“定制行为”阶段——开发者不再满足于开箱即用，而是需要精确控制代理的思考方式（如反 AI 废话、代码质量规范、营销文案风格）。**可复用的技能文件可能成为类似 npm 的包管理新形态**。

### 🛡️ Agent 安全落地需求急迫
`destructive_command_guard` 以 Rust 实现轻量级命令拦截器，今日新增 471 star。随着 AI Agent 被授予 shell 执行权限，误操作或恶意指令的风险成为实际痛点。该工具填补了“Agent 沙箱”与“用户监督”之间的空白，让开发者可以安全地在大模型环境中运行危险命令。类似的安全组件可能会被集成到主流 Agent 框架中。

### 🏛️ 垂直场景 Agent 获高校实验室青睐
HKUDS 实验室连续推出 `Vibe-Trading`（金融交易）和 `DeepTutor`（教育辅导），两个项目在 Trending 榜上均表现亮眼。这类垂直 Agent 不再泛化“万能助手”，而是聚焦特定领域的数据、规则与工作流，更易落地和验证价值。**Agent 的“专精化”趋势或将在未来数月内加剧**。

## 4. 社区关注热点

- **🤖 [mattpocock/skills](https://github.com/mattpocock/skills)（+2130 today）**：来自知名 TypeScript 专家的 Claude Code 技能集，可作为 Agent 行为编程的最佳实践模板，值得每位 AI 编码代理用户参考。
- **🔒 [Dicklesworthstone/destructive_command_guard](https://github.com/Dicklesworthstone/destructive_command_guard)（+471 today）**：首个针对 Agent 的 git/shell 危险命令防护器，安全性成为 Agent 落地的前置条件。
- **📈 [HKUDS/Vibe-Trading](https://github.com/HKUDS/Vibe-Trading)（+915 today）**：全栈个人交易 Agent，代码开源且结构清晰，适合对金融 + AI 感兴趣的开发者 fork 二开。
- **🧩 [Shubhamsaboo/awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps)（+1236 today）**：100+ 可实际运行的开源 AI Agent 和 RAG 应用合集，是所有想快速构建原型开发者的“一键启动”宝典。
- **📚 [HenryNdubuaku/maths-cs-ai-compendium](https://github.com/HenryNdubuaku/maths-cs-ai-compendium)（+725 today）**：面向 AI/ML 研究工程师的知识体系与学习路线图，对想要系统入门或进阶的开发者有极高价值。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*