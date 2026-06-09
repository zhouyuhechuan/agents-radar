# AI 开源趋势日报 2026-06-09

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-09 02:30 UTC

---

# AI 开源趋势日报（2026-06-09）

## 今日速览
- **Agent 基础设施全面爆发**：超过半数 Trending 项目围绕 Agent 技能（Skills）和 Agent 运行时（Harness）展开，`mvanhorn/last30days-skill` 单日增长 3558 stars，Agent 生态从框架向“可组装能力”快速演进。
- **本地 LLM 优化与评测工具受捧**：`whichllm`（+143 stars）和 `turbovec`（+1729 stars）分别从“模型适配”和“向量索引效率”两个维度降低本地部署门槛，社区对“我的硬件能跑什么模型”的关注度持续升温。
- **计算机视觉工具 `supervision` 单日暴增 1288 stars**，表明 AI 视觉应用（结合 Agent 的实时视觉能力）正在成为新的增长点。
- **RAG 与记忆系统竞争白热化**：`MemPalace`（+170 stars）宣称“最佳开源 AI 记忆系统”，`Claude-mem`（81k stars）主打跨会话持久上下文，RAG 不再是简单检索，而是转向“智能记忆层”。
- **微软、Google 等巨头加速 Agent 平台开放**：`google/skills` 发布 Google 产品 Agent 技能集，微软的 `synthetic-rag-index` 也在主题搜索中亮相，大厂正将自家生态与 Agent 技能市场深度绑定。

---

## 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [ollama/ollama](https://github.com/ollama/ollama) | ⭐173,630 | 本地运行 LLM 的最简方案，已支持 Kimi-K2.6、GLM-5.1 等最新模型，成为本地推理标配。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | ⭐82,260 | 高吞吐、内存高效的 LLM 推理引擎，企业级部署首选，持续优化 PagedAttention。 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | ⭐161,421 | 模型定义与训练框架，支持数千种预训练模型，社区生态核心。 |
| [turbovec](https://github.com/RyanCodrai/turbovec)（Trending） | ⭐0（+1729 today） | 基于 Rust 的 TurboQuant 向量索引，Python 绑定，性能对标 FAISS，专为本地高效检索设计。 |
| [whichllm](https://github.com/Andyyyy64/whichllm)（Trending） | ⭐0（+143 today） | 一行命令找出本地硬件上运行最快、效果最佳的 LLM，用实时评测代替参数堆砌。 |
| [langchain4j](https://github.com/langchain4j/langchain4j) | ⭐12,250 | Java 生态的 LLM 应用框架，统一 API 对接多模型/向量库，与 Spring Boot 深度集成。 |

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | ⭐184,849 | 最早的开源自主 Agent 项目，近期聚焦“技能市场”与多模型编排。 |
| [OpenHands](https://github.com/OpenHands/OpenHands) | ⭐76,273 | AI 驱动的软件开发 Agent，支持代码生成、调试、部署全流程闭环。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | ⭐97,805 | 让 AI Agent 像人一样操作浏览器，实现网页自动化任务。 |
| [aaif-goose/goose](https://github.com/aaif-goose/goose)（Trending） | ⭐0（+699 today） | 开源、可扩展的 AI Agent，超越代码补全，可安装、执行、测试任何 LLM。 |
| [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit)（Trending） | ⭐0（+378 today） | 前端 Agent 栈，React/Angular/移动端均可嵌入 Agent 与生成式 UI，定义 AG-UI 协议。 |
| [santifer/career-ops](https://github.com/santifer/career-ops)（Trending） | ⭐0（+308 today） | AI 求职系统，14 种技能模式 + Go 仪表盘 + PDF 生成，基于 Claude Code 构建。 |
| [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)（Trending） | ⭐0（+3558 today） | 跨平台信息研究 Agent（Reddit/X/YouTube/HN/Polymarket），输出结构化摘要。单日增速冠军。 |

### 📦 AI 应用（具体应用产品、垂直场景解决方案）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | ⭐47,083 | AI 生产力工作室，集成智能聊天、自主 Agent、300+ 助手，统一访问前沿 LLM。 |
| [roboflow/supervision](https://github.com/roboflow/supervision)（Trending） | ⭐0（+1288 today） | 可复用的计算机视觉工具库，让开发者轻松构建目标检测、分割、追踪等视觉应用。 |
| [ppt-master](https://github.com/hugohe3/ppt-master) | ⭐25,312 | 从文档一键生成可编辑 PPT，带原生形状、动画、语音旁白，支持自定义模板。 |
| [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) | ⭐41,402 | LLM 驱动的多市场股票分析系统，零成本定时运行，消息推送。 |
| [shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) | ⭐65,487 | 从零构建类 Claude Code 的 Agent harness，Bash 超轻量实现，教学价值极高。 |

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) | ⭐72,005 | 统一高效微调 100+ LLM/VLM 的工具，ACL 2024，社区事实标准。 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | ⭐4,258 | 面向系统工程师的 LLM 推理服务学习项目，在 Apple Silicon 上构建迷你 vLLM+Qwen。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | ⭐7,068 | 全面的大模型评测平台，支持 100+ 数据集与多种模型。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | ⭐187,522 | 自进化 Agent，强调与用户共同成长，同时包含模型训练与 Agent 能力。 |

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [langgenius/dify](https://github.com/langgenius/dify) | ⭐144,452 | 生产级 Agent RAG 平台，可视化工作流，支持多种 LLM 与向量库。 |
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | ⭐140,702 | 最火的本地 AI 界面，对接 Ollama/OpenAI，支持 RAG、多模态。 |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | ⭐82,232 | 领先的 RAG 引擎，融合 Agent 能力与上下文层，API 友善。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | ⭐58,084 | AI Agent 的通用记忆层，跨会话持久化上下文记忆。 |
| [MemPalace/mempalace](https://github.com/MemPalace/mempalace)（Trending） | ⭐0（+170 today） | 号称“最佳开源 AI 记忆系统”，通过基准评测证明性能，免费使用。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | ⭐44,686 | 云原生高性能向量数据库，大规模 ANN 搜索首选。 |
| [weaviate/weaviate](https://github.com/weaviate/weaviate) | ⭐16,297 | 开源向量数据库，支持对象与向量混合搜索，故障容错。 |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | ⭐81,316 | 跨会话持久上下文：捕获 Agent 操作→压缩→注入未来会话，支持 Claude Code 等。 |

> 注：以上列表为每个维度的代表性项目，完整分类数据在原始库中可查。

---

## 趋势信号分析

今日 Trending 榜单揭示了三个关键信号：

1. **Agent 技能（Skill）市场成为新风口**：`mvanhorn/last30days-skill`（+3558）、`phuryn/pm-skills`、`google/skills` 等项目表明，社区不再满足于单个 Agent 框架，而是追求可插拔、可复用的“技能包”。这与近期 Anthropic 发布的 Claude Code skill 协议、OpenAI 的插件系统形成呼应，未来 Agent 生态将围绕“技能市场”展开竞争。

2. **本地优先 + 多模态评估工具崛起**：`whichllm` 和 `turbovec` 的快速增长说明，随着开源模型（Kimi、GLM、DeepSeek等）密集发布，开发者迫切需要工具来自动评估“我的硬件能跑多快”，以及“如何用本地向量搜索替代云端方案”。这标志着 AI 部署正从“云优先”转向“本地 + 云端混合”。

3. **计算机视觉与 Agent 结合加速**：`roboflow/supervision` 一天获 1288 stars，同时 `Agent-Reach` 强调“给 AI agent 眼睛看互联网”，暗示 Agent 不再只是文本交互，视觉理解能力正在从研究走向应用（如自动抓取社交媒体图像、实时视频分析）。这与 OpenAI 最新发布的 GPT-Vision 和 Google 的 Gemini 多模态能力紧密相关。

---

## 社区关注热点

- **🆕 单日冠军 `last30days-skill`**：一个 Agent 技能就能在一天内积累 3558 stars，说明“信息研究”类 Agent 需求旺盛，尤其关注跨平台舆情综合。建议开发者关注其数据合成思路，可复用到金融、竞品分析等垂直场景。

- **🆕 `goose`（aaif-goose）**：开源、可扩展的 Agent 运行时，超越代码补全，强调“安装、执行、编辑、测试”全链路。其 Rust 实现性能优异，值得对比同类的 `OpenHands` 和 `AutoGPT`，探索轻量级 Agent 架构。

- **🔥 记忆层之争**：`MemPalace`（+170 stars）与 `Claude-mem`（81k stars）正面竞争，前者强调纯开源与基准测试，后者已被大量 Claude Code 用户采用。AI Agent 的持久化记忆是当前最大瓶颈之一，相关工具（如 `mem0ai`）将持续受到社区审视。

- **🏆 视觉工具 `supervision`**：由 Roboflow 维护，支持 YOLO、SAM 等现代视觉模型的一行集成。其今日爆发表明，CV 社区正寻求一种“零样板代码”的视觉能力接入方式，与 Agent 结合后潜力巨大。

- **📦 `career-ops` 与 `ppt-master`**：垂直应用类项目正在用 Agent 重构传统工作流（求职、PPT制作），证明了 AI Agent + 具体场景的直接商业价值，开发者可参考其“技能模式 + 文档生成”的落地思路。

---

> **数据说明**：Trending 数据来自 2026-06-09 GitHub Trending 榜单（今日新增 stars 标注为 "+N today"），主题搜索数据来自 GitHub Search API（标注总量 stars）。所有项目均经过 AI/ML 相关性筛选，排除非 AI 项目（如通用教材库 `ChinaTextbook`、纯文档工具 `tolaria` 等）。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*