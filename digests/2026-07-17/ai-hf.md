# Hugging Face 热门模型日报 2026-07-17

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-17 01:59 UTC

---

好的，作为AI模型生态分析师，以下是基于2026年7月17日数据生成的《Hugging Face 热门模型日报》。

---

### Hugging Face 热门模型日报 (2026-07-17)

#### **今日速览**

本周 Hugging Face 榜单呈现“多模态与极致量化”双轮驱动的景象。**zai-org/GLM-5.2** 拿下周点赞榜首，标志着国产MoE架构模型在社区中的号召力。值得注意的是，**empero-ai** 家族的 **Qwythos-9B** 系列和 **HauhauCS** 的 **Qwen3.6** 魔改版凭借海量下载量，显示出社区对于“视觉+推理”模型的巨大渴求。最核心的趋势是 **1-bit/2-bit 量化技术**大爆发，以 **prism-ml** 的 Bonsai 系列为首，将大模型的门槛降至个人设备可运行的水平。此外，**Baidu** 开源的 **Unlimited-OCR** 也成为本周黑马，证明了垂直领域专用模型的强劲潜力。

#### **热门模型**

##### 🧠 语言模型

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** (zai-org · 点赞: 4,029 · 下载: 513k) — 智谱开源的 MoE-DSA 架构顶尖模型，凭借强大的原生推理能力成为本周社区最受关注的模型。
- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** (deepreinforce-ai · 点赞: 902 · 下载: 1.79M) — 具备工业级工具调用能力的高性能35B模型量化版，因其强大的通用性和高下载量备受瞩目。
- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** (prism-ml · 点赞: 341 · 下载: 559k) — 革命性的**1-bit 量化模型**，通过将模型精度压至极低水平，使得27B参数模型能在 CPU 上流畅运行。

##### 🎨 多模态与生成

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** (HauhauCS · 点赞: 2,787 · 下载: 2.33M) — 本周下载量冠军。基于 Qwen3.6 的 MoE 模型，主打“无审查+激进风格”的视觉对话，社区热度极高。
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** (empero-ai · 点赞: 2,237 · 下载: 2.04M) — 将 Claude 多模态风格与 Qwen3.5 推理能力融合的明星模型，其长上下文和优秀的多模态理解能力导致下载量激增。
- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** (tencent · 点赞: 813 · 下载: 12k) — 腾讯发布的 Hunyuan 系列最新文本生成模型，作为国内大厂的最新力作备受关注。
- **[Wan-AI/Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)** (Wan-AI · 点赞: 92 · 下载: 2k) — 图像到视频生成模型，专注于舞蹈动作生成，代表了视频生成领域专业化的新方向。

##### 🔧 专用模型

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** (baidu · 点赞: 2,010 · 下载: 1.85M) — 百度开源的通用 OCR 模型，凭借接近商用的识别率和对复杂场景的卓越处理能力，成为本周最大的黑马之一。
- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** (ATH-MaaS · 点赞: 136 · 下载: 3.7k) — 专注于视觉文档理解与 OCR 的多模态模型，配合 Qwen3.5 架构扩展了文档处理能力。
- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** (yuxinlu1 · 点赞: 1,208 · 下载: 506k) — 基于 Gemma-4 的 Agent 微调版，在编程和终端操作上表现出色，是 Agent 模型中的热门之选。

##### 📦 微调与量化

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** (prism-ml · 点赞: 607 · 下载: 74k) — 采用**三元量化（Ternary，-1,0,1）** 的代表作，以极致的 2-bit 精度实现高效率部署，引领了超低比特量化浪潮。
- **[unsloth/Qwen3.6-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.6-27B-NVFP4)** (unsloth · 点赞: 216 · 下载: 1.71M) — 来自知名优化工具 unsloth 的 4-bit 量化版，专为 NVIDIA FP4 硬件加速设计，兼顾速度与内存效率。
- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)** (GnLOLot · 点赞: 264 · 下载: 121k) — 将 Claude 思维链能力蒸馏到 MiniCPM5 的 1B 小模型，体现了“大模型知识蒸馏”与“小模型 + 量化”的热门玩法。
- **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** (Cactus-Compute · 点赞: 248 · 下载: 733) — 基于 JAX 框架的函数调用专用模型，代表了用于 Agent 和工具使用的轻量级模型研究趋势。

#### **生态信号**

1.  **“Qwen”生态与“GLM”生态对决**：本周榜单几乎被 **Qwen3.5/3.6** 及其衍生模型（如 Qwythos、多种量化版）和 **GLM-5** 系列主导。这表明头部开源模型生态已形成寡头格局，社区开发者更倾向于在最好的“基底模型”上进行微调和优化。
2.  **量化竞赛进入“比特时代”**：**1-bit 和 Ternary（三元）量化**技术的成熟是本周期最显著的信号。`prism-ml` 的 Bonsai 系列证明了通过牺牲部分精度换取在个人笔记本、甚至手机芯片上运行大模型的可能性。这预示着 AI 推理将进一步去中心化。
3.  **“视觉+推理”成为标配**：无论是点赞第一的 GLM-5.2 还是下载量巨大的 Qwythos-9B，**image-text-to-text** 任务几乎覆盖了榜单一半的模型。多模态不再是附加功能，而是下一代基础模型的标配特征。

#### **值得探索**

1.  **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**：作为本周点赞王，值得深入体验其 MoE-DSA 架构在复杂推理和多轮对话上的表现，它是当前国产最强开源模型的代表。
2.  **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)**：如果你对在非专业显卡或 Apple Silicon Mac 上运行大模型感兴趣，这个三元量化模型是当前的首选技术实验品，体现了未来 AI 端侧部署的前沿方向。
3.  **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**：作为下载冠军，它展示了社区对特定“个性风格”微调模型的需求。研究其训练数据和方法，对于理解如何塑造模型的行为和价值观有重要参考价值。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*