# Hugging Face 热门模型日报 2026-05-31

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-05-31 06:56 UTC

---

# Hugging Face 热门模型日报（2026-05-31）

## 今日速览

- **DeepSeek-V4 系列全面领跑**：DeepSeek-V4-Pro 以 4,471 点赞、近 600 万下载稳居热度榜首，Flash 版本也收获 1,308 点赞，表明高性能对话模型仍是社区核心需求。
- **多模态模型持续井喷**：美团 LongCat-Video-Avatar 1.5（视频数字人生成）、Circlestone Anima（图像生成）、Supertone 3（语音合成）等多领域模型上榜，多模态生成赛道愈发拥挤。
- **Qwen3.6 生态爆发**：Qwen3.6-27B 基础模型、社区微调与 GGUF 版本（如 unsloth、Jackrong）齐上榜，加上 uncensored 变体，Qwen 家族成为本周“最卷”模型族。
- **量化与社区微调活跃**：GGUF 版本在榜单中占据 5 席，社区涌现了 uncensored、强大聊天模板修复等针对性优化，开源生态的二次创作热度不减。

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

- **deepseek-ai/DeepSeek-V4-Pro**  
  作者: deepseek-ai | 点赞: 4,471 | 下载: 5,918,111  
  ✅ 新一代旗舰对话模型，凭借极致性能和在线能力成为本周人气榜首。

- **deepseek-ai/DeepSeek-V4-Flash**  
  作者: deepseek-ai | 点赞: 1,308 | 下载: 3,427,926  
  ✅ DeepSeek-V4 的轻量化版本，兼顾速度与效果，采用 MIT 开源协议。

- **Qwen/Qwen3.6-27B**  
  作者: Qwen | 点赞: 1,539 | 下载: 4,971,730  
  ✅ Qwen 官方最新多模态语言模型（image-text-to-text），延续对话强项，下载量巨大。

- **stepfun-ai/Step-3.7-Flash**  
  作者: stepfun-ai | 点赞: 142 | 下载: 3,400  
  ✅ 阶跃星辰的轻量级视觉语言模型，主打高效推理。

- **sapientinc/HRM-Text-1B**  
  作者: sapientinc | 点赞: 423 | 下载: 138,118  
  ✅ 专门用于人力资源场景的 1B 文本生成模型，垂直领域特色突出。

- **NemoStation/Marlin-2B**  
  作者: NemoStation | 点赞: 458 | 下载: 15,780  
  ✅ 支持视频+文本输入的 2B 对话模型，拓展视频理解场景。

- **openbmb/MiniCPM5-1B**  
  作者: openbmb | 点赞: 622 | 下载: 28,793  
  ✅ 小尺寸（1B）但功能完整，适合端侧部署。

- **LiquidAI/LFM2.5-8B-A1B**  
  作者: LiquidAI | 点赞: 288 | 下载: 17,084  
  ✅ 采用 MoE 架构的 8B 总参/1B 激活模型，兼顾性能与效率。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **nvidia/LocateAnything-3B**  
  作者: nvidia | 点赞: 515 | 下载: 18,327  
  ✅ 用于图像中任意目标定位的多模态模型（image-text-to-text），通用感知利器。

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**  
  作者: HauhauCS | 点赞: 1,125 | 下载: 2,227,885  
  ✅ Qwen3.6 的社区 uncensored 版本，35B-MoE 架构，下载量超过 220 万，受内容创作圈热捧。

- **meituan-longcat/LongCat-Video-Avatar-1.5**  
  作者: meituan-longcat | 点赞: 419 | 下载: 0  
  ✅ 美团推出的音频/图像生成视频数字人模型，支持音频+图像到视频。

- **bytedance-research/Lance**  
  作者: bytedance-research | 点赞: 983 | 下载: 2,856  
  ✅ 字节跳动出品，支持任意模态到任意模态（any-to-any）的通用生成模型，涵盖图像、视频。

- **SulphurAI/Sulphur-2-base**  
  作者: SulphurAI | 点赞: 1,458 | 下载: 1,557,858  
  ✅ 专注于文本到视频的扩散模型，支持 ComfyUI，下载量超过 150 万。

- **Supertone/supertonic-3**  
  作者: Supertone | 点赞: 746 | 下载: 55,382  
  ✅ 超强文本到语音（TTS）模型，语音合成质量优秀。

- **OpenMOSS-Team/MOSS-TTS-v1.5**  
  作者: OpenMOSS-Team | 点赞: 75 | 下载: 11,254  
  ✅ 中国团队开源 TTS 模型，支持中文语音生成。

- **microsoft/Lens**  
  作者: microsoft | 点赞: 145 | 下载: 1,517  
  ✅ 微软推出的文本到图像扩散模型，支持英文生成，附有论文。

- **nvidia/PiD**  
  作者: nvidia | 点赞: 198 | 下载: 437  
  ✅ 图像超分辨率扩散模型，专注于细节重建。

- **circlestone-labs/Anima**  
  作者: circlestone-labs | 点赞: 1,603 | 下载: 736,443  
  ✅ 单文件扩散模型，兼容 ComfyUI，主打图像生成，社区热度极高。

- **numind/NuExtract3**  
  作者: numind | 点赞: 205 | 下载: 53,338  
  ✅ 图像到文本提取（OCR/理解）模型，基于 Qwen3.5 视觉语言架构。

- **PaddlePaddle/PaddleOCR-VL-1.6**  
  作者: PaddlePaddle | 点赞: 109 | 下载: 2,294  
  ✅ 飞桨 OCR 视觉语言模型最新版，集成 ERNIE 4.5 能力。

### 🔧 专用模型（代码、数学、医疗、嵌入、翻译等）

- **tencent/Hy-MT2-30B-A3B**  
  作者: tencent | 点赞: 435 | 下载: 3,833  
  ✅ 腾讯推出的 30B-MoE 机器翻译模型，支持多语种高效翻译。

- **tencent/Hy-MT2-1.8B**  
  作者: tencent | 点赞: 1,092 | 下载: 16,805  
  ✅ 同系列轻量版翻译模型（1.8B），适合资源受限场景。

- **pyannote/speaker-diarization-3.1**  
  作者: pyannote | 点赞: 2,077 | 下载: 9,771,170  
  ✅ 说话人分割与识别（说话人日志）模型，音频领域标杆，下载量近千万。

- **openai/privacy-filter**  
  作者: openai | 点赞: 1,571 | 下载: 304,691  
  ✅ 用于隐私保护的分词分类模型（token-classification），实现敏感信息过滤。

- **froggeric/Qwen-Fixed-Chat-Templates**  
  作者: froggeric | 点赞: 460 | 下载: 0  
  ✅ 专门为 Qwen 模型修复聊天模板的非模型资源，提升社区使用体验。

### 📦 微调与量化（社区微调、GGUF、AWQ）

- **unsloth/Qwen3.6-27B-MTP-GGUF**  
  作者: unsloth | 点赞: 567 | 下载: 877,938  
  ✅ unsloth 优化的 Qwen3.6-27B GGUF 量化版，结合 MTP（多 Token 预测）特性，适合 llama.cpp 本地运行。

- **Jackrong/Qwopus3.6-27B-v2-MTP-GGUF**  
  作者: Jackrong | 点赞: 172 | 下载: 105,264  
  ✅ 社区二次微调的 Qwen3.6 变体，采用 MTP 量化，支持视觉输入。

- **Jackrong/Qwopus3.6-27B-v2-GGUF**  
  作者: Jackrong | 点赞: 187 | 下载: 33,167  
  ✅ 同系列的普通 GGUF 版本（无 MTP），灵活选择。

- **LiquidAI/LFM2.5-8B-A1B-GGUF**  
  作者: LiquidAI | 点赞: 126 | 下载: 23,685  
  ✅ LFM2.5 的 GGUF 量化版，专为边缘设备设计。

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**  
  （已在多模态中列出，同时属于微调+GGUF类别，因其标记包含 gguf 和 uncensored 微调。）

## 生态信号

- **DeepSeek 与 Qwen 双雄争霸**：DeepSeek-V4 系列以绝对点赞量领跑，但 Qwen3.6 家族（含官方+社区变体）在模块数量（8个模型上榜）和下载总量上更胜一筹，印证了“基础模型+生态量化”的扩散模式。
- **MoE 与小模型成为主流**：10B 以下的小参数量模型（MiniCPM-1B、LFM-8B-A1B、HRM-1B）和 MoE 结构（35B-A3B、30B-A3B）频繁出现，业界对高效推理的追求愈发明显。
- **量化与二次创作热度不减**：GGUF 模型占据 5 席，且下载量普遍较高（数万至百万），说明本地部署需求旺盛。社区 uncensored、MTP 等微调方向丰富，开源生态活力十足。
- **多模态全面开花**：从视频（Sulphur-2、LongCat）、语音（Supertone-3、MOSS-TTS）、图像（Anima、Lens）到任意模态（Lance），生成任务覆盖更广，新玩家频频入局。

## 值得探索

1. **bytedance-research/Lance** — 字节跳动的 any-to-any 通用生成模型，支持图像、视频等多种模态的互相转换，代表了未来多模态生成的前沿方向，值得试用和探究其架构。
2. **pyannote/speaker-diarization-3.1** — 近千万下载量的说话人分割标杆模型，在音频会议、对话分析领域有极高实用价值，适合语音应用开发者深入研究。
3. **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** — 社区微调的 uncensored MoE 模型，下载量惊人（220万+），体现了用户对“无限制”输出的强烈需求，也引发内容安全与合规的讨论。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*