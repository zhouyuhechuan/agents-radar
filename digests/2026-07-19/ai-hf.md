# Hugging Face 热门模型日报 2026-07-19

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-19 01:58 UTC

---

好的，以下是基于您提供的 2026 年 7 月 19 日 Hugging Face 热门模型数据生成的日报。

---

## **HuggingFace 热门模型日报 | 2026-07-19**

### **今日速览**

今日榜单由 **GLM-5.2** 和 **Gemma-4-31B** 两大旗舰模型领衔，标志着开源大模型进入新一轮能力竞赛。**多模态（特别是图像-文本到文本）成为绝对主流**，前十名中近半数为多模态模型。量化生态异常活跃，**Bonsai 系列（1-bit/2-bit）和 Qwythos 系列的高下载量**，表明社区对极致部署效率的追求已超越传统蒸馏。此外，**百度发布的 Unlimited-OCR** 以200万下载量位居前列，显示出垂直领域专业模型仍有巨大市场。

---

### **热门模型**

#### 🧠 语言模型（LLM、对话模型、指令微调）

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** | 作者：zai-org | 点赞：4,126 | 下载：541,662
  - zai-org 的旗舰级通用对话模型，采用 MoE 架构，以出色性能夺得本周点赞和热度双料冠军。

- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** | 作者：google | 点赞：3,263 | 下载：12,608,008
  - Google 开源第四代轻量级指令模型，体积适中但性能强劲，是迄今为止下载量最高的模型之一，体现了 Google 在开源生态的强大号召力。

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** | 作者：tencent | 点赞：829 | 下载：13,571
  - 腾讯推出的 Hy3 第三代文本生成模型，基于 Hunyuan 架构，是近期国产大模型开源的重要代表。

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** | 作者：InternScience | 点赞：579 | 下载：35,575
  - 基于 Qwen3.5 MoE 架构的 Agent 专用模型，强调工具调用能力，是 Agent 生态繁荣的直接证明。

#### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** | 作者：thinkingmachines | 点赞：1,063 | 下载：12,456
  - 创新多模态模型，支持图像/文本/音频综合理解，代表了多模态模型向“全能感知”进化。

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** | 作者：empero-ai | 点赞：2,315 | 下载：2,112,869
  - 基于 Qwen3.5 的 9B 级多模态推理模型（GGUF 量化版），极高的下载量表明社区对高质量小型多模态模型的渴求。

- **[HauhauCS/Qwen3.6-35B-A3B-Une–HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** | 作者：HauhauCS | 点赞：2,865 | 下载：2,190,398
  - 基于 Qwen3.6 的 MoE 视觉模型，以“无审查”和“激进”风格为卖点，在社区引发较大关注。

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** | 作者：baidu | 点赞：2,025 | 下载：2,088,470
  - 百度开源的全能 OCR 模型，下载量超 200 万，证明了通用图像文字识别在金融、文档处理等领域的极高应用价值。

- **[Wan-AI/Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)** | 作者：Wan-AI | 点赞：114 | 下载：2,328
  - 专门用于图像到视频生成的 14B 模型，是视频生成赛道的重要新星，专注于舞蹈等动态场景生成。

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** | 作者：OpenMOSS-Team | 点赞：259 | 下载：86,385
  - 音频到文本的专业模型，支持语音识别与说话人分离，是多模态从视觉向听觉延伸的代表。

#### 🔧 专用模型（代码、数学、医疗、嵌入）

- **(暂无显著高赞的代码/数学/医疗模型上榜，本周期专用模型主要集中在工具调用和嵌入方向)**

- **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** | 作者：Cactus-Compute | 点赞：268 | 下载：935
  - 基于 JAX 的轻量级工具调用（Function Calling）模型，专门为 Agent 类应用设计，代表着小而专的模型趋势。

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** | 作者：froggeric | 点赞：941 | 下载：0
  - 不是模型，而是为 Qwen 系列模型修复的聊天模板配置文件，超高点赞说明基础工程对社区同样至关重要。

#### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** | 作者：prism-ml | 点赞：737 | 下载：301,893
  - 27B 参数的 **三进制（Ternary）** 量化模型，仅用2-bit精度大幅缩减体积，代表了极限量化方向的最新探索。

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** | 作者：prism-ml | 点赞：444 | 下载：1,218,815
  - 同样是 27B 的 Bonsai，但进一步压缩到 **1-bit**，极端量化下仍在社区拥有百万级下载，说明“小型化”是硬需求。

- **[empero-ai/Qwythos-9B-v2-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-v2-GGUF)** | 作者：empero-ai | 点赞：169 | 下载：103,504
  - Qwythos 9B v2 的 GGUF 版本，是 Qwen3.5 家族的重要社区微调量化作品，下载量已破十万。

- **[unsloth/inkling-GGUF](https://huggingface.co/unsloth/inkling-GGUF)** | 作者：unsloth | 点赞：96 | 下载：6,461
  - 知名量化工具 Unsloth 对 Inkling 多模态模型进行 GGUF 量化，满足多模态模型在边缘设备部署需求。

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)** | 作者：GnLOLot | 点赞：277 | 下载：172,409
  - 1B 参数的 MiniCPM5 的 GGUF 量化版本，结合 Claude 蒸馏的推理能力，主打在低算力设备上实现“思考”模型。

---

### **生态信号**

1.  **Qwen家族与GLM/Gemma三分天下**：以 **Qwen3.5/3.6** 为基座的微调模型（Qwythos、HauhauCS变体、Agents-A1）占据了榜单的绝大多数席位，与 **GLM-5.2**、**Gemma-4** 形成三足鼎立之势。Qwen 因其开放的模型规模（从 1B 到 35B）和高频更新，已成为社区最活跃的“模型乐高”。

2.  **极端量化成为主流**：从 **Bonsai 的 1-bit/2-bit** 到 **Ternary 三进制**，量化技术已从“压缩”走向“重塑”。社区不再仅仅追求保留 95% 的性能，而是愿意在性能和部署效率之间进行更激进的取舍，以实现在消费级或移动设备上运行 27B 级大模型。

3.  **多模态走向专用与 Agent**：除了通用的图生文模型，出现了像 **Unlimited-OCR** 这样的“杀手级应用”模型，以及 **needle** 这样的 Agent 专用模型。这表明 AI 生态正从“大一统”模型向“基础模型 + 专用插件/工具”的架构演进。

---

### **值得探索**

- **推荐尝试：** **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)**
  - **理由**：作为 Google 最新开源的指令模型，它结合了顶尖的性能与相对较小的 31B 参数量。高达 1200 万的下载量证明了其卓越的实用性和社区支持度，是评估当前顶级开源基础能力的最好样本。

- **推荐研究：** **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)**
  - **理由**：三进制（Ternary）量化是模型压缩领域的前沿方向。该模型将 27B 参数压缩至 2-bit，探索了“超低比特”下的模型能力边界，对希望在嵌入式或移动端部署大模型的研究者和工程师极具参考价值。

- **推荐关注：** **[Wan-AI/Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)**
  - **理由**：视频生成是下一代 AIGC 的焦点。Wan-Dancer 专门针对“图像到视频”中的动态场景（如舞蹈）进行了优化，该领域的专业模型预示着 AI 视频生成正从“生成个动画”迈向“生成专业内容”的新阶段。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*