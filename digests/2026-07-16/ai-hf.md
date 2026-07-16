# Hugging Face 热门模型日报 2026-07-16

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-16 01:55 UTC

---

# Hugging Face 热门模型日报（2026-07-16）

## 今日速览

本周 Hugging Face 上 GLM-5.2（zai-org）以 4,000 点赞登顶热度榜首，标志着国内大模型在 MoE 架构上的新突破。Qwen3.6 系列多模态模型（如 ThinkingCap、Uncensored 变体）及大量 GGUF 量化版持续霸榜下载量，社区对本地部署和极端量化的需求依然强劲。baidu 推出的 Unlimited-OCR 模型凭借 2,002 点赞和 170 万下载量成为本周 OCR 领域的明星。此外，函数调用专用模型 `needle` 和 agentic 微调版本 `gemma-4-12B` 也显示出工具使用与智能体方向的升温。

---

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**  
  作者: zai-org | 👍 4,000 | 📥 489,611  
  基于 MoE-DSA 架构的 52B 级对话模型，点赞量本周最高，代表国产大规模 MoE 的快速迭代。

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)**  
  作者: tencent | 👍 800 | 📥 10,406  
  腾讯 Hunyuan 系列第三代文本生成模型，官方发布即获社区广泛关注。

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking)**  
  作者: GnLOLot | 👍 129 | 📥 3,483  
  基于 MiniCPM5 的 1B 参数思考型对话模型，融合 Claude 风格微调，小参数高性能的代表。

- **[nvidia/Nemotron-Labs-Audex-30B-A3B](https://huggingface.co/nvidia/Nemotron-Labs-Audex-30B-A3B)**  
  作者: nvidia | 👍 156 | 📥 1,332  
  NVIDIA 推出的 30B 级 MoE 语言模型（3B 激活），专注于实验室场景的音频理解与生成。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)**  
  作者: thinkingmachines | 👍 365 | 📥 0  
  统一图像与音频输入的多模态对话模型，探索“视+听”交互新范式。

- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)**  
  作者: bottlecapai | 👍 366 | 📥 6,208  
  Qwen3.6 的 27B 多模态思考模型，结合 Chain-of-Thought 提升图文理解能力。

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)**  
  作者: InternScience | 👍 556 | 📥 30,539  
  基于 Qwen3.5 MoE 的多模态 Agent 模型，专为工具调用与视觉交互设计。

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)**  
  作者: OpenMOSS-Team | 👍 215 | 📥 65,109  
  语音转录 + 说话人分离的端到端模型，开源语音 LLM 的重要进展。

- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)**  
  作者: conradlocke | 👍 307 | 📥 0  
  基于 Krea-2 的身份保留图像编辑 LoRA，支持人物面部一致性编辑。

- **[robbyant/lingbot-world-v2-14b-causal-fast](https://huggingface.co/robbyant/lingbot-world-v2-14b-causal-fast)**  
  作者: robbyant | 👍 99 | 📥 0  
  世界模型风格图像到视频生成模型，因果预训练加速推理。

- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)**  
  作者: Alissonerdx | 👍 154 | 📥 0  
  LTX 视频生成的身份保留 LoRA，参考图像驱动视频人物一致性。

- **[mgwr/M87](https://huggingface.co/mgwr/M87)**  
  作者: mgwr | 👍 126 | 📥 2,408  
  基于 Krea-2 Turbo 的文本到图像 LoRA，专注于高质量图像风格生成。

- **[robbyant/lingbot-video-moe-30b-a3b](https://huggingface.co/robbyant/lingbot-video-moe-30b-a3b)**  
  作者: robbyant | 👍 111 | 📥 700  
  30B MoE 视频生成模型（3B 激活），高效视频扩散新架构。

- **[open-gigaai/Giga

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*