# Hugging Face 热门模型日报 2026-07-25

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-25 01:59 UTC

---

好的，作为AI模型生态分析师，这是为您整理的2026年7月25日 Hugging Face 热门模型日报。

---

### 《Hugging Face 热门模型日报》 — 2026-07-25

---

### 📈 今日速览

今日Hugging Face生态多点开花，核心趋势围绕“量化多模态”与“巨型MoE模型”。**Google Gemma-4-31B** 和 **Qwen Qwen3.6-35B-A3B** 凭借强大的原生多模态能力与海量下载量，成为最受关注的旗舰模型。以 **Unlimited-OCR** 与 **Inkling** 为代表的专用多模态模型表现抢眼，显示出社区对结构化数据提取和交互式AI的强烈需求。此外，量化与微调活动异常活跃，围绕**GLM-5.2**、**Qwen3.6**等基座模型的GGUF版本占据了榜单半壁江山。

---

### 📊 热门模型分类盘点

#### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 👍点赞 📥下载 | 一句话说明 |
| :--- | :--- | :--- | :--- |
| **[Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** | upstage | 541 / 1,106 | Upstage开源的250B参数MoE大模型，主打高性能开放权重大语言模型。 |
| **[Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** | Nanbeige | 372 / 8,169 | 小参数（3B）高效能语言模型，适合边缘设备与快速部署场景。 |
| **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** | zai-org | 4,415 / 667,403 | 智谱AI强大的MoE架构模型，凭借高推理质量和灵活的DSA（动态稀疏注意力）技术，成为近期最热门的基座模型之一。 |
| **[Motif-3-Beta](https://huggingface.co/Motif-Technologies/Motif-3-Beta)** | Motif-Technologies | 185 / 2,108 | 一款专注于特征提取的模型，可能用于RAG或特定知识库场景。 |
| **[antares-1b](https://huggingface.co/fdtn-ai/antares-1b)** | fdtn-ai | 149 / 4,266 | 专注安全的1B小模型，使用GraniteMoEHybrid架构，表明小模型安全对齐是一个细分方向。 |
| **[Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1)** | poolside | 611 / 28,992 | 生产级文本生成模型，适用于代码生成等专业任务。多个量化版本同日在榜，显示其实用性。 |

#### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 👍点赞 📥下载 | 一句话说明 |
| :--- | :--- | :--- | :--- |
| **[Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** | baidu | 3,014 / 2,500,391 | 百度开源的通用OCR模型，支持多语言、多场景，下载量惊人，是图像转文本的标杆工具。 |
| **[Inkling](https://huggingface.co/thinkingmachines/Inkling)** | thinkingmachines | 1,546 / 27,883 | 一款具备对话能力的图像理解模型，可能主打视觉问答与交互式分析。 |
| **[Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)** | microsoft | 234 / 891 | 微软的文本到图像生成模型，支持图像编辑，标志着大厂在生成式AI上的持续投入。 |
| **[Qwen3.6-27B-Fable...GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** | DavidAU | 486 / 407,421 | 基于Qwen3.6的社区微调版，带"Uncensored"标签，表明社区对无审查模型的特殊兴趣。 |
| **[Qwen3.6-35B-A3B-Uncensored...GGUF](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** | HauhauCS | 3,069 / 2,057,103 | 同样是Qwen3.6的无审查量化版，下载量极高，反映了社区对高性能且无限制多模态模型的追捧。 |
| **[Gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** | google | 3,360 / 12,629,921 | Google的旗舰多模态模型，以令人难以置信的下载量位列前茅，是当前最受关注的开源模型之一。 |
| **[Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** | Qwen | 2,503 / 6,460,680 | Qwen官方推出的MoE多模态模型（35B总参数，3B活跃），凭借高性价比和多模态能力引爆社区。 |
| **[QVQ-Plus](https://huggingface.co/Qwen/QVQ-Plus)** | Qwen | 1,196 / 619,841 | Qwen推出的大视觉语言模型，强化了视觉推理能力。 |
| **[Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge)** | nvidia | 112 / 30,303 | NVIDIA开源的物理世界理解与生成模型，可能用于自动驾驶或机器人仿真。 |
| **[nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** | nvidia | 937 / 797,525 | NVIDIA推出的流式自动语音识别模型，专注于低延迟的语音交互。 |
| **[Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** | moonshotai | 1,263 / 756,668 | 月之暗面推出的代码多模态模型，使用压缩张量技术，专注代码场景下的图像理解。 |

#### 🔧 专用模型（代码、数学、医疗、嵌入）

| 模型 | 作者 | 👍点赞 📥下载 | 一句话说明 |
| :--- | :--- | :--- | :--- |
| **[MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** | openbmb | 173 / 559 | 专为机器人操作设计的视觉-语言-动作模型，是具身智能领域的有力探索。 |
| **[MiniCPM-RobotTrack](https://huggingface.co/openbmb/MiniCPM-RobotTrack)** | openbmb | 123 / 349 | 与RobotManip同系列，专注于机器人轨迹跟踪，显示了在机器人领域的持续深耕。 |
| **[KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev)** | Kwaipilot | 125 / 396 | 基于Qwen3.5的代码专用MoE模型，专注编程辅助。 |

#### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 👍点赞 📥下载 | 一句话说明 |
| :--- | :--- | :--- | :--- |
| **[Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** | prism-ml | 1,006 / 595,415 | 使用2-bit三元量化的27B模型，极限压缩的代表，下载量很高，说明社区对极端量化感兴趣。 |
| **[Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** | prism-ml | 632 / 2,028,115 | 同样是Bonsai模型家族，使用更极端的1-bit量化，是追求极致部署效率的典型。 |
| **[Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V5-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V5-GGUF)** | LuffyTheFox | 134 / 36,703 | Qwen3.6的又一变体，融合了Hermes风格，是无审查微调与量化的结合。 |
| **[GLM-5.2-Vision-NVFP4](https://huggingface.co/baseten/GLM-5.2-Vision-NVFP4)** | baseten | 90 / 494 | GLM-5.2的多模态量化版，采用NVIDIA的NVFP4格式，表明云服务商在推动特定硬件上的量化部署。 |
| **[Laguna-S-2.1-GGUF](https://huggingface.co/poolside/Laguna-S-2.1-GGUF)** | poolside | 133 / 62,092 | Laguna的官方GGUF版本，方便在llama.cpp等工具链上本地部署。 |

---

### 🔍 生态信号

- **MoE与多模态融合势不可挡**：榜单中的头部模型（如 **Qwen3.6** 和 **GLM-5.2**）普遍采用MoE（混合专家）架构，结合强大的多模态能力，在提高性能的同时控制了推理成本，这已成为新一代基座模型的标准范式。
- **开源权重模型主宰生态**：榜单前30名均为可下载的权重，且大厂（Google、Qwen、百度、NVIDIA、微软）的贡献占据高位，证明了开放权重策略在推动生态繁荣和社区采纳上的绝对优势。**Gemma**和**Qwen**两大系列呈现出双龙戏珠的态势。
- **量化与“无审查”微调形成热潮**：围绕 **Qwen3.6**、**GLM-5.2** 等基座模型的量化版本（GGUF）和社区微调（带“Uncensored”标签）占据了大量篇幅。这表明社区对本地化部署和内容自由的强烈渴望，极限量化（如2-bit/1-bit）成为降低门槛的关键技术。

---

### 💡 值得探索

1.  **`zai-org/GLM-5.2`**
    - **理由**：它不仅点赞数高居榜首，其下载/点赞比极高，说明很多用户下载并实际使用它。作为一款采用DSA（动态稀疏注意力）的MoE模型，它代表了中文大模型在架构创新上的前沿，值得研究其长上下文处理能力。

2.  **`prism-ml/Ternary-Bonsai-27B-gguf` & `prism-ml/Bonsai-27B-gguf`**
    - **理由**：这两款模型代表了量化技术的极限探索（2-bit和1-bit）。对于希望在消费级硬件上运行27B大模型的开发者来说，这是极其宝贵的资源。评估其在极端压缩下的能力损失，对边缘AI部署有重要参考价值。

3.  **`nvidia/Cosmos3-Edge`**
    - **理由**：作为NVIDIA开源的物理世界理解模型，它可能成为机器人、自动驾驶和数字孪生领域的重要基石。相比其他语言或多模态模型，它开辟了“世界模型”这一前沿赛道，值得所有对具身智能和物理AI感兴趣的人深入探索。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*