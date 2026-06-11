# AI 开源趋势日报 2026-06-11

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-11 02:53 UTC

---

## 《AI 开源生态日报》2026-06-11

### 一、今日速览

今日 GitHub 突显两个核心趋势：**Agent 技能标准化** 与 **检索增强（RAG）生态成熟化**。Trending 榜单中，多个以“skills”命名的项目（如 `agent-skills`、`pm-skills`、`google/skills`）集中爆发，标志着业界正从泛化 Agent 框架转向可复用的模块化技能库。与此同时，主题搜索中 RAG/向量数据库项目仍稳居流量高地（`milvus`、`qdrant`、`ragflow` 等持续霸榜），而面向个人开发者的轻量级训练工具（`train-llm-from-scratch`）及垂直领域 AI 应用（`MoneyPrinterTurbo`、`openmed`）亦表现出强劲社区关注度。

---

### 二、各维度热门项目

#### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | ⭐82,469 | 高性能 LLM 推理引擎，今日因支持更多量化技术而受关注。 |
| [ollama/ollama](https://github.com/ollama/ollama) | ⭐173,805 | 极简本地 LLM 运行工具，已集成超过 20 种主流开源模型。 |
| [samchon/nestia](https://github.com/samchon/nestia) | ⭐2,159 | 为 NestJS 框架提供 AI 聊天机器人开发能力的 SDK，TypeScript 生态新宠。 |
| [google/skills](https://github.com/google/skills) | ⭐ 0 (+211 today) | 官方出品：Google 产品与技术的 Agent 技能集，重塑开发者与 Google API 的交互方式。 |

#### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | ⭐184,887 | 经典自主 Agent 框架，近期引入多模态感知能力。 |
| [bytedance/deer-flow](https://github.com/bytedance/deer-flow) | ⭐70,917 | 字节开源的长周期 SuperAgent 编排系统，支持沙盒、记忆与子代理协作。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | ⭐190,081 | 成长型 Agent 框架，通过自我反思与环境交互持续进化。 |
| [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | ⭐ 0 (+821 today) | 生产级 AI 编码技能集，为 Claude Code、Codex 等提供标准化技能组件，今日新增最活跃。 |
| [phuryn/pm-skills](https://github.com/phuryn/pm-skills) | ⭐ 0 (+804 today) | 项目管理技能市场：100+ 预构建 Agent 技能，覆盖策略、执行、增长全流程。 |
| [obra/superpowers](https://github.com/obra/superpowers) | ⭐ 0 (+1,104 today) | 一套完整的 Agent 技能框架及软件开发方法，今日 Trend 排名靠前。 |
| [activeloopai/hivemind](https://github.com/activeloopai/hivemind) | ⭐ 0 (+64 today) | 统一多 Agent 脑：让不同 Agent 共享记忆与知识，实现协同工作。 |

#### 📦 AI 应用（具体产品、垂直场景解决方案）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | ⭐ 0 (+1,389 today) | 利用 AI 大模型一键生成高清短视频，面向内容创作者，今日新增暴涨。 |
| [maziyarpanahi/openmed](https://github.com/maziyarpanahi/openmed) | ⭐ 0 (+527 today) | 开源医疗 AI 工具包，集成诊断、影像分析与病历生成。 |
| [ruvnet/RuView](https://github.com/ruvnet/RuView) | ⭐ 0 (+420 today) | 基于 WiFi 信号的空间感知与生命体征监测——无需摄像头，实现非接触式 AI 感知。 |
| [roboflow/supervision](https://github.com/roboflow/supervision) | ⭐ 0 (+695 today) | 计算机视觉开源工具库，简化 YOLO、SAM 等模型的集成部署。 |
| [Picovoice/picollm](https://github.com/Picovoice/picollm) | ⭐312 | 超轻量设备端 LLM 推理库，支持 X-Bit 量化，适合嵌入式场景。 |

#### 🧠 大模型/训练（模型权重、训练框架、微调工具）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) | ⭐72,056 | 统一高效微调 100+ LLM/VLM 的框架（ACL 2024），社区标准工具。 |
| [FareedKhan-dev/train-llm-from-scratch](https://github.com/FareedKhan-dev/train-llm-from-scratch) | ⭐ 0 (+247 today) | 手把手教程：从数据下载到生成文本，带你从零训练 LLM。 |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | ⭐254 | 稳定、可扩展的预训练库，专为基础模型与 World Model 设计。 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | ⭐4,267 | 学习 LLM 推理服务的课程项目：基于 Apple Silicon 构建迷你 vLLM + Qwen。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | ⭐7,080 | LLM 评测平台，支持 100+ 数据集与主流模型，今日新增对多模态模型的评价。 |

#### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | ⭐44,724 | 云原生高绩效向量数据库，支撑大规模 ANN 搜索。 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | ⭐32,015 | Rust 编写的高性能向量数据库，支持云端与本地部署。 |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | ⭐82,421 | 领先的开源 RAG 引擎，融合 Agent 能力提供 LLM 上下文层。 |
| [Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm) | ⭐61,407 | 本地优先的 RAG 应用，将任何文档变为 LLM 可查询的知识库。 |
| [StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN) | ⭐11,903 | [MLsys2026] 97% 存储节省的 RAG 方案，可在个人设备上运行。 |
| [safishamsi/graphify](https://github.com/safishamsi/graphify) | ⭐65,031 | 将代码、文档等转化为知识图谱的 Agent 技能，支持 Claude Code 等工具。 |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | ⭐81,662 | 为 Claude Code 提供跨会话持久记忆，压缩历史并注入上下文。 |

---

### 三、趋势信号分析

**1. “技能化” Agent 生态爆发**  
今日 Trending 前 5 名中，`agent-skills`、`pm-skills`、`superpowers`、`last30days-skill` 均属于 Agent 技能库或技能市场。这反映社区正从单一 Agent 框架（如 AutoGPT）转向**标准化、可复用、可组合的技能组件**。`google/skills` 的入场更证实大型科技公司正在将内部能力封装为通用技能接口，类似 MCP 协议的进一步落地。

**2. 轻量级训练工具与教育化内容升温**  
`train-llm-from-scratch` 今日新增 247 stars，`tiny-llm` 保持 4k+ stars，说明**个人开发者对理解和实践 LLM 训练的需求**持续增加。结合 `LlamaFactory` 等微调工具的成熟，AI 训练已从大型团队下沉至个人实验场景。

**3. 计算机视觉与多模态感知融合**  
`roboflow/supervision` 今日新增 695 stars，`RuView`（WiFi 感知）也登上热榜，表明**非视觉传感器的 AI 感知**（如 WiFi、雷达）开始获得关注，与传统的视觉 CV 工具形成互补。

**4. RAG 基础设施继续巩固**  
`milvus`、`qdrant`、`ragflow` 等长期位于搜索量前列，而 `LEANN`、`graphify` 等新项目强调**存储优化与知识图谱集成**，表明 RAG 正从简单检索向多模态、结构化知识管理演进。

---

### 四、社区关注热点

- **🔍 Agent 技能市场（Skill Marketplace）**  
  如 `agent-skills`、`pm-skills`、`google/skills`——社区正在定义 Agent 能力的“App Store”模式，开发者可发布、发现和组合技能，降低 AI 编码代理的构建门槛。

- **🎥 AI 短视频生成工具**  
  `MoneyPrinterTurbo` 今日新增近 1400 stars，结合大模型的视频生成能力被寄予厚望，尤其适合内容创作者和营销场景。

- **🧠 跨会话记忆系统**  
  `claude-mem`、`mem0`、`cognee` 等项目持续活跃，**Agent 记忆** 成为 RAG 之外另一个技术热点，直接影响 AI 的长期协同能力。

- **📚 从零训练 LLM 的教育资源**  
  `train-llm-from-scratch`、`tiny-llm` 等教程类项目增长迅猛，说明开发者希望深入了解模型内部机理，而不仅仅是使用 API。

- **🌐 非视觉 AI 感知**  
  `RuView`（WiFi 信号感知）与 `roboflow/supervision`（传统 CV）形成对比，提示**低成本、隐私友好的环境感知方案**可能成为 IoT 与边缘 AI 的新突破口。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*