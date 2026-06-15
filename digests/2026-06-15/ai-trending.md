# AI 开源趋势日报 2026-06-15

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-15 02:59 UTC

---

# AI 开源趋势日报（2026-06-15）

## 今日速览

- **AI 安全赛道爆发**：NVIDIA 开源的 AI Agent 安全扫描器 **SkillSpector** 获 964 个今日 stars，成为今日增幅最高的项目，反映社区对 AI 安全防护的迫切需求。
- **统一 API 成刚需**：Andrew Ng 团队推出的 **aisuite** 以 291 今日 stars 冲入 Trending，提供多模型统一接口，降低开发者在不同 LLM 提供商间切换的成本。
- **金融大模型热度持续**：国内项目 **Kronos**（金融基础模型）和 **TradingAgents**（多智能体交易框架）双双获关注，AI 在量化交易领域的应用探索加速。
- **智能体生态持续繁荣**：ECC、Hermes Agent、AutoGPT 等百万级 star 项目保持活跃，同时新晋项目如 **caveman**（极简 token 压缩）和 **claude-mem**（跨会话记忆）在细分场景上创新。

## 各维度热门项目

### 🔧 AI 基础工具（框架、推理引擎、CLI 等）

| 项目 | Stars | 说明 |
|------|-------|------|
| [ollama/ollama](https://github.com/ollama/ollama) | ⭐174,178 | 本地大模型运行工具，现已支持 Kimi、GLM、DeepSeek 等最新模型，是 AI 基础设施的标配。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | ⭐82,864 | 高吞吐 LLM 推理引擎，今日仍是生产环境部署的首选方案。 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | ⭐161,589 | 业界标准模型库，支持文本、视觉、音频等多模态模型的推理与训练。 |
| [andrewyng/aisuite](https://github.com/andrewyng/aisuite) | ⭐0 (+291 today) | 统一接口调用多种 Generative AI 提供商，简化多模型集成流程。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | ⭐98,841 | 让 AI Agent 能操作浏览器自动执行在线任务，是 Agent 落地的重要工具。 |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | ⭐132,822 | 大规模网页抓取 API，专为 AI Agent 和 RAG 场景优化。 |

### 🤖 AI 智能体 / 工作流

| 项目 | Stars | 说明 |
|------|-------|------|
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | ⭐184,942 | 自主 AI 智能体先驱，持续迭代，今日仍是最受欢迎的通用 Agent 框架之一。 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | ⭐77,081 | AI 驱动的软件开发助手，实现从需求到代码的自动化流程。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | ⭐193,620 | 可成长的智能体，支持个性化配置和技能进化，社区关注度极高。 |
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | ⭐215,566 | Agent 性能优化系统，涵盖技能、记忆、安全等模块，是 Claude Code、Cursor 等工具的增强套件。 |
| [langgenius/dify](https://github.com/langgenius/dify) | ⭐145,224 | 生产级 Agentic 工作流开发平台，可视化搭建 AI 应用。 |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | ⭐86,194 | 多智能体 LLM 金融交易框架，今日与 Kronos 共同推高金融 AI 热度。 |

### 📦 AI 应用（垂直场景、安全、金融等）

| 项目 | Stars | 说明 |
|------|-------|------|
| [NVIDIA/SkillSpector](https://github.com/NVIDIA/SkillSpector) | ⭐0 (+964 today) | **今日最热**：AI Agent 技能安全扫描器，检测恶意模式与漏洞，NVIDIA 官方出品。 |
| [shiyu-coder/Kronos](https://github.com/shiyu-coder/Kronos) | ⭐0 (+244 today) | 金融大模型基础模型，专注于金融市场语言，为量化分析提供原生 AI 能力。 |
| [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman) | ⭐72,561 | 极简 token 压缩技巧，用"原始人"语言减少 65% 的 token 消耗，适合 Claude Code 等场景。 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | ⭐47,332 | AI 生产力工作室，集成智能聊天、自主 Agent 和 300+ 助手，支持多模型。 |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | ⭐82,296 | 跨会话持久记忆层，自动捕获 Agent 行为并注入上下文，解决 Agent 无记忆痛点。 |

### 🧠 大模型 / 训练（模型权重、微调、评估）

| 项目 | Stars | 说明 |
|------|-------|------|
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | ⭐100,758 | 深度学习框架基石，今日仍是最活跃的训练基础设施。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | ⭐7,084 | LLM 评估平台，支持 100+ 数据集和主流模型，是模型选型的重要参考。 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | ⭐4,278 | 苹果芯片上学习 LLM 推理服务的教学项目，适合系统工程师入门。 |
| [Picovoice/picollm](https://github.com/Picovoice/picollm) | ⭐312 | 设备端 LLM 推理引擎，支持 X-bit 量化，适合边缘部署。 |
| [acon96/home-llm](https://github.com/acon96/home-llm) | ⭐1,358 | 与 Home Assistant 集成的本地 LLM，用于智能家居控制。 |

### 🔍 RAG / 知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 说明 |
|------|-------|------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | ⭐82,733 | 领先的开源 RAG 引擎，融合 Agent 能力，构建 LLM 的上下文层。 |
| [Shubhamsaboo/awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps) | ⭐114,560 | 100+ 可运行的 AI Agent 和 RAG 应用合集，快速上手实战。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | ⭐58,566 | AI Agent 的通用记忆层，支持长期记忆存储与检索。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | ⭐44,777 | 高性能云原生向量数据库，支撑大规模向量搜索。 |
| [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) | ⭐82,214 | OCR 工具包，可将 PDF/图片转化为结构化数据，是 RAG 数据预处理的重要组件。 |
| [StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN) | ⭐11,923 | [MLsys2026] 论文实现，在个人设备上实现 97% 存储节省的私有化 RAG 应用。 |

## 趋势信号分析

**安全与合规成为 AI 生态新焦点**：NVIDIA 推出的 SkillSpector 一日内增长近千星，表明社区开始重视 Agent 技能中的恶意代码和隐私泄露风险。这与近期多起 AI Agent 事故（如未授权的 API 调用、敏感数据泄露）密切相关，预计安全扫描工具将迅速成为 AI 开发标配。

**统一化与标准化需求爆发**：aisuite 和 ollama 的多模型支持思路获得高关注，开发者厌倦了为不同提供商编写适配代码，统一 API 正从理想走向现实。同时，browser-use 和 firecrawl 等让 AI 直接操作物理世界的工具也保持高速增长，反映“Agent + 工具使用”是当前最热的技术栈。

**金融 AI 走向实战**：Kronos 金融大模型与 TradingAgents 多智能体交易框架同时冲榜，结合此前 TauricResearch 推出的同类项目，表明 AI 在量化金融领域的应用正从论文走向可部署系统。这些项目强调多数据源整合、实时分析和低延迟推理，预计将催生一批专注金融场景的 AI 中间件。

**token 优化进入“极简主义”**：caveman 通过“原始人语言”减少 65% token 的做法虽看似玩笑，却精准切中开发者对高昂 API 成本的痛点。类似思路将推动更多 token 压缩、缓存和复用方案的出现。

## 社区关注热点

- **SkillSpector（安全扫描）**：AI Agent 安全尚处于早期，NVIDIA 官方的开源工具将成为行业标杆，建议所有 Agent 开发团队集成使用。
- **aisuite（统一 API）**：Andrew Ng 背书，项目虽今日才进入视野，但理念直接解决多模型切换痛点，可能成为下一个基础设施级项目。
- **Kronos（金融基础模型）**：针对金融市场的预训练模型较为稀缺，Kronos 若开源权重将极大降低金融 AI 的入门门槛。
- **caveman（token 压缩）**：简单粗暴但有效，适合在成本敏感或长上下文场景中实验，尤其是个人开发者和中小团队。
- **LEANN（本地 RAG）**：MLsys 2026 论文落地方案，兼顾存储高效和隐私保护，对边缘 AI 和消费级 RAG 应用有启发意义。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*