# Hugging Face 热门模型日报 2026-07-24

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-24 01:59 UTC

---

好的，作为AI模型生态分析师，以下是根据您提供的2026年7月24日数据生成的《Hugging Face 热门模型日报》。

---

### Hugging Face 热门模型日报 | 2026年7月24日

#### 今日速览

本周 Hugging Face 榜单呈现三大亮点：**多模态模型全面主导**，前三位中有两个为 image-text-to-text 任务，且下载量均达百万级；**中文模型开源力量崛起**，百度、智谱（GLM-5.2）和上海 AI Lab（OpenMOSS）均有高热度模型上榜；**量化与社区微调生态极度活跃**，针对 Qwen3.6 的微调变体（如 uncensored、GGUF）占据大量席位，并出现了 1-bit / 2-bit 的极致量化尝试。此外，Google 的 Gemma-4 以超千万下载量持续领跑，显示了顶级闭源转开源模型的影响力。

---

#### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 点赞数 | 下载数 | 一句话说明 |
| :--- | :--- | :--- | :--- | :--- |
| **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** | zai-org | **4,371** | 596k | 智谱最新开源旗舰，采用 MoE 架构，自发布以来持续获社区高度关注。 |
| **[poolside/Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1)** | poolside | 516 | 13k | 专注于代码生成的 S 级模型，本周出现多个变体（如 NVFP4、GGUF），表明企业级部署正在推进。 |
| **[upstage/Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** | upstage | 450 | 362 | Upstage 开源的 250B 大参数模型，代表了韩国开源社区的技术前沿。 |
| **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** | Nanbeige | 322 | 4.5k | 新晋的 3B 级别中文小模型，适合资源受限的本地部署场景。 |
| **[Motif-Technologies/Motif-3-Beta](https://huggingface.co/Motif-Technologies/Motif-3-Beta) | Motif-Technologies | 173 | 1.8k | 新一代特征提取/通用文本生成模型，Beta 版正吸引开发者尝鲜。 |

#### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞数 | 下载数 | 一句话说明 |
| :--- | :--- | :--- | :--- | :--- |
| **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** | baidu | **2,891** | **2.4M** | 百度开源的通用 OCR 模型，支持任意文字图像转文本，是本周最实用的多模态工具。 |
| **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** | thinkingmachines | 1,508 | 24k | 一款拥有对话能力的强大多模态模型，将视觉理解与对话交互深度结合。 |
| **[Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice](https://huggingface.co/Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice)** | Qwen | 1,799 | **2.5M** | 通义千问带来的高质量 TTS 模型，支持定制音色，广泛用于内容创作。 |
| **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** | google | 3,347 | **12.6M** | Google 开放的最强 Gemma 系列模型，超千万下载量证明其指令遵循与多模态能力的统治力。 |
| **[microsoft/Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)** | microsoft | 185 | 411 | 微软推出的文本到图像/编辑流程模型，旨在简化生成式 AI 的图像创作。 |
| **[Moonshot AI/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** | moonshotai | 1,249 | 766k | 月之暗面推出的代码专业版模型，专注编程与代码理解。 |
| **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** | ATH-MaaS | 257 | 26k | 另一个基于 Qwen3.5 的 OCR 模型，体现了该领域的高活跃度。 |
| **[nvidia/Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge)** | nvidia | 100 | 28k | NVIDIA 发布的 Cosmos 系列边缘计算版模型，关注在端侧的多模态生成能力。 |

#### 🔧 专用模型（代码、数学、医疗、ASR、嵌入）

| 模型 | 作者 | 点赞数 | 下载数 | 一句话说明 |
| :--- | :--- | :--- | :--- | :--- |
| **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** | nvidia | 926 | 750k | NVIDIA 强大的流式语音识别模型，主打低延迟高精度。 |
| **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** | OpenMOSS-Team | 320 | 111k | 来自上海 AI Lab 的音频转文字 + 说话人分离模型，会议纪要等场景的利器。 |
| **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** | openbmb | 165 | 408 | 面壁智能开源的具身智能模型，将视觉语言模型直接应用在机器人操控。 |
| **[fdtn-ai/antares-1b](https://huggingface.co/fdtn-ai/antares-1b)** | fdtn-ai | 121 | 2.7k | 专注于安全的 1B 级别语言模型，面向对安全性有严格要求的垂直领域。 |

#### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 点赞数 | 下载数 | 一句话说明 |
| :--- | :--- | :--- | :--- | :--- |
| **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** | HauhauCS | 3,033 | **2.0M** | 基于 Qwen3.6 的激进步长 MoE 模型，打破了审查限制，社区下载量极高。 |
| **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** | empero-ai | 2,439 | **2.1M** | 使用 Claude 合成数据进行微调，并量化后的社区明星模型，推理能力极强。 |
| **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** | prism-ml | 984 | 576k | 采用创新三值量化的 27B 模型，在极低精度下显著缩小模型体积。 |
| **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** | prism-ml | 620 | **1.9M** | 同样来自 prism-ml，将 27B 参数模型压缩至 1-bit，是极致量化的代表。 |
| **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored...](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** | DavidAU | 397 | 334k | 以超长模型名著称的社区微调版，无审查的丰富角色扮演模型。 |

---

#### 生态信号

1.  **模型家族势头**：**Qwen 生态**在本周占据统治地位，几乎所有高下载量的社区微调或量化模型都基于 Qwen 3.5 / 3.6 系列，显示了其作为“AI 底座”的深厚生态。智谱 **GLM 系列** 的快速迭代和百度 **Unlimited-OCR** 的实用性上榜，体现了中国开源大模型的强势崛起。
2.  **开源 vs 闭源**：本周榜单完全由**开源权重模型**主导。然而，来自 Google 的 Gemma-4 和 NVIDIA 的 Nemotron 系列，虽然开放权重，但背后有顶级闭源公司的强力支持，标志着“大厂开源”模式的成熟与成功。
3.  **量化与微调趋势**：社区对**低比特量化（1-bit, 2-bit）** 的热情空前高涨，Bonsai 系列等模型证明了将大型模型部署到本地的可能性。同时，“Uncensored”微调模型的大量出现，反映出社区对非审查制对话的强烈需求，但也带来了安全与伦理方面的潜在讨论。

---

#### 值得探索

1.  **zai-org/GLM-5.2**：作为国产 MoE 模型的代表，其高点赞数值得深入研究其架构设计和应用表现，是体验中国前沿大模型能力的最佳入口。
2.  **thinkingmachines/Inkling**：作为本周多模态黑马，其将对话能力与图像文本处理结合得较好，可探索其在智能助理、内容理解等场景下的创新应用。
3.  **prism-ml/Ternary-Bonsai-27B-gguf**：对于研究模型压缩与边缘部署的开发者和研究者而言，这个三值量化模型是必选项，它的表现证明了极端量化并非不可行。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*