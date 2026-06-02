# AI 开源趋势日报 2026-06-02

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-02 02:52 UTC

---

## 《AI 开源趋势日报》| 2026-06-02

---

### 1. 今日速览

今日 GitHub Trending 上 **AI Agent 相关项目占据半壁江山**，多智能体金融交易框架 `TradingAgents` 与基于 Hermes 的 WebUI 工具 `hermes-webui` 热度飙升。视频生成工具 `MoneyPrinterTurbo` 以 **+3375 stars** 领跑今日新增，彰显 AI 内容创作需求持续旺盛。语音合成领域迎来新突破：OpenBMB 开源的 `VoxCPM` 实现无分词器多语言语音生成及真假声克隆。与此同时，从零训练大语言模型（`train-llm-from-scratch`）和 AI 记忆层（`supermemory`）也获得社区高度关注，显示出开发者对底层能力建立的强烈兴趣。

---

### 2. 各维度热门项目

#### 🔧 AI 基础工具（框架、SDK、推理引擎、CLI）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [ollama/ollama](https://github.com/ollama/ollama) | ⭐172,862 | 本地运行 LLM 的最流行工具，现已支持 Kimi、GLM、DeepSeek 等最新模型。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | ⭐81,637 | 高吞吐、高内存效率的 LLM 推理与 serving 引擎，生产部署首选。 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | ⭐161,180 | 定义状态的最前沿 ML 模型加载、推理与训练框架。 |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | ⭐127,345 | 专为 AI agent 设计的规模化网页搜索、抓取与交互 API。 |
| [dmtrKovalenko/fff](https://github.com/dmtrKovalenko/fff) | ⭐0 (+135 today) | 极速文件搜索工具，为 AI agents 提供近乎瞬时的本地文件检索。 |
| [p-e-w/heretic](https://github.com/p-e-w/heretic) | ⭐0 (+249 today) | 全自动语言模型审查移除工具，帮助突破不必要的限制。 |
| [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) | ⭐7,487 | Rust 生态中模块化、可扩展的 LLM 应用构建框架。 |

#### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [langgenius/dify](https://github.com/langgenius/dify) | ⭐143,455 | 生产级 AI 工作流开发平台，支持可视化构建 Agent 与 RAG。 |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | ⭐184,704 | 实现 AI 民主化的自主 agent 系统，人人可用的自动化工具。 |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | ⭐81,840 (+299 today) | 基于多智能体 LLM 的金融交易框架，今日 Trending 热门。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | ⭐176,112 | 伴随你成长的智能 agent，其 WebUI 子项目 `hermes-webui` 今日 +945 stars。 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | ⭐75,612 | AI 驱动开发助手，能编写、运行和调试代码。 |
| [can1357/oh-my-pi](https://github.com/can1357/oh-my-pi) | ⭐0 (+335 today) | 终端 AI 编码 agent，支持 hash-anchored 编辑、LSP、浏览器等能力。 |
| [revfactory/harness](https://github.com/revfactory/harness) | ⭐0 (+524 today) | 元技能：设计领域特定 agent 团队并生成其使用的技能。 |
| [EveryInc/compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin) | ⭐0 (+417 today) | 统一 Claude Code、Codex、Cursor 等 Agent 的工程插件。 |

#### 📦 AI 应用（具体产品、垂直场景）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | ⭐0 (+3375 today) | 利用 AI 大模型一键生成高清短视频，今日新增 stars 最高。 |
| [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | ⭐0 (+485 today) | 设计语言模板，让 AI 辅助设计更加精准和美观。 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | ⭐46,719 | 全能 AI 生产力工作室，集成智能聊天、自主 agents 与 300+ 助手。 |
| [stefan-jansen/machine-learning-for-trading](https://github.com/stefan-jansen/machine-learning-for-trading) | ⭐0 (+93 today) | 《机器学习量化交易》第二版配套代码，实践导向的金融 AI 教科书。 |
| [zhayujie/CowAgent](https://github.com/zhayujie/CowAgent) | ⭐45,011 | 开源超级 AI 助手，具备任务规划、工具调用、记忆与知识自主成长能力。 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | ⭐23,365 | 一键将文档生成可编辑的 PowerPoint，含动画、语音注释。 |

#### 🧠 大模型/训练（模型权重、训练框架、微调）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) | ⭐71,774 | 统一高效微调 100+ LLM 与 VLM 的工具（ACL 2024）。 |
| [OpenBMB/VoxCPM](https://github.com/OpenBMB/VoxCPM) | ⭐0 (+888 today) | 无分词器多语言语音生成模型，支持创意语音设计与高保真克隆。 |
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) | ⭐50,971 | 2 小时从零训练 64M 参数 LLM 的教程，极低门槛。 |
| [FareedKhan-dev/train-llm-from-scratch](https://github.com/FareedKhan-dev/train-llm-from-scratch) | ⭐0 (+861 today) | 从数据下载到文本生成，一条龙训练 LLM 的实用指南。 |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | ⭐244 | 可靠、可扩展的基础模型与世界模型预训练库。 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | ⭐4,232 | 在 Apple Silicon 上学习 LLM 推理 serving 的课程项目：构建微型 vLLM + Qwen。 |

#### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | ⭐81,681 | 领先的开源 RAG 引擎，融合 Agent 能力为 LLM 提供优质上下文层。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | ⭐44,582 | 高性能、云原生的向量数据库，支撑大规模向量 ANN 搜索。 |
| [supermemoryai/supermemory](https://github.com/supermemoryai/supermemory) | ⭐0 (+647 today) | 极速、可扩展的记忆引擎与 API，为 AI 时代提供持久记忆。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | ⭐57,339 | AI agents 的通用记忆层，支持长期记忆与上下文注入。 |
| [HKUDS/LightRAG](https://github.com/HKUDS/LightRAG) | ⭐36,050 | [EMNLP2025] 简单快速的检索增强生成系统。 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | ⭐31,735 | 高性能向量搜索引擎与数据库，专为下一代 AI 设计。 |
| [topoteretes/cognee](https://github.com/topoteretes/cognee) | ⭐17,627 | 6 行代码即可为 AI agents 添加记忆平台。 |

---

### 3. 趋势信号分析

从今日数据可以提炼出三大趋势：

1. **AI Agent 的工程化与场景化爆发**  
   今日 Trending 中 Agent 相关项目多达 6 个（`TradingAgents`, `hermes-webui`, `oh-my-pi`, `harness`, `compound-engineering-plugin` 等），且均有数百至数千 stars 新增。多智能体协作（如交易、工程插件）成为社区焦点，开发者不再满足于单一对话式 Agent，而是追求可组合、可编排的 Agent 生态。

2. **从“使用模型”到“构建模型”的下沉**  
   `train-llm-from-scratch`（+861）和 `minimind`（今日未进 Trending 但总量极高）持续火爆，表明大量开发者正在试图掌握 LLM 训练的全流程。这与近期低成本训练工具（如 LlamaFactory）的成熟和轻量化模型（如 Tiny LLM）的涌现相辅相成。

3. **AI 记忆层与检索增强（RAG）成为基础设施刚需**  
   `supermemory` 今日突增 +647 stars，`mem0` 已超 57k stars，`LightRAG` 等学术成果快速落地。AI Agent 的长期记忆、跨会话上下文继承正从可选项变为必备能力。同时向量数据库（Milvus、Qdrant）持续迭代，RAG 正从简单的“文档检索”升级为智能知识管理。

此外，`VoxCPM` 的登榜预示着**多模态语音生成**赛道加速，`MoneyPrinterTurbo` 的火爆则印证了 AI 视频生成在内容创作领域的巨大需求。金融领域的 AI Agent（`TradingAgents`, `machine-learning-for-trading`）也开始获得社区认可，垂直行业应用正在打开。

---

### 4. 社区关注热点

- **多智能体金融交易系统**  
  `TradingAgents` 今日 +299 stars，展示了 LLM 在量化交易中的潜力。关注其如何使用多 Agent 协作进行市场分析、决策和风控，可能成为金融 AI 的标杆项目。

- **从零训练 LLM 的实操教程**  
  `train-llm-from-scratch`（+861）和 `minimind` 让每个人都可能复现基础模型。强烈建议希望深入理解 Transformer 架构的开发者跟进学习。

- **AI 记忆层的统一接口**  
  `supermemory` 与 `mem0` 正在定义 Agent 记忆的标准。如果你在开发需要跨会话知识的应用，这两个项目值得深入研究其架构与 API。

- **无分词器 TTS 语音克隆**  
  `VoxCPM` 以“True-to-Life Cloning”为卖点，今日 +888 stars。对比传统的 Tacotron、VITS 等方案，其创新在于直接对语音进行建模，可能改变语音合成行业的开发范式。

- **Agent 工程插件化生态**  
  `compound-engineering-plugin` 试图统一 Claude Code、Codex、Cursor 等工具的插件能力。这表明 Agent 开发正从单工具转向跨平台互操作，类似的“Agent 中间件”将成为下一个增长点。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*