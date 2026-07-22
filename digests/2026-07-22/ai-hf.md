# Hugging Face 热门模型日报 2026-07-22

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-22 01:56 UTC

---

好的，没问题。作为 AI 模型生态分析师，这是为您生成的 2026-07-22 Hugging Face 热门模型日报。

---

### **Hugging Face 热门模型日报 | 2026-07-22**

#### **今日速览**

今日榜单呈现“巨头领跑、社区创新”的格局。Google 的 `gemma-4-31B-it` 凭借超千万下载量成为绝对焦点，而百度 `Unlimited-OCR` 则展示了传统技术巨头的实用模型功底。值得注意的是，以 `prism-ml` 和 `GnLOLot` 为代表的社区量化专家异常活跃，推出了多个 1-bit、2-bit 及 Ternary 量化的超低比特模型，推动模型压缩技术迈向新边界。此外，基于 `Qwen3.5/3.6` 指令微调和未审查（Uncensored）的社区模型占据了榜单相当比例，显示出社区生态的高度繁荣与迭代速度。

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

*   **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** | 作者: prism-ml | 👍 899 | ⬇️ 432,196
    *   一款基于 27B 模型的 2-bit Ternary 量化版本，旨在通过极端量化将大模型塞入消费级硬件，是社区研究模型压缩极限的代表。
*   **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** | 作者: zai-org | 👍 4,281 | ⬇️ 545,109
    *   智谱 AI 推出的 GLM 系列最新迭代，采用了 MoE (Mixture-of-Experts) 架构和 DSA 技术，在性能和效率上实现了平衡，是当前最受关注的开源中文大模型之一。
*   **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** | 作者: prism-ml | 👍 570 | ⬇️ 1,404,962
    *   与Ternary版本同系列的 1-bit 极致量化版本，下载量极高，表明社区对能够本地运行的大模型有强烈需求。
*   **[poolside/Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1)** | 作者: poolside | 👍 194 | ⬇️ 3,056
    *   这是一个由企业发布的代码生成模型，专注于软件工程领域的任务，代表了LLM在垂直行业的深化应用。
*   **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking)** | 作者: GnLOLot | 👍 166 | ⬇️ 6,165
    *   基于 MiniCPM5 的社区微调版本，融合了多个知名模型（如 Claude）的风格和思路，旨在提升小模型的思考能力。
*   **[AngelSlim/Hy3-GGUF](https://huggingface.co/AngelSlim/Hy3-GGUF)** | 作者: AngelSlim | 👍 156 | ⬇️ 145,102
    *   腾讯开源模型 `Hy3` 的 GGUF 量化版本，方便用户在 CPU 或低显存设备上本地运行，是社区快速跟进新模型的体现。
*   **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** | 作者: Nanbeige | 👍 77 | ⬇️ 0
    *   一个 3B 参数的小型语言模型，主打高效推理，适合资源受限场景或边缘部署。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

*   **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** | 作者: thinkingmachines | 👍 1,366 | ⬇️ 16,441
    *   一个原生多模态 MoE 模型，支持图像和文本输入，能够进行图像理解与对话，是多模态统一模型的优秀代表。
*   **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** | 作者: baidu | 👍 2,609 | ⬇️ 2,237,351
    *   百度推出的通用 OCR 模型，宣称能处理任意场景下的文字识别，其极高的下载量表明实用型多功能工具模型有巨大的市场。
*   **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** | 作者: HauhauCS | 👍 2,971 | ⬇️ 1,997,690
    *   基于 Qwen3.6 的 MoE 模型微调版本，主打“未审查”和“激进”风格，迎合了社区对模型自由度的高需求。
*   **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** | 作者: empero-ai | 👍 2,388 | ⬇️ 2,133,420
    *   一个经过大量数据微调的推理模型 GGUF 版本，它融合了 Claude 等模型的风格，在社区中非常受欢迎，下载量巨大。
*   **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** | 作者: moonshotai | 👍 1,200 | ⬇️ 722,058
    *   月之暗面推出的代码专用视觉语言模型，使用压缩张量技术，专门针对代码理解和生成优化，是“AI+编程”赛道的有力竞争者。
*   **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** | 作者: google | 👍 3,314 | ⬇️ 12,113,203
    *   谷歌开源的第四代 Gemma 系列旗舰模型，这是一个支持图像和文本输入的多模态对话模型。其下载量断层式领先，堪称本日“社区之王”。
*   **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** | 作者: Alissonerdx | 👍 222 | ⬇️ 0
    *   一个用于 `LTX-Video` 身份保持的 LoRA 模型，专注于从参考图像生成视频时保持人物面部一致性。
*   **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** | 作者: nvidia | 👍 903 | ⬇️ 590,230
    *   英伟达推出的流式语音识别模型，专为低延迟实时转录场景设计，是 AI 硬件的头部厂商在模型层的布局。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

*   **[nvidia/Nemotron-3-Embed-1B-BF16](https://huggingface.co/nvidia/Nemotron-3-Embed-1B-BF16)** | 作者: nvidia | 👍 96 | ⬇️ 93,021
    *   英伟达发布的 1B 参数通用文本嵌入模型，用于语义搜索、聚类等 RAG 应用，是构建 AI 应用基础设施的关键组件。
*   **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** | 作者: Cactus-Compute | 👍 298 | ⬇️ 1,068
    *   使用 JAX 框架构建的模型，专注于函数调用和工具使用，这一特性对于构建能与外部系统交互的 AI Agent 至关重要。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

*   **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** | 作者: DavidAU | 👍 249 | ⬇️ 62,842
    *   一个极具个性的社区微调模型，混合了多种模型风格，并进行了 GGUF 量化，反映了社区对模型个性化定制的热情。
*   **[unsloth/inkling-GGUF](https://huggingface.co/unsloth/inkling-GGUF)** | 作者: unsloth | 👍 116 | ⬇️ 7,377
    *   知名微调加速库 Unsloth 推出的 `Inkling` 模型 GGUF 量化版本，方便更多人便捷地使用这款多模态 MoE 模型。
*   **[prism-ml/Bonsai-27B-mlx-1bit](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)** | 作者: princi-ml | 👍 161 | ⬇️ 25,273
    *   为 Apple Silicon 优化的 MLX 框架下的 1-bit 模型，表明量化社区正在积极适配不同硬件平台。
*   **[prism-ml/Ternary-Bonsai-27B-mlx-2bit](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-mlx-2bit)** | 作者: princi-ml | 👍 135 | ⬇️ 20,445
    *   与上一条相似，此为 MLX 框架下的 2-bit Ternary 量化版本，展现了开发者对“Bonsai”系列模型进行多框架、多精度量化的系统化尝试。
*   **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF)** | 作者: GnLOLot | 👍 147 | ⬇️ 51,746
    *   同一位作者对同一款小模型的多次微调和量化迭代，展示了社区内对特定模型进行精细化打磨和快速迭代的工作流。

#### **生态信号**

本周榜单释放出强烈的**多模态与“小模型”** 双重信号。一方面，以 `Gemma-4-31B-it` 和 `Inkling` 为代表的原生多模态模型成为主流，`image-text-to-text` 任务占比极高，视觉语言融合已成标配。另一方面，模型量化活动空前繁荣，`prism-ml` 的“Bonsai”系列将 27B 模型量化至 1-bit 和 2-bit，标志着开源社区在**模型压缩技术上的又一次飞跃**，旨在让高端模型在个人设备上流畅运行。此外，基于 `Qwen3.6` 和 `MiniCPM5` 的大量社区微调版本（Uncensored、Thinking、风格融合等）表明，**基础模型能力已基本满足社区需求，现在焦点正在转向个性化、风格化**和针对特定能力的强化。开源权重模型已形成完整且极具活力的生态，从基础研究到社区二次开发再到终端部署的闭环日益成熟。

#### **值得探索**

1.  **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)**：作为本日下载量冠军，它代表了当前大模型性能的前沿，值得所有开发者上手体验其多模态对话能力，测试其与社区的融合程度。
2.  **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** 和 **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)**：这两款极致量化的模型是探索模型压缩极限的绝佳案例，值得研究其性能、推理速度与硬件需求的平衡点。
3.  **[poolside/Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1)**：作为专注于代码领域的商业模型，它是观察LLM在垂直行业应用趋势的窗口，可以将其与通用模型在编程任务上进行对比。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*