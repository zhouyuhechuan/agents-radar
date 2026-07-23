# Hugging Face 热门模型日报 2026-07-23

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-23 02:04 UTC

---

好的，作为AI模型生态分析师，以下是我为您整理分析的2026年7月23日Hugging Face热门模型日报。

---

### **Hugging Face 热门模型日报 | 2026-07-23**

#### **今日速览**

本周Hugging Face生态中，**国产大模型GLM-5.2**与**Google Gemma-4**两大系列表现抢眼，分别登顶点赞榜和下载榜，显示了开源社区对顶级MoE（混合专家）架构的追捧。**量化模型**持续主导社区热度，从1-bit到2-bit的激进量化方案（如prism-ml的Bonsai系列）下载量惊人，表明用户对端侧部署和效率优化的极致追求。同时，**多模态模型**（尤其是图像文本理解和OCR）依然是最活跃的应用方向，百度、NVIDIA等巨头均有新作上榜。

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** - 作者: zai-org | 点赞: 4,339 | 下载: 545,109
  - 一句话说明：本周最受关注的国产MoE大语言模型，基于DS-A技术实现高效推理，凭借顶尖性能成为榜单焦点。
- **[poolside/Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1)** - 作者: poolside | 点赞: 396 | 下载: 3,056
  - 一句话说明：继初代版本后迭代的代码生成模型，在软件工程任务上表现出色，吸引了大量开发者关注。
- **[Moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** - 作者: moonshotai | 点赞: 1,225 | 下载: 722,058
  - 一句话说明：Kimi系列最新代码专用模型，采用压缩技术降低部署门槛，下载量巨大。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** - 作者: baidu | 点赞: 2,716 | 下载: 2,237,351
  - 一句话说明：百度推出的通用OCR大模型，凭借强大的识别能力和海量下载量，成为本周最热门的多模态应用模型。
- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** - 作者: google | 点赞: 3,328 | 下载: 12,113,203
  - 一句话说明：谷歌新一代开源多模态模型，31B参数具备顶尖的视觉理解能力，下载量断层式领先，堪称“社区顶流”。
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** - 作者: HauhauCS | 点赞: 3,003 | 下载: 1,997,690
  - 一句话说明：基于Qwen3.6的MoE视觉模型社区微调版，主打“无审查”激进风格，话题度和下载量极高。
- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** - 作者: conradlocke | 点赞: 497 | 下载: 0
  - 一句话说明：基于Krea-2基础模型的身份编辑LoRA，代表了社区在可控图像生成上的探索。
- **[nvidia/Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge)** - 作者: nvidia | 点赞: 90 | 下载: 6,623
  - 一句话说明：NVIDIA推出的Cosmos3系列边缘端模型，针对物理世界理解与生成，拓展了工业应用边界。
- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** - 作者: Alissonerdx | 点赞: 235 | 下载: 0
  - 一句话说明：用于视频生成的身份保持LoRA，旨在解决视频制作中的人脸一致性问题。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[NVIDIA/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** - 作者: nvidia | 点赞: 914 | 下载: 590,230
  - 一句话说明：NVIDIA推出的流式语音识别（ASR）模型，专注实时场景，在语音领域表现强势。
- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** - 作者: OpenMOSS-Team | 点赞: 308 | 下载: 92,265
  - 一句话说明：集成了语音转录和说话人分离功能的音频文本模型，为用户提供了实用的一站式音频处理方案。
- **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** - 作者: openbmb | 点赞: 154 | 下载: 58
  - 一句话说明：面向机器人操作的视觉-语言-动作（VLA）模型，代表了AI从“感知”向“行动”延伸的重要方向。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** - 作者: prism-ml | 点赞: 946 | 下载: 432,196
  - 一句话说明：采用突破性的2-bit三元量化技术，将27B模型压缩至极小尺寸，是量化领域的明星项目。
- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** - 作者: prism-ml | 点赞: 596 | 下载: 1,404,962
  - 一句话说明：Bonsai系列基础量化版，1-bit极端量化引发了社区对模型“最小化”可能性的广泛讨论。
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** - 作者: empero-ai | 点赞: 2,417 | 下载: 2,133,420
  - 一句话说明：基于Qwen3.5的社区微调模型，融合了Claude的“思考”风格，下载量巨大。
- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** - 作者: DavidAU | 点赞: 323 | 下载: 62,842
  - 一句话说明：社区极简命名的典型案例，基于Qwen3.6的激进微调与量化模型，实验性质浓厚。

---

#### **生态信号**

本周生态呈现 **“一超多强，量化为王”** 的格局。
- **模型家族势头**：Google **Gemma** 和智谱 **GLM** 两大系列形成第一梯队，通过大规模开源抢夺生态位。**Qwen** 系列则成为社区微调的首选基座，衍生模型数量众多。
- **开源 vs 闭源**：开源权重模型的竞争已趋于白热化，头部项目均通过开源完全权重来建立壁垒。闭源API厂商在HuggingFace上的影响力正被开源社区浪潮所稀释。
- **量化与微调**：**1-bit/2-bit量化**（如Bonsai）成为新热点，其极致的压缩比率和保留部分性能的能力挑战了传统量化认知。社区微调活动高度集中于 **“无审查（Uncensored）”** 和对特定模型风格（如Claude风格）的融合。

---

#### **值得探索**

1.  **🧪 [zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**
    - **理由**：作为本周点赞最高的模型，它不仅代表了国产MoE技术的最新高度，更是开源社区性能竞赛的“新王”。尝试研究其DS-A架构，对理解下一代高效MoE至关重要。

2.  **🔥 [prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)**
    - **理由**：探索1-bit/2-bit量化的终极边界。如果你关注模型部署、边缘计算和硬件效率，这是当前最具研究价值的实验对象。它告诉我们，在极端压缩下，模型能力的下限在哪里。

3.  **🤖 [openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)**
    - **理由**：从“纸上谈兵”到“动手操作”，这是AI领域最激动人心的转变之一。这个模型是通往具身智能的桥梁，值得所有对机器人、自动化感兴趣的开发者深入研究。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*