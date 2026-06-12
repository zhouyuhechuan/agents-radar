# AI 开源趋势日报 2026-06-12

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-12 02:50 UTC

---

# AI 开源趋势日报（2026-06-12）

## 今日速览

- **AI Agent 技能生态爆发**：`addyosani/agent-skills` 单日飙升 3278 stars，`phuryn/pm-skills`、`obra/superpowers`、`msitarzewski/agency-agents` 等技能市场类项目集体登榜，表明社区正从“构建 Agent”转向“复用和交易技能”。
- **安全与合规成为 Agent 标配**：NVIDIA 推出 `SkillSpector` 安全扫描器，针对 AI Agent 技能中的漏洞和恶意模式，标志着 Agent 生态开始引入专业安全工具。
- **医疗垂直 AI 再获关注**：`maziyarpanahi/openmed` 开源医疗 AI 项目单日 +426 stars，结合近期医疗大模型发布潮，AI+医疗仍是热门落地场景。
- **RAG 与记忆层持续迭代**：`graphify`（知识图谱查询）、`claude-context`（代码搜索 MCP）、`claude-mem`（会话记忆压缩）等新项目快速积累数万 stars，RAG 正向结构化、持久化、跨会话方向发展。
- **系统提示与 Agent 逆向工程升温**：`x1xhlol/system-prompts‑and‑models‑of‑ai‑tools` 收集了 30+ 款 AI 工具的内部系统提示，反映出开发者对 Agent 内部机制的深度探索需求。

---

## 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、CLI）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [langgenius/dify](https://github.com/langgenius/dify) | ⭐144,896 | 生产级 Agent 工作流开发平台，支持拖拽构建、RAG、工具调用 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | ⭐82,606 | 高吞吐 LLM 推理引擎，内存效率优秀，支撑大规模部署 |
| [ollama/ollama](https://github.com/ollama/ollama) | ⭐173,908 | 一键运行本地大模型（Kimi、DeepSeek、Qwen 等），开发者首选推理入口 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | ⭐161,514 | 🤗 模型定义与微调框架，支持文本、视觉、音频、多模态 |
| [langchain4j/langchain4j](https://github.com/langchain4j/langchain4j) | ⭐12,295 | Java 生态的 LangChain 实现，集成 Spring Boot / Quarkus，企业级 LLM 开发利器 |
| [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) | ⭐7,590 | Rust 编写的高性能 LLM 应用框架，模块化、类型安全 |
| [Picovoice/picollm](https://github.com/Picovoice/picollm) | ⭐312 | 设备端 LLM 推理库，量子化压缩后可在边缘设备运行 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | ⭐4,270 | 面向系统工程师的 LLM 推理服务学习课程，动手实现微型 vLLM |

### 🤖 AI 智能体 / 工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | ⭐184,889 | 开创性自主 Agent 项目，持续引领多智能体协作与任务规划 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | ⭐76,509 | AI 驱动软件开发助手，自动完成编码、测试、部署全流程 |
| [bytedance/deer-flow](https://github.com/bytedance/deer-flow) | ⭐71,005 | 字节开源的长周期 SuperAgent 框架，集成沙箱、记忆、子 Agent 和技能仓库 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | ⭐98,354 | 让 AI Agent 像人类一样操控浏览器，自动化在线任务 |
| [addyosani/agent-skills](https://github.com/addyosani/agent-skills) | ⭐0 (+3278 today) | 生产级 AI 编码 Agent 技能集，今日热度**最高**，适合强化 Agent 工程能力 |
| [phuryn/pm-skills](https://github.com/phuryn/pm-skills) | ⭐0 (+1978 today) | 产品经理专用 Agent 技能市场：100+ 从策略到增长的插件 |
| [obra/superpowers](https://github.com/obra/superpowers) | ⭐0 (+1322 today) | 一套可复用的 Agent 技能框架+软件方法论，旨在解决 Agent 开发效率 |
| [msitarzewski/agency-agents](https://github.com/msitarzewski/agency-agents) | ⭐0 (+1599 today) | 一站式 AI 代理机构，包含前端、社区运营、内容注入等各类专门 Agent |
| [NVIDIA/SkillSpector](https://github.com/NVIDIA/SkillSpector) | ⭐0 (+319 today) | NVIDIA 出品，专门扫描 AI Agent 技能的安全漏洞和恶意模式 |
| [hexo-ai/sia](https://github.com/hexo-ai/sia) | ⭐0 (+199 today) | 自我改进 AI 框架：自动优化 Agent / 模型在基准任务上的表现 |

### 📦 AI 应用（具体产品、垂直场景解决方案）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | ⭐141,138 | 最流行的本地 AI 聊天界面，支持 Ollama、OpenAI 等，功能丰富 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | ⭐47,225 | AI 生产力工作室：智能对话、自主 Agent、300+ 助手，统一访问前沿 LLM |
| [maziyarpanahi/openmed](https://github.com/maziyarpanahi/openmed) | ⭐0 (+426 today) | 开源医疗 AI，覆盖诊断、问答、文档处理，垂直场景标杆 |
| [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) | ⭐42,201 | LLM 驱动的股票分析系统，集成行情、新闻、LLM 决策仪表盘 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | ⭐26,703 | 从文档自动生成可编辑 PowerPoint，包含原生动画、讲稿、语音 |
| [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) | ⭐26,405 | 让 Agent“看”遍全网：一键搜索 Twitter、Reddit、YouTube、GitHub 等，零 API 费用 |
| [ScrapeGraphAI/Scrapegraph-ai](https://github.com/ScrapeGraphAI/Scrapegraph-ai) | ⭐27,100 | 基于 LLM 的智能爬虫，将自然语言查询转化为结构化数据 |
| [iOfficeAI/AionUi](https://github.com/iOfficeAI/AionUi) | ⭐28,087 | 免费的本地开源 24/7 协同工作台，支持 Claude Code、Hermes Agent 等 20+ CLI Agent |

### 🧠 大模型 / 训练（模型权重、训练框架、微调工具）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) | ⭐72,092 | 统一高效微调框架，支持 100+ LLM/VLM，ACL 2024 论文 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | ⭐7,081 | 开源 LLM 评估平台，覆盖 Llama3、GPT-4、Qwen 等 100+ 数据集 |
| [zchoi/Awesome-Embodied-Robotics-and-Agent](https://github.com/zchoi/Awesome-Embodied-Robotics-and-Agent) | ⭐1,813 | 具身智能与机器人+LLM 的精选研究列表，前沿方向 |
| [acon96/home-llm](https://github.com/acon96/home-llm) | ⭐1,357 | Home Assistant 集成+本地 LLM 模型，用自然语言控制智能家居 |
| [RyanLiu112/Awesome-Process-Reward-Models](https://github.com/RyanLiu112/Awesome-Process-Reward-Models) | ⭐167 | 过程奖励模型精选合集，强化学习训练的最新方法 |
| [llm-jp/awesome-japanese-llm](https://github.com/llm-jp/awesome-japanese-llm) | ⭐1,409 | 日语 LLM 大全，持续追踪日语语言模型的进展 |
| [testtimescaling/testtimescaling.github.io](https://github.com/testtimescaling/testtimescaling.github.io) | ⭐105 | 大模型测试时扩展（Test‑Time Scaling）综述资源页 |

### 🔍 RAG / 知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | ⭐82,493 | 开源 RAG 引擎标杆，融合 Agent 能力，为 LLM 提供高质量上下文层 |
| [Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm) | ⭐61,462 | 本地优先的 Agent 体验：文档存储、向量化、多模型对话 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | ⭐58,370 | AI Agent 的通用记忆层，跨会话持久化知识 |
| [run-llama/llama_index](https://github.com/run-llama/llama_index) | ⭐50,088 | 领先的文档 Agent 和 OCR 平台，连接数据与 LLM |
| [safishamsi/graphify](https://github.com/safishamsi/graphify) | ⭐65,722 | 将任何代码、文档、图片转为可查询的知识图谱，赋能 Agent 深度理解 |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | ⭐81,856 | 跨会话 Agent 上下文压缩与注入，支持 Claude Code、Codex 等，突破上下文限制 |
| [zilliztech/claude-context](https://github.com/zilliztech/claude-context) | ⭐11,820 | 代码搜索 MCP 工具，让 Agent 拥有整个代码库作为上下文 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | ⭐44,732 | 云原生高性能向量数据库，ANN 搜索基准领先 |
| [NirDiamant/RAG_Techniques](https://github.com/NirDiamant/RAG_Techniques) | ⭐27,873 | RAG 系统进阶技术教程库，每项技术附带完整 Notebook 示例 |

---

## 趋势信号分析

**社区爆发性关注点：Agent 技能市场与安全化。** 今日 Trending 榜单中，`addyosani/agent-skills`、`phuryn/pm-skills`、`obra/superpowers`、`msitarzewski/agency-agents` 四个技能相关项目合计获得超过 8000 个今日新增 stars。这表明社区已从“如何写一个 Agent”转向“如何获取、复用和安全管理 Agent 技能”。NVIDIA 的 `SkillSpector` 作为首个专业 Agent 安全扫描工具出现，暗示技能供应链安全将成为下一阶段焦点。

**新兴方向首次登榜：** `kenn-io/agentsview` 主打本地优先的 Coding Agent 会话分析，是继 `ccusage` 后更高效的开源替代，反映 Agent 可观测性需求正在形成独立赛道。同时，`hexo-ai/sia` 提出**自我改进 AI 框架**，让 Agent 自动在基准任务上提升性能，这一方向未来可能融入 AutoGPT 等主流框架。

**与行业事件的关联：** 近期多个医疗大模型发布（如 Med‑Palm、开源医疗模型）推动了 `maziyarpanahi/openmed` 的增长。`x1xhlol/system-prompts‑and‑models‑of‑ai‑tools` 的火爆则与“Agent 内部机制透明化”的运动有关——开发者希望剥离产品外壳，直接研究底层系统提示与模型配置。

---

## 社区关注热点

- **🛠 学习与构建 Agent 技能：** 推荐关注 `addyosani/agent-skills`（生产级编码技能）和 `shareAI-lab/learn-claude-code`（从零构建类似 Claude Code 的 Agent 工具），适合希望深入 Agent 开发的工程师。
- **🔒 Agent 安全与审计：** `NVIDIA/SkillSpector` 是今天唯一的专业安全工具，未来可能被集成到 CI/CD 流程中。如果你的项目使用了第三方 Agent 技能，建议立即试用。
- **🧠 持久记忆与知识图谱：** `mem0`、`graphify`、`claude-context` 正推动 Agent 从“对话式”向“拥有长期记忆和结构知识”演进。`thedotmack/claude-mem` 的 8 万 stars 表明跨会话上下文是刚需。
- **🚀 垂直场景 agent 应用：** `ppt-master`（自动化 PPT）、`daily_stock_analysis`（金融分析）、`openmed`（医疗）展示 Agent 在具体行业中的落地潜力，适合寻找创业或二次开发方向的开发者。
- **📦 本地化与隐私优先：** `ollama`、`anything-llm`、`CherryHQ/cherry-studio` 的持续流行，叠加 `picollm`（设备端推理）的出现，说明社区对“不依赖云端、数据自主掌控”的需求依然强劲。

---

*数据来源：GitHub Trending (2026-06-12) & GitHub Search API（7天内活跃 AI 项目，主题标签分类）*

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*