# AI 开源趋势日报 2026-06-13

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-13 02:42 UTC

---

# AI 开源趋势日报 | 2026-06-13

## 一、今日速览

今日 GitHub Trending 榜单中 **AI Agent 技能类项目（agent-skills、superpowers、pm-skills、agency-agents）** 集体爆发，单日新增 stars 均在 800 以上，反映出社区对可复用、生产级的 Agent 技能市场与框架高度热情。同时，LLM 推理优化工具 **LMCache** 稳定增长，医疗 AI 应用 **openmed** 首次进入热榜，显示垂直领域落地加速。主题搜索中，RAG 与向量数据库生态持续活跃，**Milvus、Qdrant、Weaviate** 等保持高热度，而 **mem0**（通用记忆层）与 **CopilotKit**（前端 Agent UI 栈）成为社区新宠。

---

## 二、各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [ollama/ollama](https://github.com/ollama/ollama) | 173,981 | 本地运行 LLM 的最便捷方式，支持 Kimi、GLM、DeepSeek 等多种模型。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 82,725 | 高吞吐、低内存的 LLM 推理与服务引擎，生产部署标配。 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | 161,547 | 业界标杆的模型定义框架，支持文本、视觉、多模态任务的推理与训练。 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | 139,148 | Agent 工程平台，提供统一的 LLM 调用、工具集成与记忆管理。 |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | 132,013 | 面向 AI 的网页抓取与搜索 API，支持大规模数据采集。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 98,524 | 让 AI Agent 自动操控浏览器，在线任务自动化利器。 |
| [LMCache/LMCache](https://github.com/LMCache/LMCache) | 0（今日+28） | 为 LLM 提供极速 KV 缓存层，显著降低推理延迟。 |

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|-----------|
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 184,915 | 通用 AI Agent 平台，让每个人都可构建自主任务系统。 |
| [langgenius/dify](https://github.com/langgenius/dify) | 145,004 | 生产级 Agent 工作流开发平台，支持可视化编排与多模型。 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | 76,671 | AI 驱动的软件开发助手，自主完成编码、调试、部署。 |
| [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | 0（+2656） | 面向 AI 编程代理的生产级工程技能集合，今日热榜第一。 |
| [obra/superpowers](https://github.com/obra/superpowers) | 0（+1275） | 一套 Agent 技能框架与软件开发方法论，强调“可工作”。 |
| [msitarzewski/agency-agents](https://github.com/msitarzewski/agency-agents) | 0（+1026） | 完整 AI 代理机构，包含前端、Reddit、创意注入等专业 Agent。 |
| [phuryn/pm-skills](https://github.com/phuryn/pm-skills) | 0（+827） | 100+ 项目管理 Agent 技能市场，覆盖发现、执行、增长全流程。 |

### 📦 AI 应用（具体应用产品、垂直场景解决方案）

| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|-----------|
| [maziyarpanahi/openmed](https://github.com/maziyarpanahi/openmed) | 0（+515） | 开源医疗 AI 系统，今日首次登榜，推动医疗领域 AI 落地。 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 47,251 | 全能 AI 生产力工作室，集成智能聊天、自主 Agent 与 300+ 助手。 |
| [zhayujie/CowAgent](https://github.com/zhayujie/CowAgent) | 45,261 | 开源超级 AI 助手与 Agent 引擎，支持多模型、多通道、记忆进化。 |
| [santifer/career-ops](https://github.com/santifer/career-ops) | 53,252 | AI 驱动的求职系统，集成 14 种技能模式与简历生成。 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | 27,017 | 从文档一键生成可编辑 PPT，含动画、演讲备注与语音旁白。 |
| [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) | 42,333 | LLM 驱动的 A/H/美 股智能分析系统，支持多数据源与仪表盘。 |

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) | 72,121 | 统一高效微调 100+ LLM/VLM 的框架（ACL 2024）。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,081 | 大规模 LLM 评测平台，支持 100+ 数据集与多种模型。 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | 4,272 | 系统工程师学习 LLM 推理服务的入门课程：从零构建 mini vLLM。 |
| [Eigenwise/atomic-agents](https://github.com/Eigenwise/atomic-agents) | 5,978 | 以原子化方式构建 AI Agent，提供细粒度组合能力。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 192,046 | “与你一起成长的 Agent”，强调记忆与自适应能力。 |

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 82,585 | 领先的开源 RAG 引擎，融合 Agent 能力为 LLM 提供上下文层。 |
| [Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm) | 61,505 | 本地优先的全能 Agent 体验，可私有化部署 RAG 与知识库。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 58,456 | 通用 AI Agent 记忆层，实现跨会话持久化上下文。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 44,751 | 高性能云原生向量数据库，支持大规模 ANN 搜索。 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | 32,065 | 极高性能向量数据库，企业级 AI 搜索引擎。 |
| [pathwaycom/llm-app](https://github.com/pathwaycom/llm-app) | 59,335 | 可即用的云端 RAG 模板，支持实时数据同步与 Docker 部署。 |
| [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) | 82,030 | 将 PDF/图像转为结构化数据，桥接 OCR 与 LLM，支持 100+ 语言。 |

---

## 三、趋势信号分析

今日社区最强烈的信号是 **Agent Skills 生态的爆发**。Trending 榜单中前四名中的三个（agent-skills、superpowers、pm-skills）均围绕“可复用的 Agent 技能/能力”展开，且总新增 stars 超过 4000。这反映出在 Claude Code、Codex、OpenCode 等编程 Agent 工具迅速普及的背景下，开发者正从“自己写 Agent”转向“组装已有专业技能”，技能市场/框架成为新的基础设施层。**LMCache** 作为 LLM 推理优化工具，虽然新增 stars 不高，但其“KV 缓存加速”概念正成为大规模部署的关键组件，预示推理效率赛道持续升温。**openmed** 首次登榜，标志着医疗 AI 开源项目开始获得社区认同，与近期 FDA 对 AI 辅助诊断的开放态度可能有关。此外，主题搜索中 **mem0**（通用记忆层）与 **CopilotKit**（前端 Agent UI 栈）的高关注度，说明 Agent 的长期记忆与交互界面正成为下一个技术热点。

---

## 四、社区关注热点

- **[agent-skills](https://github.com/addyosmani/agent-skills)** – 今日增速最快，提供工程级技能供 Claude Code 等 Agent 使用，是 Agent 技能标准化的重要尝试。
- **[LMCache](https://github.com/LMCache/LMCache)** – 超大 KV 缓存层，对降低 LLM 推理成本、提升响应速度意义重大，适合高并发场景。
- **[mem0](https://github.com/mem0ai/mem0)** – 通用记忆层，解决 Agent“记不住”的痛点，未来或成为 Agent 系统的标配组件。
- **[openmed](https://github.com/maziyarpanahi/openmed)** – 开源医疗 AI 项目，填补垂直领域空白，适合医疗影像、诊断辅助等场景的二次开发。
- **[ragflow](https://github.com/infiniflow/ragflow)** – 持续领跑 RAG 赛道，近期融合 Agent 能力的更新使其成为知识密集型应用的优先选择。

---

*数据来源：GitHub Trending & Search API（2026-06-13），筛选后仅保留 AI/ML 明确相关项目。*

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*