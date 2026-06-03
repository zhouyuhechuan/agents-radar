# Hugging Face 热门模型日报 2026-06-03

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-03 03:26 UTC

---

# Hugging Face 热门模型日报 (2026-06-03)

## 📰 今日速览

本周 Hugging Face 榜单迎来多个重磅更新：**DeepSeek V4 系列**（Pro / Flash）以超 4500 点赞和近千万下载量统治语言模型赛道；**Qwen3.6 家族** 在多模态领域全面开花，官方 27B 与社区微调版本均跻身前列；**Nvidia 一口气发布 6 款模型**，涵盖目标定位（LocateAnything-3B）、视觉生成（Cosmos3 系列）及超分（PiD），生态布局意图明显；**视频生成** 赛道升温，Sulphur-2、Lance、LongCat 等模型同时上榜；此外，**MoE 架构** 持续深化，量化社区（GGUF、NVFP4）也异常活跃，极端三元量化（1.58-bit）首次进入热门视线。

---

## 🔥 热门模型

### 🧠 语言模型（LLM、对话、指令微调）

1. **deepseek-ai/DeepSeek-V4-Pro**  
   [链接](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)  
   作者: deepseek-ai | 👍 4,577 | ⬇️ 5,829,042  
   > DeepSeek 最新旗舰对话模型，采用 MoE 架构，以极高点赞和下载量断层领先，成为本周社区焦点。

2. **deepseek-ai/DeepSeek-V4-Flash**  
   [链接](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)  
   作者: deepseek-ai | 👍 1,367 | ⬇️ 3,525,218  
   > V4 系列的轻量版（MIT 许可），推理速度更快，适合低成本部署，社区下载量紧随 Pro 版本。

3. **LiquidAI/LFM2.5-8B-A1B**  
   [链接](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)  
   作者: LiquidAI | 👍 444 | ⬇️ 47,742  
   > Liquid 基金会推出的 MoE 模型，激活仅 1B 参数却达到 8B 级性能，兼顾效率与效果。

4. **openbmb/MiniCPM5-1B**  
   [链接](https://huggingface.co/openbmb/MiniCPM5-1B)  
   作者: openbmb | 👍 737 | ⬇️ 57,683  
   > MiniCPM 第五代 1B 参数小模型，适用于端侧部署，凭借高性价比获得开发者青睐。

5. **JetBrains/Mellum2-12B-A2.5B-Thinking**  
   [链接](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)  
   作者: JetBrains | 👍 142 | ⬇️ 799  
   > JetBrains 出品的 MoE 推理优化模型，强调“思考链”能力，在代码和逻辑任务上有潜力。

6. **sapientinc/HRM-Text-1B**  
   [链接](https://huggingface.co/sapientinc/HRM-Text-1B)  
   作者: sapientinc | 👍 476 | ⬇️ 153,029  
   > 专为人力资源管理场景设计的轻量文本生成模型，1B 参数即支持 HR 对话与文书生成。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

1. **Qwen/Qwen3.6-27B**  
   [链接](https://huggingface.co/Qwen/Qwen3.6-27B)  
   作者: Qwen | 👍 1,579 | ⬇️ 5,243,648  
   > Qwen 官方发布的多模态视觉语言模型（27B），支持图文交互与对话，下载量突破 500 万。

2. **nvidia/LocateAnything-3B**  
   [链接](https://huggingface.co/nvidia/LocateAnything-3B)  
   作者: nvidia | 👍 999 | ⬇️ 61,604  
   > Nvidia 推出的通用目标定位模型，3B 参数，可通过文本或图像指令完成精细定位，引发科研与应用关注。

3. **stepfun-ai/Step-3.7-Flash**  
   [链接](https://huggingface.co/stepfun-ai/Step-3.7-Flash)  
   作者: stepfun-ai | 👍 217 | ⬇️ 12,932  
   > 阶跃星辰发布的多模态 Flash 版本，兼顾图文理解与生成速度，定位端侧应用。

4. **meituan-longcat/LongCat-Video-Avatar-1.5**  
   [链接](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)  
   作者: meituan-longcat | 👍 492 | ⬇️ 174  
   > 美团推出的音频/图像驱动的视频数字人生成模型，支持语音到口型、表情同步。

5. **bytedance-research/Lance**  
   [链接](https://huggingface.co/bytedance-research/Lance)  
   作者: bytedance-research | 👍 1,012 | ⬇️ 3,192  
   > 字节跳动发布的“任意到任意”多模态生成模型，可同时处理图像、视频、文本与音频，潜力巨大。

6. **NemoStation/Marlin-2B**  
   [链接](https://huggingface.co/NemoStation/Marlin-2B)  
   作者: NemoStation | 👍 498 | ⬇️ 17,616  
   > 基于 Qwen3.5 的视频理解模型（2B 参数），支持视频-文本对话，轻量高效。

7. **nvidia/Cosmos3-Nano**  
   [链接](https://huggingface.co/nvidia/Cosmos3-Cosmos3-Nano)  
   作者: nvidia | 👍 115 | ⬇️ 9,071  
   > Nvidia Cosmos3 系列的最小版本，面向极低算力的视觉生成（Omni 模型）。

8. **SulphurAI/Sulphur-2-base**  
   [链接](https://huggingface.co/SulphurAI/Sulphur-2-base)  
   作者: SulphurAI | 👍 1,512 | ⬇️ 1,663,826  
   > 基于 Lightricks LTX-2.3 的高效文本到视频生成模型，下载量超 160 万，社区热捧。

9. **nvidia/Cosmos3-Super**  
   [链接](https://huggingface.co/nvidia/Cosmos3-Cosmos3-Super)  
   作者: nvidia | 👍 100 | ⬇️ 2,830  
   > Cosmos3 系列的旗舰版本，支持文本/图像到视频、图像生成等多种任务。

10. **nvidia/Cosmos3-Super-Image2Video**  
    [链接](https://huggingface.co/nvidia/Cosmos3-Cosmos3-Super-Image2Video)  
    作者: nvidia | 👍 84 | ⬇️ 536  
    > Cosmos3 系列的图像到视频专版，将静态图转化为动态视频。

11. **nvidia/Cosmos3-Super-Text2Image**  
    [链接](https://huggingface.co/nvidia/Cosmos3-Cosmos3-Super-Text2Image)  
    作者: nvidia | 👍 79 | ⬇️ 517  
    > Cosmos3 的文本到图像子模型，与其兄弟版本构成完整 Omni 管线。

12. **nvidia/PiD**  
    [链接](https://huggingface.co/nvidia/PiD)  
    作者: nvidia | 👍 268 | ⬇️ 646  
    > 基于扩散模型的图像超分辨率模型，在细节恢复上具有竞争力。

13. **Kwai-Keye/Keye-VL-2.0-30B-A3B**  
    [链接](https://huggingface.co/Kwai-Keye/Keye-VL-2.0-30B-A3B)  
    作者: Kwai-Keye | 👍 100 | ⬇️ 964  
    > 快手推出的 MoE 视觉语言模型（30B 总参、3B 激活），兼顾多模态理解与效率。

### 🔧 专用模型（代码、数学、医疗、嵌入、OCR、TTS 等）

1. **PaddlePaddle/PaddleOCR-VL-1.6**  
   [链接](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)  
   作者: PaddlePaddle | 👍 190 | ⬇️ 4,003  
   > 百度飞桨的新版视觉语言 OCR 模型，融合 ERNIE 4.5，文档理解能力大幅提升。

2. **openai/privacy-filter**  
   [链接](https://huggingface.co/openai/privacy-filter)  
   作者: openai | 👍 1,595 | ⬇️ 300,

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*