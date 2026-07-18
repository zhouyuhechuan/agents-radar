# Hugging Face 热门模型日报 2026-07-18

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-18 01:49 UTC

---

好的，作为AI模型生态分析师，以下是为您整理的2026年7月18日Hugging Face热门模型日报。

---

## 📰 Hugging Face 热门模型日报 (2026-07-18)

### **今日速览**

本周Hugging Face平台呈现出显著的 **“轻量化与多模态”** 双轮驱动趋势。一方面，以 `prism-ml` 的 **Bonsai** 系列为代表的极端量化模型（1-bit,2-bit）凭借巨大的下载量，表明社区对端侧部署和极致效率的强烈需求。另一方面，`zai-org` 的 **GLM-5.2** 和 `bottlecapai` 的 **ThinkingCap** 等大型MoE模型获得了极高的关注度，显示了前沿研究对稀疏激活架构的持续探索。此外，**Qwen3.5/3.6** 架构已成为社区微调和部署的绝对主力，大量衍生模型涌现，生态地位稳固。最后，以 `baidu` 的 **Unlimited-OCR** 为代表的专用多模态模型也表现出强劲势头，应用导向的模型吸引力不减。

---

### **热门模型**

#### 🧠 **语言模型 (LLMs, 对话模型)**

*   **`zai-org/GLM-5.2`** ([链接](https://huggingface.co/zai-org/GLM-5.2))
    *   **作者**: zai-org | **点赞**: 4,071 | **下载**: 534,698
    *   **一句话说明**: 基于MoE-DSA架构的顶尖大型语言模型，以最高点赞数领跑，代表了当前开源LLM的前沿研究水平。
*   **`prism-ml/Bonsai-27B-gguf`** ([链接](https://huggingface.co/prism-ml/Bonsai-27B-gguf))
    *   **作者**: prism-ml | **点赞**: 396 | **下载**: 1,045,182
    *   **一句话说明**: **1-bit** 极量化的27B模型，下载量巨大，展示了社区对可在消费级硬件上运行的高性能模型的狂热需求。
*   **`prism-ml/Ternary-Bonsai-27B-gguf`** ([链接](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf))
    *   **作者**: prism-ml | **点赞**: 680 | **下载**: 200,774
    *   **一句话说明**: Bonsai系列的三元量化版本（2-bit），在压缩率与性能之间取得平衡，是轻量化部署的热门选择。
*   **`tencent/Hy3`** ([链接](https://huggingface.co/tencent/Hy3))
    *   **作者**: tencent | **点赞**: 820 | **下载**: 12,719
    *   **一句话说明**: 腾讯出品的Hunyuan系列第三代大模型，成为本周热门的基座模型，其GGUF版本也迅速跟进。

#### 🎨 **多模态与生成 (图像/视频/音频/OCR)**

*   **`empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF`** ([链接](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF))
    *   **作者**: empero-ai | **点赞**: 2,274 | **下载**: 2,096,147
    *   **一句话说明**: 基于Qwen3.5的9B多模态模型量化版，融合了Claude风格的数据，以惊人的下载量成为本周最受欢迎的量化多模态模型之一。
*   **`baidu/Unlimited-OCR`** ([链接](https://huggingface.co/baidu/Unlimited-OCR))
    *   **作者**: baidu | **点赞**: 2,019 | **下载**: 1,992,355
    *   **一句话说明**: 百度推出的通用OCR模型，凭借其“无限制”的识别能力和强大的性能，在特定任务上获得了社区的广泛认可。
*   **`HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive`** ([链接](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive))
    *   **作者**: HauhauCS | **点赞**: 2,828 | **下载**: 2,295,313
    *   **一句话说明**: 基于Qwen3.6的35B MoE视觉模型，在无审查和激进风格上进行了定制，社区参与度极高，下载量上榜第一。
*   **`Wan-AI/Wan-Dancer-14B`** ([链接](https://huggingface.co/Wan-AI/Wan-Dancer-14B))
    *   **作者**: Wan-AI | **点赞**: 108 | **下载**: 2,185
    *   **一句话说明**: 专为舞蹈动作生成的图像到视频模型，代表了AI在创意视频领域应用的细分化趋势。

#### 🔧 **专用模型 (工具调用/编辑)**

*   **`Cactus-Compute/needle`** ([链接](https://huggingface.co/Cactus-Compute/needle))
    *   **作者**: Cactus-Compute | **点赞**: 257 | **下载**: 874
    *   **一句话说明**: 一个专注于函数调用和工具使用的JAX模型，在Agent和自动化应用兴起背景下，其针对性设计使其具有独特价值。
*   **`froggeric/Qwen-Fixed-Chat-Templates`** ([链接](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates))
    *   **作者**: froggeric | **点赞**: 934 | **下载**: 0
    *   **一句话说明**: 一个非模型文件，而是提供了修正后的Qwen对话模板，这反映了社区对标准化和易用性基础设施工具的渴求。

#### 📦 **微调与量化 (GGUF/社区版)**

*   **`unsloth/Qwen3.6-27B-NVFP4`** ([链接](https://huggingface.co/unsloth/Qwen3.6-27B-NVFP4))
    *   **作者**: unsloth | **点赞**: 225 | **下载**: 1,924,495
    *   **一句话说明**: unsloth出品的高效量化版本，采用NVFP4精度，在高下载量的同时，代表了针对特定硬件优化的量化方向。
*   **`AngelSlim/Hy3-GGUF`** ([链接](https://huggingface.co/AngelSlim/Hy3-GGUF))
    *   **作者**: AngelSlim | **点赞**: 122 | **下载**: 84,834
    *   **一句话说明**: `tencent/Hy3` 基座模型的GGUF社区量化版，迅速满足了社区对本地部署该模型的需求。
*   **`GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF`** ([链接](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF))
    *   **作者**: GnLOLot | **点赞**: 273 | **下载**: 154,762
    *   **一句话说明**: 对1B级小型模型进行“思考”能力的微调并量化，展示了在小模型上注入复杂推理能力的尝试，这类模型在社区中颇具热度。

---

### **生态信号**

*   **Qwen生态一枝独秀**：从榜单看，几乎一半的热门模型（如Qwythos、HauhauCS、ThinkingCap）都基于 **Qwen3.5 / Qwen3.6** 架构。这表明Qwen系列已成为社区微调、量化和再创作的“新基建”，生态垄断地位初现。
*   **极端量化成为主流**：`prism-ml` 的Bonsai系列（1-bit, 2-bit）及其衍生产品总下载量超过百万，标志着社区对“能跑起来”的模型的渴求远超对极致性能的追求。三元量化（ternary）技术是本周的一个亮点。
*   **开源权重模型的“军备竞赛”**：`zai-org/GLM-5.2` 和 `tencent/Hy3` 代表着大厂和顶尖实验室开源完整权重模型的持续投入。与之对应的是，社区微调和量化版本（如`unsloth`, `AngelSlim`）迅速跟进，形成了一个快速响应的生态循环。
*   **“思考”与“视觉”是两大微调热点**：无论是大型模型（如ThinkingCap）还是小型模型（如MiniCPM5-...-Thinking），赋予模型更强的“思考/推理”能力是社区微调的核心方向。同时，图像/视频生成、OCR等视觉模型热度不减，工具调用（如needle）也成为一个新兴的增长点。

---

### **值得探索**

1.  **`thinkingmachines/Inkling`** ([链接](https://huggingface.co/thinkingmachines/Inkling))：作为本周点赞数第一的“纯”多模态模型，它很可能代表了一种新的原生多模态架构。强烈建议 研究其模型结构和多模态交互方式，这可能是未来趋势的风向标。

2.  **`prism-ml/Bonsai-27B-gguf`** ([链接](https://huggingface.co/prism-ml/Bonsai-27B-gguf))：作为1-bit量化的巅峰之作，它是验证“极致压缩”与“实用性能”平衡点的最佳样本。如果你对边缘计算或个人设备上运行大模型感兴趣，这个模型是必试之选。

3.  **`Cactus-Compute/needle`** ([链接](https://huggingface.co/Cactus-Compute/needle))：在Agent和AI工具使用日益重要的今天，这是一个值得深入研究的专项模型。了解它在JAX框架下的函数调用能力，可能为构建更可靠的AI应用提供新思路。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*