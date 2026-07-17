# AI 开源趋势日报 2026-07-17

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-17 01:59 UTC

---

## AI 开源趋势日报 (2026-07-17)

### 📰 今日速览
- **AI Agent 技能定制工具爆发**：`Nutlope/hallmark`（抗 AI 废料设计技能）单日新增 3372 星，`mattpocock/skills`（来自 `.claude` 目录的实用技能）新增 2060 星，显示开发者对精细化、可插拔 Agent 能力的高度追求。
- **Rust 重写浪潮持续**：老牌编码代理 `openinterpreter` 迁移至 Rust，新增 661 星，并原生支持 Kimi K3 等开放模型，性能与开放性并重。
- **个性化教育 AI 成新热点**：港大团队 `DeepTutor` 获得 656 星，基于大模型实现终身个性化辅导，结合会话记忆与知识追踪。
- **知识图谱 + RAG 融合**：`Graphify-Labs/graphify` 新增 1107 星，将代码、文档、数据库等转化为可查询的知识图谱，为 AI Agent 提供结构化的上下文层。
- **GitHub 推出官方的 Copilot Agent SDK**：`github/copilot-sdk`（Java）发布，标志着 Copilot 从工具向平台组件的演进，企业级集成迎来标准化接口。

---

### 🔧 AI 基础工具（框架、SDK、推理引擎、CLI）
| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [github/copilot-sdk](https://github.com/github/copilot-sdk) | ⭐0 (+13 today) | GitHub 官方多平台 SDK，让应用和服务轻松集成 Copilot Agent 能力。 |
| [apache/ossie](https://github.com/apache/ossie) | ⭐0 (+60 today) | Apache 孵化项目，标准化 AI/BI 平台间语义元数据交换，打造厂商中立事实标准。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | ⭐86,454 | 高吞吐、低显存的大模型推理和服务引擎，支撑大规模线上部署。 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | ⭐141,934 | 最流行的 Agent 工程框架，提供 LLM 应用开发的统一抽象层。 |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | ⭐152,040 | 为 AI Agent 提供大规模网页搜索、爬取和交互的 API，让 Agent “看到”互联网。 |

### 🤖 AI 智能体 / 工作流（Agent 框架、自动化、多智能体）
| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [Nutlope/hallmark](https://github.com/Nutlope/hallmark) | ⭐0 (+3,372 today) | Anti-AI-slop 设计技能，为 Claude Code、Cursor 等工具注入高质量设计能力。 |
| [openinterpreter/openinterpreter](https://github.com/openinterpreter/openinterpreter) | ⭐0 (+661 today) | 用 Rust 重写的开放模型编码代理，支持 Kimi K3，可执行代码、管理文件系统。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | ⭐216,007 | 自增长的通用 Agent 框架，适配多种模型和工具，持续演化。 |
| [Shubhamsaboo/awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps) | ⭐122,922 (+923 today) | 100+ 可运行的 AI Agent 与 RAG 应用集合，克隆即可上手，降低开发门槛。 |
| [lobehub/lobehub](https://github.com/lobehub/lobehub) | ⭐0 (+71 today) | 首席 Agent 运营商：自动招聘、调度、汇报整个 AI 团队，实现 7×24 自动化。 |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | ⭐185,579 | 自主 AI Agent 的里程碑项目，持续推动“AI 人人可用”愿景。 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | ⭐81,027 | AI 驱动的软件开发 Agent，自主完成从需求分析到代码提交的全流程。 |

### 📦 AI 应用（具体产品、垂直场景解决方案）
| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [HKUDS/DeepTutor](https://github.com/HKUDS/DeepTutor) | ⭐0 (+656 today) | 终身个性化辅导系统，基于 LLM + 记忆实现因材施教，支持多轮交互。 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | ⭐48,668 | AI 生产力工作室：智能对话、自主 Agent、300+ 内置助手，统一接入前沿 LLM。 |
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | ⭐145,683 | 用户友好的 AI 界面，支持 Ollama、OpenAI 等多种后端，本地部署首选。 |
| [langgenius/dify](https://github.com/langgenius/dify) | ⭐149,084 | 生产级 Agent 工作流开发平台，可视化编排，快速构建 AI 应用。 |
| [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) | ⭐85,645 | 多语言 OCR 引擎，将图像/PDF 转为结构化数据，成为 LLM 的“眼睛”。 |
| [jeecgboot/JeecgBoot](https://github.com/jeecgboot/JeecgBoot) | ⭐47,104 | AI 低代码平台，通过 AI Skills 一句话生成前后端代码及报表、大屏。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*