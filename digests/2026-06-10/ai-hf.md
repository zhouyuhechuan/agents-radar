# Hugging Face 热门模型日报 2026-06-10

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-10 02:43 UTC

---

# Hugging Face 热门模型日报（2026-06-10）

## 📰 今日速览

- **DeepSeek-V4-Pro 以 4,740 周点赞登顶**，下载突破 430 万，成为当前最受关注的开源语言模型，延续 DeepSeek 家族的高人气。
- **Google Gemma-4 系列全面爆发**：基础版、指令版、量化版（GGUF）以及社区微调版（如 OBLITERATUS 的 “OBLITERATED” 版本）占据多个席位，多模态（any-to-any）能力成为最大亮点。
- **NVIDIA 多款模型上榜**，包括定位模型 LocateAnything-3B、流式语音识别 Nemotron-3.5-ASR、超大 MoE 模型 Nemotron-3-Ultra-550B，展示其在多模态和基础设施层的主导地位。
- **量化与社区微调活跃**：Unsloth 为 Gemma-4 提供了多个 GGUF/QAT 版本，下载量极高；Ideogram-4 发布 FP8/NF4 量化版，推动图像生成模型在消费级硬件上运行。
- **多模态生成全面开花**：图像、视频、音频、语音到文本、文本到视频（ByteDance Bernini-R、JD JoyAI-Echo）等方向均有新模型发布，多模态融合趋势明显。

---

## 🔥 热门模型分类

### 🧠 语言模型（LLM、对话、指令微调）

1. **deepseek-ai/DeepSeek-V4-Pro**  
   [→ HF链接](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)  
   👤 deepseek-ai | 👍 4,740 | ⬇️ 4,302,553  
   💡 **最强开源对话模型**，DeepSeek-V4 专业版，延续 MoE 高效架构，在推理、编码和通用对话上表现突出，本周绝对热度第一。

2. **nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16**  
   [→ HF链接](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)  
   👤 nvidia | 👍 175 | ⬇️ 56,864  
   💡 **超级 MoE 语言模型**，550B 参数但仅激活 55B，NVIDIA 企业级推理旗舰，BF16 权重发布。

3. **nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4**  
   [→ HF链接](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)  
   👤 nvidia | 👍 153 | ⬇️ 71,818  
   💡 **同一模型的 NVFP4 量化版**，进一步降低显存需求，适配高吞吐部署。

4. **sapientinc/HRM-Text-1B**  
   [→ HF链接](https://huggingface.co/sapientinc/HRM-Text-1B)  
   👤 sapientinc | 👍 734 | ⬇️ 133,351  
   💡 **人力资源管理专用文本模型**，1B 参数，面向 HR 场景的指令微调模型，下载量高显示垂直领域需求强劲。

5. **LiquidAI/LFM2.5-8B-A1B**  
   [→ HF链接](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)  
   👤 LiquidAI | 👍 572 | ⬇️ 137,138  
   💡 **Liquid 基础模型家族 2.5 版**，8B 参数仅激活 1B（MoE），效率与性能兼顾，社区认可度高。

6. **JetBrains/Mellum2-12B-A2.5B-Thinking**  
   [→ HF链接](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)  
   👤 JetBrains | 👍 273 | ⬇️ 17,571  
   💡 **JetBrains 推出的推理增强对话模型**，12B 参数 MoE（激活 2.5B），强调“思考”能力，适合编程助手。

7. **CohereLabs/North-Mini-Code-1.0**  
   [→ HF链接](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)  
   👤 CohereLabs | 👍 163 | ⬇️ 1,784  
   💡 **Cohere 北系列代码模型 Mini 版**，专为代码生成和编程对话设计，轻量高效。

8. **OBLITERATUS/Gemma-4-12B-OBLITERATED**  
   [→ HF链接](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)  
   👤 OBLITERATUS | 👍 143 | ⬇️ 8,106  
   💡 **社区微调版 Gemma-4**，去除安全限制的“解放版”，引发讨论与下载热度。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

1. **google/gemma-4-12B-it**  
   [→ HF链接](https://huggingface.co/google/gemma-4-12B-it)  
   👤 google | 👍 817 | ⬇️ 581,354  
   💡 **Gemma-4 指令版多模态模型**，支持任意输入到任意输出（any-to-any），文本、图像、音频兼可，生态核心。

2. **google/gemma-4-12B**  
   [→ HF链接](https://huggingface.co/google/gemma-4-12B)  
   👤 google | 👍 480 | ⬇️ 122,464  
   💡 **Gemma-4 基础版**，无指令微调，适合开发者进一步训练或集成。

3. **nvidia/LocateAnything-3B**  
   [→ HF链接](https://huggingface.co/nvidia/LocateAnything-3B)  
   👤 nvidia | 👍 1,733 | ⬇️ 123,922  
   💡 **通用目标定位模型**，输入图像+文本描述即可输出目标位置，3B 参数，本周点赞第二高。

4. **ideogram-ai/ideogram-4-fp8**  
   [→ HF链接](https://huggingface.co/ideogram-ai/ideogram-4-fp8)  
   👤 ideogram-ai | 👍 442 | ⬇️ 5,915  
   💡 **Ideogram-4 图像生成模型 FP8 量化版**，节省显存，适合消费者级 GPU 生成高质量图片。

5. **ideogram-ai/ideogram-4-nf4**  
   [→ HF链接](https://huggingface.co/ideogram-ai/ideogram-4-nf4)  
   👤 ideogram-ai | 👍 288 | ⬇️ 5,250  
   💡 **Ideogram-4 NF4 量化版**，更极致的低精度部署方案。

6. **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**  
   [→ HF链接](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)  
   👤 HauhauCS | 👍 1,596 | ⬇️ 2,983,909  
   💡 **Qwen3.6 超大 MoE 视觉语言模型**，35B 参数仅激活 3B，去审查“激进”版，下载量近 300 万。

7. **stepfun-ai/Step-3.7-Flash**  
   [→ HF链接](https://huggingface.co/stepfun-ai/Step-3.7-Flash)  
   👤 stepfun-ai | 👍 359 | ⬇️ 46,729  
   💡 **阶跃星辰最新视觉语言模型**，轻量高效，擅长图文理解与对话。

8. **nex-agi/Nex-N2-Pro**  
   [→ HF链接](https://huggingface.co/nex-agi/Nex-N2-Pro)  
   👤 nex-agi | 👍 162 | ⬇️ 783  
   💡 **Nex 系列多模态 MoE 模型**，支持图文输入，侧重对话生成。

9. **nex-agi/Nex-N2-mini**  
   [→ HF链接](https://huggingface.co/nex-agi/Nex-N2-mini)  
   👤 nex-agi | 👍 111 | ⬇️ 748  
   💡 **Nex-N2 迷你版**，轻量化多模态模型，适合边缘部署。

10. **ByteDance/Bernini-R**  
    [→ HF链接](https://huggingface.co/ByteDance/Bernini-R)  
    👤 ByteDance | 👍 196 | ⬇️ 281  
    💡 **字节跳动文本到视频生成模型**，支持根据描述生成视频，同步 arXiv 论文，学术与工程结合。

11. **jdopensource/JoyAI-Echo**  
    [→ HF链接](https://huggingface.co/jdopensource/JoyAI-Echo)  
    👤 jdopensource | 👍 115 | ⬇️ 4,502  
    💡 **京东开源文本/音频到视频模型**，融合音频和视频生成，创新方向。

12. **google/magenta-realtime-2**  
    [→ HF链接](https://huggingface.co/google/magenta-realtime-2)  
    👤 google | 👍 164 | ⬇️ 18,216  
    💡 **实时文本到音乐/音频生成**，Magenta 项目第二代，支持 TFLite，可边输入边播放。

13. **nvidia/Cosmos3-Nano**  
    [→ HF链接](https://huggingface.co/nvidia/Cosmos3-Nano)  
    👤 nvidia | 👍 214 | ⬇️ 36,739  
    💡 **NVIDIA Cosmos 世界模型 Nano 版**，支持全模态（omni），用于机器人/自动驾驶等物理世界理解。

14. **PaddlePaddle/PaddleOCR-VL-1.6**  
    [→ HF链接](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)  
    👤 PaddlePaddle | 👍 281 | ⬇️ 10,139  
    💡 **视觉语言 OCR 模型**，基于 ERNIE 4.5，端到端图文识别，适用于文档分析。

### 🔧 专用模型（语音、代码、医疗、检索等）

1. **nvidia/nemotron-3.5-asr-streaming-0.6b**  
   [→ HF链接](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)  
   👤 nvidia | 👍 321 | ⬇️ 4,181  
   💡 **流式自动语音识别模型**，0.6B 参数，支持缓存感知推理，适合实时语音转写。

2. **bosonai/higgs-audio-v3-tts-4b**  
   [→ HF链接](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)  
   👤 bosonai | 👍 285 | ⬇️ 16,207  
   💡 **Higgs 第三代语音合成模型**，4B 参数，基于 Qwen 架构，支持文本到语音生成。

3. **MisoLabs/MisoTTS**  
   [→ HF链接](https://huggingface.co/MisoLabs/MisoTTS)  
   👤 MisoLabs | 👍 175 | ⬇️ 0  
   💡 **全新文本到语音模型**，尚未有下载量但获大量点赞，说明社区期待度高。

4. **Comfy-Org/Ideogram-4**  
   [→ HF链接](https://huggingface.co/Comfy-Org/Ideogram-4)  
   👤 Comfy-Org | 👍 113 | ⬇️ 0  
   💡 **ComfyUI 对 Ideogram-4 的封装集成**，方便现有工作流调用，暂无下载数但热度迅速攀升。

### 📦 微调与量化（GGUF、FP8、NF4、社区版）

1. **unsloth/gemma-4-12b-it-GGUF**  
   [→ HF链接](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)  
   👤 unsloth | 👍 532 | ⬇️ 660,140  
   💡 **Gemma-4 指令版 GGUF 量化**，Unsloth 出品，下载量超 66 万，是部署到 llama.cpp 等本地推理的首选。

2. **unsloth/gemma-4-12B-it-qat-GGUF**  
   [→ HF链接](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF)  
   👤 unsloth | 👍 172 | ⬇️ 127,332  
   💡 **采用量化感知训练（QAT）的 GGUF 版本**，推理精度更优，适合高质量本地部署。

3. **unsloth/gemma-4-26B-A4B-it-qat-GGUF**  
   [→ HF链接](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)  
   👤 unsloth | 👍 115 | ⬇️ 96,059  
   💡 **Gemma-4 更大尺寸（26B 激活 4B）的 QAT GGUF**，提供高参数量下的本地化推理。

4. **google/gemma-4-12B-it-qat-q4_0-gguf**  
   [→ HF链接](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf)  
   👤 google | 👍 115 | ⬇️ 63,049  
   💡 **Google 官方提供 Q4_0 量化 GGUF 版本**，证明大厂开始主动支持量化格式，推动开源生态。

---

## 🌐 生态信号

- **Gemma-4 家族势头最强**：从基础版到指令版，从官方量化到社区 GGUF，累计点赞超 2,000，下载超 150 万，成为本周当之无愧的模型生态中心。其 “any-to-any” 多模态能力标志着模型从单一文本/图像向全模态融合的跨越，未来生态扩展潜力巨大。
- **开源权重 vs 闭源：开源浪潮彻底主导**。DeepSeek-V4-Pro 与 Gemma-4 均以完全开放权重发布，HauhauCS 等社区版本更是激发“去审查”等定制化需求。NVIDIA 也在逐步开放更多模型（如 Nemotron-3 系列），表明开源已成为主流，闭源模型（如 GPT 系列）在 HF 趋势榜上几近消失。
- **量化与微调活动异常活跃**：Unsloth 几乎为每个 Gemma-4 版本都提供了 GGUF/QAT 变体，下载量极高，说明社区对消费级硬件运行大模型的迫切需求。同时，Ideogram-4 的 FP8/NF4 量化也表明图像生成模型正加速适配普及型 GPU。
- **MoE 架构全面普及**：DeepSeek-V4、Nemotron-3-Ultra、Liquid LFM2.5、Qwen3.6、Gemma-4-26B-A4B 等均采用 Mixture-of-Experts，在保持高性能的同时降低激活参数，成为业界标配。

---

## 🔬 值得探索

1. **nvidia/LocateAnything-3B**  
   以 1,733 点赞高居第二，表明“通用定位”能力极具吸引力。该模型可将图像与自然语言描述结合，输出目标位置，有望在机器人、自动驾驶、图像编辑等领域广泛应用。建议测试其在开放世界物体检测任务上的表现。

2. **deepseek-ai/DeepSeek-V4-Pro**  
   作为本周绝对王者（点赞 4,740，下载 430 万），代表了开源 LLM 的最新天花板。强烈推荐研究者深入分析其 MoE 路由策略和上下文扩展能力，或将其作为 Agent 框架的基座模型。

3. **google/gemma-4-12B-it（及其 GGUF 版）**  
   

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*