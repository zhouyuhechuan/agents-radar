# AI 开源趋势日报 2026-06-14

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-14 02:54 UTC

---

# AI 开源趋势日报（2026-06-14）

---

## 1. 今日速览

今日 GitHub Trending 上 AI 相关项目迎来爆发：**AI agent 技能与安全**成为最热主题——`addyosmani/agent-skills`（+1514 stars）、`obra/superpowers`（+924）和 `NVIDIA/SkillSpector`（+804）分别聚焦技能库、框架和安全隐患扫描；`LMCache/LMCache`（+238）作为面向 LLM 的 KV 缓存层首次登榜，标志着推理优化工具进入社区视野；`andrewyng/aisuite`（+127）提供统一的多模型接口，简化多提供商集成。与此同时，主题搜索中 `hermes-agent`（19.2万 stars）、`dify`（14.5万）、`open-webui`（14.1万）等 agent 与 RAG 项目持续领跑，生态正从“能用”向“安全、高效、可观测”演进。

---

## 2. 各维度热门项目

### 🔧 AI 基础工具

| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|------------|
| [andrewyng/aisuite](https://github.com/andrewyng/aisuite) | 0 (+127) | 统一的 Python 接口，一行代码切换多个 Generative AI 提供商，降低模型集成成本。 |
| [LMCache/LMCache](https://github.com/LMCache/LMCache) | 0 (+238) | 最快的 KV 缓存层，显著提升 LLM 推理吞吐量，是 vLLM 生态的重要补充。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 82,785 | 高吞吐、低显存的 LLM 推理引擎，当前部署 inference 的首选方案。 |
| [ollama/ollama](https://github.com/ollama/ollama) | 174,074 | 本地运行多种大模型的一站式工具，支持 Kimi、DeepSeek、Qwen 等，社区部署标配。 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | 139,216 | 语言模型应用工程平台，提供 agent、检索、链式调用等核心抽象。 |
| [kenn-io/agentsview](https://github.com/kenn-io/agentsview) | 0 (+190) | 本地优先的 coding agent 会话分析工具，支持 Claude Code、Codex 等 20+ 种 agent，可替代 cusage。 |
| [NVIDIA/SkillSpector](https://github.com/NVIDIA/SkillSpector) | 0 (+804) | AI agent 技能安全扫描器，自动检测恶意模式与漏洞，NVIDIA 官方出品。 |

### 🤖 AI 智能体/工作流

| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|------------|
| [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | 0 (+1514) | 面向 AI coding agent 的生产级技能集合，覆盖测试、部署、审查等工程环节。 |
| [obra/superpowers](https://github.com/obra/superpowers) | 0 (+924) | 一套 agentic skills 框架与方法论，配合软件开发流程使用，今日增长极快。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 192,825 | 会随着使用自成长的个人 agent，支持记忆、工具调用与多模型切换。 |
| [langgenius/dify](https://github.com/langgenius/dify) | 145,090 | 生产级 agentic workflow 开发平台，可视化编排 LLM 应用。 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | 76,911 | AI 驱动的软件开发助手，能自动写代码、调试、部署，类似“开源 Devin”。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 98,700 | 让 AI agent 能像人一样操作浏览器，自动化网页任务。 |
| [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit) | 35,017 | 为 agent 与生成式 UI 提供前端框架，支持 React、Angular、移动端等。 |

### 📦 AI 应用

| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|------------|
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 47,286 | 集成智能聊天、自主 agent 和 300+ 助手的 AI 生产力工具，统一访问前沿大模型。 |
| [OpenBB-finance/OpenBB](https://github.com/OpenBB-finance/OpenBB) | 69,070 | 为分析师、量化研究员和 AI agent 提供开源金融数据平台。 |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | 85,858 | 基于多 agent 的金融交易框架，结合 LLM 做出交易决策。 |
| [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) | 82,117 | 基于 OCR 的文档结构化工具，支持 100+ 语言，是 LLM 处理非结构化数据的前置利器。 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | 27,247 | 从任意文档自动生成可编辑的 PowerPoint，支持原生形状与动画，含语音旁白。 |
| [santifer/career-ops](https://github.com/santifer/career-ops) | 53,542 | AI 驱动的求职系统，基于 Claude Code，包含 14 种技能模式与看板。 |

### 🧠 大模型/训练

| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|------------|
| [huggingface/transformers](https://github.com/huggingface/transformers) | 161,569 | 最主流的模型定义框架，支持文本、视觉、音频、多模态模型，训练与推理皆可。 |
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | 100,733 | 动态神经网络框架，AI 研究与生产的事实标准。 |
| [ultralytics/ultralytics](https://github.com/ultralytics/ultralytics) | 58,357 | YOLO 系列目标检测框架，支持训练与部署，社区广泛使用。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,082 | 大规模 LLM 评估平台，支持 Llama3、GPT-4、Claude 等 100+ 数据集。 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | 4,274 | 面向系统工程师的 LLM 推理课程，动手构建微型 vLLM + Qwen，实践性强。 |

### 🔍 RAG/知识库

| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|------------|
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | 141,401 | 用户友好的 AI 界面，支持 Ollama 和 OpenAI API，内置 RAG 与知识库管理。 |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 82,659 | 领先的开源 RAG 引擎，融合 agent 能力，构建高质量上下文层。 |
| [run-llama/llama_index](https://github.com/run-llama/llama_index) | 50,112 | 领先的文档 agent 与 OCR 平台，擅长结构化非结构化数据。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 44,764 | 云原生高性能向量数据库，支持 ANN 搜索，RAG 基础设施首选。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 58,494 | AI agent 的通用记忆层，实现跨会话持久化上下文。 |
| [FlowiseAI/Flowise](https://github.com/FlowiseAI/Flowise) | 53,549 | 可视化构建 AI agent 和 RAG 流程，低代码友好。 |

---

## 3. 趋势信号分析

**AI agent 技能化与安全化**是今日最强烈的信号。`agent-skills` 和 `superpowers` 同时登顶 Trending，前者提供即用型生产级技能，后者定义了一种方法论，两者加起来日增超 2400 stars，表明社区不再满足于“能跑”，而是追求**专业、可复用、可审计**的 agent 工程实践。`NVIDIA/SkillSpector` 的爆火（+804）则直接呼应了 agent 安全风险——当 agent 可以自主执行命令，技能仓库可能成为攻击面。**推理优化工具首次登榜**：`LMCache` 作为 KV 缓存层，区别于传统的量化或剪枝，从内存管理角度提升吞吐，这对长上下文场景和实时应用极为关键。`andrewyng/aisuite` 虽增速不算极高，但来自知名 AI 学者 Andrew Ng 的项目，代表“统一接口”模式正被主流接受，与 LangChain 形成竞争/互补。

纵观主题搜索，`hermes-agent`（19 万 stars）与 `dify`（14 万）等老牌项目仍保持统治力，但 `TradingAgents`、`browser-use` 等垂直 Agent 应用增长迅猛，显示 **AI agent 正从通用聊天向金融、自动化测试、求职等具体场景渗透**。RAG 领域 `open-webui` 与 `anything-llm` 的本地优先策略持续吸引开发者，与 Ollama 形成“部署闭环”。

---

## 4. 社区关注热点

- 🔥 **addyosmani/agent-skills** — 背靠 Google Chrome 团队，提供编码、测试、CI/CD 等技能，是 AI agent 开发的“瑞士军刀”，今日增长最猛。
- 🔥 **NVIDIA/SkillSpector** — 首个针对 agent 技能的安全扫描器，NVIDIA 官方出品，标志 agent 安全成为新赛道。
- 🔥 **LMCache/LMCache** — 优化 LLM 推理的新范式，与 vLLM 配合后可大幅降低成本，适合高并发/长上下文场景。
- 🔥 **open-webui + ollama** — 本地部署 AI 的黄金组合，社区关注度持续高涨，适合隐私敏感和个人开发者。
- 🔥 **hermes-agent** — 19 万 stars 的“自成长 agent”，代表下一代通用 agent 方向，值得跟踪其技能生态演进。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*