# Hugging Face 热门模型日报 2026-07-14

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-14 01:49 UTC

---

好的，作为AI模型生态分析师，我为您整理了2026年7月14日的Hugging Face热门模型日报。

---

### Hugging Face 热门模型日报 (2026-07-14)

#### 1. 今日速览

本周 Hugging Face 生态依旧火热，**Qwen** 家族（特别是 3.5/3.6 系列）成为绝对主导，围绕其进行的微调、量化（GGUF）和多模态增强模型霸占了榜单的多数席位。同时，**GLM-5.2** 和 **DeepSeek-V4-Flash** 作为重量级开源模型持续获得高关注。值得注意的是，量化格式（特别是 GGUF）已成为社区部署的标准选择，而如 **Unlimited-OCR**、**TabFM** 等垂直领域的专用模型也展现出强劲的流行度，标志着AI技术的应用正在快速细分化。

#### 2. 热门模型

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** (tencent, 点赞: 754, 下载: 9,157)
  - 继Hunyuan系列后的最新版本，代表了腾讯在通用文本生成领域的持续投入，因其强大的中文能力和综合性能登上趋势榜。

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** (zai-org, 点赞: 3,901, 下载: 464,914)
  - 智谱AI最新的高端开源语言模型，采用创新的MoE架构（glm_moe_dsa），凭借其顶尖的对话和推理能力获得了社区极高的关注度。

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** (InternScience, 点赞: 526, 下载: 29,801)
  - 基于Qwen3.5 MoE的智能体模型，专门为工具调用和任务自主完成优化，是“智能体（Agent）”概念在开源社区落地的代表。

- **[nvidia/Nemotron-Labs-Audex-30B-A3B](https://huggingface.co/nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4)** (nvidia, 点赞: 114/143, 下载: 38,775/1,058)
  - NVIDIA推出的高效MoE模型系列（30B总参/3B激活），代表了顶尖厂商在推理效率和模型性能间平衡的最新探索。

- **[jlnsrk/GLM-5.2-colibri-int4](https://huggingface.co/jlnsrk/GLM-5.2-colibri-int4)** (jlnsrk, 点赞: 87, 下载: 1,997)
  - GLM-5.2的4比特CPU量化版本，专为低资源设备上的高效推理设计，反映了社区对模型本地化部署的强烈需求。

- **[SupraLabs/Supra-Router-51M](https://huggingface.co/SupraLabs/Supra-Router-51M)** (SupraLabs, 点赞: 114, 下载: 1,573)
  - 一个轻量级的“路由”模型，用于智能调度不同LLM，是构建混合专家系统或模型编排的基础设施组件。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** (empero-ai, 点赞: 2,084, 下载: 1,985,221)
  - 基于Qwen3.5的视觉语言模型，通过大量合成数据（Claude生成）进行微调，旨在融合多种风格生成能力，受到社区创作者热捧。

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** (baidu, 点赞: 1,963, 下载: 1,506,937)
  - 百度推出的通用OCR模型，能处理各种复杂场景的文字识别，其强大的实用性和高精度使其在应用层面热度极高。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored...](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** (HauhauCS, 点赞: 2,710, 下载: 2,512,124)
  - Qwen3.6的“无审查”MoE版本，以去除内容限制和激进的回答风格为卖点，在特定社区中下载量极高，反映了内容安全与开放性之间的持续张力。

- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** (Alissonerdx, 点赞: 124, 下载: 0)
  - 专注于视频生成中的面部身份保留的LoRA模型，与LTX-Video结合使用，是社区在视频生成细分化方向上的探索。

- **[CohereLabs/cohere-transcribe-arabic-07-2026](https://huggingface.co/CohereLabs/cohere-transcribe-arabic-07-2026)** (CohereLabs, 点赞: 102, 下载: 11,647)
  - Cohere推出的阿拉伯语自动语音识别模型，填补了小语种ASR的开源空白，并展现了其在该领域的投入。

- **[nineninesix/gepard-1.0](https://huggingface.co/nineninesix/gepard-1.0)** (nineninesix, 点赞: 95, 下载: 3,940)
  - 基于Qwen3.5的文本到语音模型，表明多模态大型模型与特定领域任务（如TTS）的结合正成为新趋势。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** (google, 点赞: 362, 下载: 21,590)
  - Google发布的基础表格模型，支持零样本分类与回归，标志着LLM技术向传统结构化数据分析领域的重大扩展。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[open-gigaai/Giga-World-1](https://huggingface.co/open-gigaai/Giga-World-1)** (open-gigaai, 点赞: 128, 下载: 0)
  - 一个开源的文生图/视频模型，目前以基础权重形式发布，预示着一个大规模、高质量的开源生成模型的到来。

- **[unsloth/DeepSeek-V4-Flash-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-GGUF)** (unsloth, 点赞: 162, 下载: 49,423)
  - DeepSeek-V4的GGUF量化版本，通过Unsloth的优化技术实现高效推理，代表着顶级开源模型生态向标准量化格式的迁移。

- **[yuxinlu1/gemma-4-12B-agentic-fable5...-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** (yuxinlu1, 点赞: 1,178, 下载: 452,627)
  - 针对编程和终端操作的Gemma-4微调模型，展现了社区在提升基础模型特定任务（如Agentic Coding）能力上的高超技巧。

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** (deepreinforce-ai, 点赞: 868, 下载: 1,392,300)
  - 一个高质量的开源35B模型，其GGUF版本下载量巨大，证明了社区对中等规模、易于部署且性能出色的模型有着极高的需求。

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** (unsloth, 点赞: 1,074, 下载: 2,901,906)
  - Qwen3.6-27B的GGUF量化版，本周下载量最高，是整个生态中“量化为王”趋势的最佳体现。

#### 3. 生态信号

- **Qwen 家族巩固统治地位**：无论是官方版、社区微调版（如 Qwythos）还是量化版（如 unsloth），Qwen 系列（尤其是3.5/3.6）已成为当前开源社区最核心的基座模型，性能、易用性和生态支持都达到了新高度。
- **MoE 成为主流架构**：前10名中，GLM-5.2、Agents-A1、Audex 等多款模型均采用混合专家（MoE）架构。这证明在追求性能与参数量平衡的竞赛中，MoE 已成为行业共识。
- **量化即标准，GGUF 统治边缘**：从生态看，几乎所有主流模型都会在第一时间推出 GGUF 版。以 **unsloth** 为代表的量化工具和社区成为连接前沿模型与普通用户的关键桥梁，降低了部署门槛。
- **开源权重模型全面领先**：榜单前十主要为开源权重模型。尽管闭源API能力强大，但社区的绝对焦点仍在“可下载、可本地运行”的开放模型上。

#### 4. 值得探索

1.  **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**：作为当前最受瞩目的MoE开源LLM之一，其独特的架构设计和顶尖的中英文能力，值得任何对前沿模型技术感兴趣的从业者深入研究。
2.  **[nvidia/Nemotron-Labs-Audex-30B-A3B](https://huggingface.co/nvidia/Nemotron-Labs-Audex-30B-A3B)**：NVIDIA提出的超高效率模型（30B参数，仅3B激活），是研究“花小钱办大事”的最前沿样本，对资源有限但追求高性能的团队有极大启发。
3.  **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)**：这是AI技术从NLP/CV向结构化数据（如金融、工业场景）攻城略地的标志性产品。探索它如何将Transformer能力应用于传统表格分析，预示着数据科学工作流的未来变革。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*