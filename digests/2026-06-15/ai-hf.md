# Hugging Face 热门模型日报 2026-06-15

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-15 02:59 UTC

---

# Hugging Face 热门模型日报 — 2026-06-15

## 今日速览

DeepSeek-V4-Pro 凭借 **4,835 点赞** 领跑本周榜单，再次证明开源大语言模型社区的强劲活力。多模态模型继续主导热门趋势，尤其是 **Gemma-4 家族**（官方版与社区微调/量化版共 7 款上榜）和 **Qwen3.6 系列微调变体**（4 款）。英伟达 **LocateAnything-3B** 以 2,005 点赞成为定位类模型的亮点。社区量化活动持续活跃，unsloth 提供的多款 GGUF 版本下载量极高，反映出用户对本地部署的强烈需求。此外，Ideogram-4 图像生成模型及 Boson AI 的 TTS 模型也受到关注。

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  作者: deepseek-ai | 点赞: 4,835 | 下载: 3,075,369  
  本周热度最高的文本生成模型，DeepSeek 最新旗舰，兼具强推理与对话能力。

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**  
  作者: google | 点赞: 1,009 | 下载: 1,084,405  
  Google 官方指令微调版 Gemma-4 12B，支持 any-to-any 多模态，但核心仍为强大的语言能力。

- **[google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B)**  
  作者: google | 点赞: 544 | 下载: 213,502  
  Gemma-4 12B 基座模型，any-to-any 架构，为后续微调和多模态应用提供基础。

- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)**  
  作者: nex-agi | 点赞: 260 | 下载: 3,396  
  基于 Qwen3.5 MoE 架构的先进文本生成模型，侧重性能与效率平衡。

- **[nex-agi/Nex-N2-mini](https://huggingface.co/nex-agi/Nex-N2-mini)**  
  作者: nex-agi | 点赞: 211 | 下载: 7,010  
  Nex-N2 系列轻量版，适合资源受限场景。

- **[silx-ai/Quasar-Preview](https://huggingface.co/silx-ai/Quasar-Preview)**  
  作者: silx-ai | 点赞: 74 | 下载: 307  
  Silx AI 推出的新型文本生成模型预览版，主打长上下文处理。

- **[XiaomiMiMo/MiMo-V2.5-Pro-FP4-DFlash](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro-FP4-DFlash)**  
  作者: XiaomiMiMo | 点赞: 114 | 下载: 4,108  
  小米推出的 MoE 文本生成模型，支持 agent 能力，FP4 量化降低部署门槛。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  作者: nvidia | 点赞: 2,005 | 下载: 75,201  
  英伟达推出的 3B 参数定位模型，可基于图像与文本描述定位任意物体，高赞背后是极强的实用价值。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  作者: HauhauCS | 点赞: 1,808 | 下载: 2,516,709  
  基于 Qwen3.6 的 35B MoE 无审查微调版，下载量突破 250 万，社区对“脱缰”模型的热情可见一斑。

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**  
  作者: google | 点赞: 801 | 下载: 198,912  
  Google 扩散+Gemma 架构的多模态对话模型，26B 总参/4B 激活，兼顾图像理解与生成。

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**  
  作者: moonshotai | 点赞: 637 | 下载: 15,145  
  月之暗面推出的代码增强多模态模型，支持图像特征提取与代码理解。

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)**  
  作者: MiniMaxAI | 点赞: 500 | 下载: 6,643  
  MiniMax 第三代多模态大模型，覆盖视觉语言理解与生成。

- **[prefeitura-rio/Rio-3.5-Open-397B](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B)**  
  作者: prefeitura-rio | 点赞: 276 | 下载: 112,371  
  397B 超大 MoE 模型，开源的多模态对话系统，下载量可观。

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)**  
  作者: bosonai | 点赞: 427 | 下载: 35,122  
  Boson AI 的 4B TTS 模型，基于多模态 Qwen3 架构，语音合成质量高。

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)**  
  作者: ideogram-ai | 点赞: 535 | 下载: 8,263  
  Ideogram 第四代文生图模型 FP8 版，保持高质量的同时降低显存需求。

- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)**  
  作者: ideogram-ai | 点赞: 337 | 下载: 3,763  
  Ideogram-4 的 NF4 量化版，进一步压缩模型体积。

- **[Comfy-Org/Ideogram-4](https://huggingface.co/Comfy-Org/Ideogram-4)**  
  作者: Comfy-Org | 点赞: 150 | 下载: 0  
  专为 ComfyUI 工作流打包的 Ideogram-4 集成包，便于流程化使用。

- **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)**  
  作者: zai-org | 点赞: 175 | 下载: 0  
  图像到视频生成模型，基于扩散模型与姿态驱动角色动画，新赛道探索者。

- **[DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF)**  
  作者: DavidAU | 点赞: 339 | 下载: 375,966  
  社区深度微调的无审查多模态模型，集成多种技术，下载量极高。

- **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)**  
  作者: Jackrong | 点赞: 184 | 下载: 33,720  
  基于 Qwen3.6 的 27B 代码增强多模态模型 GGUF 版，支持推理和图像理解。

- **[Jackrong/Qwopus3.6-27B-v2-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-MTP-GGUF)**  
  作者: Jackrong | 点赞: 303 | 下载: 175,472  
  同一系列的 v2 版本，优化了推理能力和视觉理解质量。

### 🔧 专用模型（代码、数学、ASR、定位等）

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)**  
  作者: CohereLabs | 点赞: 369 | 下载: 9,932  
  Cohere 推出的轻量代码生成模型，基于 MoE 架构，专攻编程任务。

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**  
  作者: nvidia | 点赞: 412 | 下载: 4,505  
  英伟达的流式语音识别模型（0.6B），支持缓存感知的实时 ASR，低延迟部署。

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**  
  作者: yuxinlu1 | 点赞: 180 | 下载: 6,219  
  社区基于 Gemma-4 微调的代码专用模型 GGUF 版，侧重推理与代码生成。

### 📦 微调与量化（社区微调、GGUF、AWQ等）

- **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)**  
  作者: unsloth | 点赞: 262 | 下载: 80,118  
  DiffusionGemma 的 GGUF 量化版，方便在 llama.cpp 等本地推理工具中使用。

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)**  
  作者: unsloth | 点赞: 598 | 下载: 926,372  
  Gemma-4-12B-it 的 GGUF 版本，下载量接近百万，社区最受欢迎的量化方案之一。

- **[unsloth/gemma-4-12B-it-qat-GGUF](https://huggingface.co/unsl

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*