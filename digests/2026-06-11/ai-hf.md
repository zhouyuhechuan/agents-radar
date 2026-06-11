# Hugging Face 热门模型日报 2026-06-11

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-11 02:53 UTC

---

好的，作为AI模型生态分析师，以下是基于2026年6月11日数据生成的日报。

---

# Hugging Face 热门模型日报（2026-06-11）

### 今日速览

本周Hugging Face生态迎来重大更新：**DeepSeek-V4-Pro** 以压倒性的点赞与下载量登顶，印证了高性能开源语言模型的持续热度。**Google Gemma-4 系列** 成为最活跃的模型家族，其强大的多模态（any-to-any）能力吸引了大量社区进行量化与微调（如Unsloth、OBLITERATUS等版）。**Nvidia** 在专业ASR（语音识别）和专业任务（位置理解）模型上发力，体现了垂直领域的深化。此外，**多模态生成模型**（图像、音频、视频）百花齐放，尤其是**Ideogram-4** 和 **ByteDance Bernini-R** 的发布，标志着AI生成内容的边界正被迅速拓宽。

### 热门模型

#### 🧠 语言模型（LLM、对话模型、指令微调）

- **DeepSeek-V4-Pro** ([链接](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro))
  - 作者: deepseek-ai | 点赞: 4,762 | 下载: 4,061,006
  - 说明：DeepSeek的最新旗舰模型，凭借顶尖性能与超高热度的社区下载量，成为本周绝对王者。

- **nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16** ([链接](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16))
  - 作者: nvidia | 点赞: 189 | 下载: 59,066
  - 说明：Nvidia的巨型MoE（混合专家）模型，550B总参数，55B活跃参数，定位高端对话与推理任务。

- **LiquidAI/LFM2.5-8B-A1B** ([链接](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B))
  - 作者: LiquidAI | 点赞: 584 | 下载: 142,134
  - 说明：Liquid AI出品的高效MoE模型，8B总参数仅1B活跃参数，体现了对推理效率的极致追求。

- **JetBrains/Mellum2-12B-A2.5B-Thinking** ([链接](https://huggingface.co/JetBrains/JetBrains/Mellum2-12B-A2.5B-Thinking))
  - 作者: JetBrains | 点赞: 281 | 下载: 18,273
  - 说明：JetBrains推出的专注于推理能力的对话模型，通过“思考”步骤提升复杂问题解答质量。

#### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **nvidia/LocateAnything-3B** ([链接](https://huggingface.co/nvidia/LocateAnything-3B))
  - 作者: nvidia | 点赞: 1,807 | 下载: 131,794
  - 说明：Nvidia发布的图像定位基础模型，能根据文本指令在图像中任意定位对象，热度惊人。

- **bosonai/higgs-audio-v3-tts-4b** ([链接](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b))
  - 作者: bosonai | 点赞: 325 | 下载: 19,948
  - 说明：一款高质量的4B参数文本转语音（TTS）模型，标志着高保真音频生成进入新阶段。

- **ideogram-ai/ideogram-4-fp8** ([链接](https://huggingface.co/ideogram-ai/ideogram-4-fp8))
  - 作者: ideogram-ai | 点赞: 474 | 下载: 7,170
  - 说明：知名图像生成模型Ideogram的第四代FP8量化版，降低了部署门槛，吸引大量用户尝试。

- **google/magenta-realtime-2** ([链接](https://huggingface.co/google/magenta-realtime-2))
  - 作者: google | 点赞: 174 | 下载: 19,806
  - 说明：Google Magenta项目新作，专注于实时文本到音频生成，探索AI音乐与声音创作新方向。

- **ByteDance/Bernini-R** ([链接](https://huggingface.co/ByteDance/Bernini-R))
  - 作者: ByteDance | 点赞: 213 | 下载: 305
  - 说明：字节跳动发布的图像文本到视频模型，专注于渲染与动画生成，是视频生成领域强力竞争者。

- **stepfun-ai/Step-3.7-Flash** ([链接](https://huggingface.co/stepfun-ai/Step-3.7-Flash))
  - 作者: stepfun-ai | 点赞: 363 | 下载: 50,187
  - 说明：阶跃星辰发布的高效能视觉语言模型，平衡了速度与性能，适合实时交互场景。

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** ([链接](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive))
  - 作者: HauhauCS | 点赞: 1,634 | 下载: 3,057,541
  - 说明：社区高度关注的“无审查”版Qwen3.6变体，火爆的下载量反映了用户对模型自由度的强烈需求。

#### 🔧 专用模型（代码、数学、医疗、嵌入）

- **nvidia/nemotron-3.5-asr-streaming-0.6b** ([链接](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b))
  - 作者: nvidia | 点赞: 349 | 下载: 4,965
  - 说明：Nvidia推出的高效流式自动语音识别（ASR）模型，专为低延迟实时转录场景设计。

- **CohereLabs/North-Mini-Code-1.0** ([链接](https://huggingface.co/CohereLabs/North-Mini-Code-1.0))
  - 作者: CohereLabs | 点赞: 262 | 下载: 1,859
  - 说明：Cohere专为代码生成推出的轻量级模型，标志着代码专用模型赛道持续升温。

- **sapientinc/HRM-Text-1B** ([链接](https://huggingface.co/sapientinc/HRM-Text-1B))
  - 作者: sapientinc | 点赞: 740 | 下载: 134,752
  - 说明：一款针对医疗记录与管理（HRM）场景的专用文本模型，反映了行业垂直模型的强劲需求。

#### 📦 微调与量化（社区微调、GGUF、AWQ）

- **unsloth/gemma-4-12b-it-GGUF** ([链接](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF))
  - 作者: unsloth | 点赞: 551 | 下载: 711,706
  - 说明：Unsloth社区制作的Gemma-4量化版，极大降低了本地部署门槛，下载量超过原版。

- **OBLITERATUS/Gemma-4-12B-OBLITERATED** ([链接](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED))
  - 作者: OBLITERATUS | 点赞: 214 | 下载: 14,838
  - 说明：社区对Gemma-4进行“摧毁式”微调的版本，通常意味着去除了安全限制，追求更高自由度。

- **google/gemma-4-12B-it-qat-q4_0-gguf** ([链接](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf))
  - 作者: google | 点赞: 124 | 下载: 96,749
  - 说明：Google官方发布的Gemma-4量化感知训练（QAT）版本，代表了官方对模型轻量化与易用性的重视。

- **huihui-ai/Huihui-gemma-4-12B-it-abliterated** ([链接](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-it-abliterated))
  - 作者: huihui-ai | 点赞: 136 | 下载: 6,400
  - 说明：另一款专注于移除模型限制的社区微调版，与OBLITERATUS类似，反映了社区对“去审查”的持续热情。

### 生态信号

1.  **“Gemma-4”家族风暴**：Google的Gemma-4无疑是本周最活跃的模型家族。从官方版、到Unsloth的量化版、再到OBLITERATUS等社区“破坏性”微调版，形成了一个围绕中心模型的完善生态圈，显示出大厂基础模型+社区二次创新的模式已非常成熟。
2.  **开源权重 vs 闭源**：本周榜单前列全都是开源权重模型（DeepSeek、Gemma、Nvidia Nemotron）。这不仅巩固了开源作为AI民主化核心驱动力的地位，也说明即使闭源模型性能强劲，开源社区凭借灵活性和可控性获得了更高的实际部署量。
3.  **量化与微调是社区核心引擎**：Unsloth社区模型的高下载量是强有力的证明。用户对本地化、高效运行大型模型的渴望远超想象。同时，“未经审查”和“激进”的微调版本火爆，揭示了用户对内容多样性和模型“创造力”边界的探索需求。

### 值得探索

1.  **DeepSeek-V4-Pro**：性能与社区反馈的标杆。如果你想了解当前开源LLM的天花板在哪，以及最活跃的开源社区是如何围绕一个模型运作的，这个模型是必选项。
2.  **nex-agi/Nex-N2-Pro**：基于Qwen3.5 MoE架构的微调版本，下载和点赞数不高但增长潜力巨大。作为新兴的MoE模型变体，它代表了“小而强”的模型设计哲学，值得研究其在特定任务上的效率提升。
3.  **ByteDance/Bernini-R**： 视频生成是当前AIGC的核心战场之一。作为来自字节跳动的新模型，它结合了图像文本到视频的能力，是探索AI视频内容创作新技术的绝佳起点。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*