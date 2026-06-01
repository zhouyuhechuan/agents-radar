# AI 开源趋势日报 2026-06-01

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-01 02:55 UTC

---

# AI 开源趋势日报｜2026-06-01

---

## 今日速览

- **Claude Code 开源引爆社区**：Anthropic 官方发布的终端 Agent 工具 `claude-code` 今日新增 489 stars，结合 Hermes Agent、OpenHands 等同类项目，AI 编程 Agent 已成为最热赛道。
- **从零训练 LLM 教程受追捧**：`train-llm-from-scratch` 今日斩获 626 stars，社区对“低门槛理解大模型原理”的需求持续高涨。
- **多模态生成应用持续爆发**：`MoneyPrinterTurbo`（短视频生成）新增 1937 stars，`VoxCPM`（语音合成与克隆）新增 635 stars，AI 视频/音频生成仍是流量入口。
- **记忆与 RAG 进入实用化阶段**：`supermemory`（专为 AI Agent 设计的记忆引擎）和 `claude-mem`（持久上下文）在 Trending 和主题搜索中均表现突出，轻量级记忆层正替代复杂 RAG 管线。

---

## 各维度热门项目

### 🔧 AI 基础工具（框架、推理引擎、CLI、SDK）

1. **[ollama](https://github.com/ollama/ollama)** ⭐172,763  
   本地运行 LLM 的一站式工具，支持 Kimi、DeepSeek、Qwen 等主流模型，是开发者和个人用户最常用的推理基础设施。

2. **[huggingface/transformers](https://github.com/huggingface/transformers)** ⭐161,130  
   🤗 Transformer 模型定义与训练框架，覆盖文本、视觉、音频、多模态，是 AI 社区最广泛使用的模型库。

3. **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐81,512  
   高性能、高吞吐的 LLM 推理引擎，已成为生产环境部署 LLM 的首选方案。

4. **[firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)** ⭐126,922  
   专为 AI Agent 设计的 Web 数据抓取 API，支持大规模搜索、爬取和结构化交互。

5. **[pytorch/pytorch](https://github.com/pytorch/pytorch)** ⭐100,301  
   动态张量与神经网络框架，兼具研究灵活性与生产级 GPU 加速能力。

6. **[tensorflow/tensorflow](https://github.com/tensorflow/tensorflow)** ⭐195,345  
   成熟的端到端机器学习框架，覆盖从研究到部署的全链路。

---

### 🤖 AI 智能体 / 工作流（Agent 框架、自动化、编程助手）

1. **[anthropics/claude-code](https://github.com/anthropics/claude-code)** ⭐0 (+489 today)  
   Claude Code 是 Anthropic 官方的终端 Agent 编程工具，可理解代码库、执行 Git 操作、完成复杂编程任务，是今日 Trending 的明星项目。

2. **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** ⭐184,682  
   开源自主 Agent 的代表，让 AI 自动规划和执行多步骤任务，持续引领 Agent 范式。

3. **[OpenHands/OpenHands](https://github.com/OpenHands/OpenHands)** ⭐75,512  
   🙌 AI 驱动开发平台，通过 Agent 自动化编码、调试、部署，大幅提升研发效率。

4. **[browser-use/browser-use](https://github.com/browser-use/browser-use)** ⭐96,445  
   🌐 让 AI Agent 直接操控浏览器执行在线任务，如数据采集、表单填写、自动化测试。

5. **[langgenius/dify](https://github.com/langgenius/dify)** ⭐143,318  
   生产级 Agentic Workflow 开发平台，内置 RAG 和可视化编排，是构建复杂 AI 应用的核心工具。

6. **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐174,837  
   “与你一起成长的 Agent”，结合记忆、工具调用和自主进化能力，开源社区活跃度极高。

7. **[revfactory/harness](https://github.com/revfactory/harness)** ⭐0 (+323 today)  
   元技能框架，可设计领域特定的 Agent 团队并自动生成协作技能，代表 Agent 工程化新方向。

8. **[shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code)** ⭐63,893  
   从零实现 Claude Code 类 Agent Harness 的教程，帮助开发者理解 Agent 内部原理。

---

### 📦 AI 应用（垂直场景、生成工具、智能助手）

1. **[harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo)** ⭐0 (+1,937 today)  
   利用 LLM 一键生成高清短视频，融合脚本、配音、画面生成，是今日新增星数最高的项目。

2. **[OpenBMB/VoxCPM](https://github.com/OpenBMB/VoxCPM)** ⭐0 (+635 today)  
   无 Tokenizer 的多语言语音生成与克隆模型，支持创意语音设计和逼真克隆，在音频生成领域引发关注。

3. **[open-webui/open-webui](https://github.com/open-webui/open-webui)** ⭐139,418  
   友好的用户界面，支持 Ollama、OpenAI 等多种后端，是本地/自建 AI 工具的首选交互层。

4. **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐46,672  
   AI 生产力工作室，集智能对话、自主 Agent、300+ 助手于一体，统一管理前沿 LLM。

5. **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** ⭐22,974  
   AI 从任意文档生成真正的 PowerPoint 文件，支持原生形状、动画、配音，可自定义模板。

6. **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** ⭐39,656  
   LLM 驱动的 A/H/美股智能分析系统，结合多数据源、实时新闻和 LLM 决策仪表盘。

7. **[Crosstalk-Solutions/project-nomad](https://github.com/Crosstalk-Solutions/project-nomad)** ⭐0 (+374 today)  
   自包含离线生存计算机，内置 AI 知识库和工具，可在无网络环境下提供智能支持。

---

### 🧠 大模型 / 训练（训练框架、微调、评估、教程）

1. **[FareedKhan-dev/train-llm-from-scratch](https://github.com/FareedKhan-dev/train-llm-from-scratch)** ⭐0 (+626 today)  
   手把手教程，从数据下载到文本生成，完整训练一个小型 LLM，适合入门学习。

2. **[hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory)** ⭐71,741  
   统一高效微调 100+ LLM & VLM 的框架，支持 LoRA、QLoRA 等，被广泛用于定制化模型。

3. **[jingyaogong/minimind](https://github.com/jingyaogong/minimind)** ⭐50,905  
   🧠 2 小时从零训练 64M 参数小模型，极大降低理解大模型训练的门槛。

4. **[open-compass/opencompass](https://github.com/open-compass/opencompass)** ⭐7,048  
   覆盖 100+ 数据集的大模型评测平台，支持 Llama、Qwen、GLM 等主流模型。

5. **[skyzh/tiny-llm](https://github.com/skyzh/tiny-llm)** ⭐4,220  
   面向系统工程师的 LLM 推理服务课程，在 Apple Silicon 上搭建迷你 vLLM + Qwen 实践。

6. **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** ⭐239  
   可靠、最小化的基础模型与世界模型预训练库，面向希望复现 SOTA 训练流程的研究者。

---

### 🔍 RAG / 知识库（向量数据库、检索增强、记忆层）

1. **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐81,608  
   领先的开源 RAG 引擎，融合检索增强与 Agent 能力，为 LLM 提供高质量上下文层。

2. **[milvus-io/milvus](https://github.com/milvus-io/milvus)** ⭐44,561  
   高性能云原生向量数据库，专为大规模向量近似搜索设计，是 RAG 系统的核心基础设施。

3. **[thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)** ⭐79,915  
   为 Agent 提供持久跨会话上下文的记忆引擎，自动压缩历史并注入相关上下文，兼容 Claude Code、Copilot 等多种 Agent。

4. **[mem0ai/mem0](https://github.com/mem0ai/mem0)** ⭐57,228  
   通用 AI Agent 记忆层，可为任意 Agent 添加长期记忆能力，代码简洁易集成。

5. **[HKUDS/LightRAG](https://github.com/HKUDS/LightRAG)** ⭐36,014  
   [EMNLP2025] 简单快速的 RAG 框架，强调轻量和高效，适合资源受限环境。

6. **[PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR)** ⭐79,159  
   将 PDF/图片转化为结构化数据，支持 100+ 语言，是连接文档和 LLM 的关键 OCR 工具箱。

7. **[supermemoryai/supermemory](https://github.com/supermemoryai/supermemory)** ⭐0 (+264 today)  
   面向 AI Agent 的极速可扩展记忆引擎和 App，提供 Memory API，替代复杂 RAG 管线。

8. **[safishamsi/graphify](https://github.com/safishamsi/graphify)** ⭐57,418  
   将代码库、SQL 模式、文档等任意文件夹转化为可查询的知识图谱，增强 Agent 对复杂系统的理解。

---

## 趋势信号分析

今日 AI 开源社区呈现三大趋势：

1. **Agent 编程工具集中爆发**：`claude-code`、`hermes-webui`、`compound-engineering-plugin`、`harness` 等多个 Agent 相关项目同时登榜 Trending，表明开发者对“AI 编程配合”的需求已从玩具级进入生产级。特别是 `claude-code` 作为官方工具开源，可能推动 Agent 编程标准化。

2. **从“用模型”到“造模型”的转变**：`train-llm-from-scratch` 和 `minimind` 的高关注度说明，社区不再满足于调用 API，而是希望理解并自主训练小模型。这与近期 DeepSeek、Kimi 等国产模型的开源浪潮相呼应，小参数模型训练工具和教程成为新的流量入口。

3. **多模态生成与记忆层成为基础设施**：视频生成（MoneyPrinterTurbo）、语音合成（VoxCPM）今日新增星数均超过 500，显示生成式 AI 的应用层仍在野蛮生长。同时，`supermemory`、`mem0`、`claude-mem` 等记忆项目集中出现，

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*