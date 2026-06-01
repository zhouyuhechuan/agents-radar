# Hugging Face 热门模型日报 2026-06-01

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-01 02:55 UTC

---

# Hugging Face 热门模型日报（2026-06-01）

## 今日速览

- **DeepSeek V4 系列登顶**：DeepSeek-V4-Pro 以 4,503 点赞遥遥领先，其 Flash 版本也进入前十，表明开源 MoE 大语言模型的关注度持续攀升。  
- **Qwen 3.6 生态爆发**：Qwen 3.6 系列（单模型、MoE、量化版）占据榜单近三分之一，社区微调版本（如 uncensored、GGUF、MTP）下载量惊人，多模态能力成为热点。  
- **多模态生成百花齐放**：视频生成（Sulphur-2、LongCat-Video-Avatar 1.5）、图像到图像（nvidia/PiD）、文本到语音（supertonic-3、MOSS-TTS）以及任意到任意模型（bytedance/Lance）密集发布，显示领域正在从纯文本向全模态融合。  
- **量化与边缘部署活跃**：GGUF 版本（LiquidAI、unsloth、Qwen）和 NVIDIA 的 NVFP4 量化方案上榜，表明社区对模型轻量化、本地推理的需求旺盛。

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  作者：deepseek-ai | 👍 4,503 | ⬇ 5,886,599  
  最新旗舰 MoE 模型，凭借极大参数规模与长上下文能力成为本周热度冠军，性能对标闭源竞品。  
- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)**  
  作者：deepseek-ai | 👍 1,323 | ⬇ 3,483,641  
  轻量化版 V4，保持高推理效率，适合大规模部署，下载量紧随 Pro 版本。  
- **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)**  
  作者：openbmb | 👍 661 | ⬇ 36,730  
  1B 参数的端侧大模型，高效小巧，适合移动设备与实时交互。  
- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)**  
  作者：LiquidAI | 👍 321 | ⬇ 27,677  
  Liquid 第二代 MoE 模型，8B 激活 1B 参数，平衡性能与速度。  
- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)**  
  作者：sapientinc | 👍 428 | ⬇ 143,904  
  专注人力资源管理领域的 1B 文本生成模型，针对招聘、面试等场景优化。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)**  
  作者：Qwen | 👍 1,552 | ⬇ 5,064,096  
  Qwen 3.6 系列最强多模态模型，26B 参数，支持图像、文本联合理解与生成。  
- **[openbmb/MiniCPM-V-4.6](https://huggingface.co/openbmb/MiniCPM-V-4.6)**  
  作者：openbmb | 👍 1,084 | ⬇ 444,679  
  轻量级多模态模型，延续 MiniCPM-V 路线，在视觉语言任务上表现优异。  
- **[bytedance-research/Lance](https://huggingface.co/bytedance-research/Lance)**  
  作者：bytedance-research | 👍 992 | ⬇ 2,948  
  字节跳动推出的“任意到任意”全模态模型，统一图像、视频、文本、音频生成。  
- **[Supertone/supertonic-3](https://huggingface.co/Supertone/supertonic-3)**  
  作者：Supertone | 👍 754 | ⬇ 56,472  
  新一代 TTS 模型，合成语音自然度极高，支持多风格控制。  
- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)**  
  作者：stepfun-ai | 👍 162 | ⬇ 7,638  
  阶跃星辰的轻量视觉语言模型，主打快速推理。  
- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)**  
  作者：SulphurAI | 👍 1,471 | ⬇ 1,590,236  
  开源文本到视频生成模型，支持长视频生成，下载量极高。  
- **[meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)**  
  作者：meituan-longcat | 👍 440 | ⬇ 0（发布初期）  
  美团出品，可根据音频+文本生成虚拟人物视频，面向数字人应用。  
- **[nvidia/PiD](https://huggingface.co/nvidia/PiD)**  
  作者：nvidia | 👍 220 | ⬇ 498  
  图像超分辨率扩散模型，基于像素级先验，细节修复出色。  
- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  作者：nvidia | 👍 619 | ⬇ 24,586  
  3B 参数的目标定位模型，可任意指定图像中物体并获取位置。  
- **[NemoStation/Marlin-2B](https://huggingface.co/NemoStation/Marlin-2B)**  
  作者：NemoStation | 👍 472 | ⬇ 16,277  
  视频文本到文本模型，专注视频内容理解与问答。  
- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)**  
  作者：PaddlePaddle | 👍 118 | ⬇ 2,731  
  结合 ERNIE 4.5 的视觉语言 OCR 模型，识别准确率行业领先。  
- **[numind/NuExtract3](https://huggingface.co/numind/NuExtract3)**  
  作者：numind | 👍 208 | ⬇ 57,248  
  图像到文本提取模型，用于文档结构化信息抽取。  
- **[microsoft/Lens](https://huggingface.co/microsoft/Lens)**  
  作者：microsoft | 👍 149 | ⬇ 1,959  
  微软文本到图像扩散模型，强调构图与语义对齐。  
- **[circlestone-labs/Anima](https://huggingface.co/circlestone-labs/Anima)**  
  作者：circlestone-labs | 👍 1,610 | ⬇ 756,861  
  ComfyUI 适配的扩散模型单文件，社区热捧，用于高质量图像生成。  
- **[OpenMOSS-Team/MOSS-TTS-v1.5](https://huggingface.co/OpenMOSS-Team/MOSS-TTS-v1.5)**  
  作者：OpenMOSS-Team | 👍 83 | ⬇ 14,272  
  中文 TTS 模型，支持延迟感知的语音合成。

### 🔧 专用模型（代码、数学、医疗、翻译、隐私、工具）

- **[tencent/Hy-MT2-30B-A3B](https://huggingface.co/tencent/Hy-MT2-30B-A3B)**  
  作者：tencent | 👍 440 | ⬇ 4,226  
  腾讯翻译大模型，30B 参数 MoE 结构，支持多语种高精度翻译。  
- **[tencent/Hy-MT2-1.8B](https://huggingface.co/tencent/Hy-MT2-1.8B)**  
  作者：tencent | 👍 1,094 | ⬇ 17,471  
  轻量版翻译模型，1.8B 密集参数，适合低资源部署。  
- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)**  
  作者：openai | 👍 1,573 | ⬇ 306,344  
  隐私信息过滤模型，基于 token 分类，用于文本去敏感化。  
- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)**  
  作者：froggeric | 👍 469 | ⬇ 0（模板资产）  
  修复 Qwen 3.5 系列聊天模板的社区工具，提升兼容性。

### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[HauhauCS/Qwen3.6-

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*