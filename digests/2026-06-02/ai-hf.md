# Hugging Face 热门模型日报 2026-06-02

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-02 02:52 UTC

---

# Hugging Face 热门模型日报（2026-06-02）

## 今日速览

本周 Hugging Face 热度集中在 **多模态混合模型** 与 **边缘量化部署** 两大方向。**Qwen3.6 系列** 凭借 35B 和 27B 两个尺寸的 MoE 版本再度登顶，其中 27B 原生模型下载量突破 500 万。**DeepSeek-V4-Pro** 以 4500+ 点赞和 585 万下载领跑纯语言赛道，证明了超大对话模型的持续需求。**视频生成** 迎来新面孔：SulphurAI 的 text-to-video 模型下载近 166 万，美团长猫团队则推出 **LongCat-Video-Avatar** 实现音频/图像到视频的生成。量化生态上，GGUF 格式覆盖了多款 3.6 系列 MoE 模型，NVIDIA 更是推出了 **Qwen3.6-35B-A3B-NVFP4** 专用量化版，推动大模型在单卡上的落地。

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

- **deepseek-ai/DeepSeek-V4-Pro**  
  https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro  
  作者: deepseek-ai | 点赞: 4,534 | 下载: 5,851,826  
  超大对话模型，支持长上下文与高并发推理，综合能力接近 GPT-4 级别，本周点赞与下载双双登顶。

- **deepseek-ai/DeepSeek-V4-Flash**  
  https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash  
  作者: deepseek-ai | 点赞: 1,342 | 下载: 3,511,636  
  V4 的轻量版，推理速度更快，MIT 开源许可，适合快速集成，是社区部署的热门选择。

- **openbmb/MiniCPM5-1B**  
  https://huggingface.co/openbmb/MiniCPM5-1B  
  作者: openbmb | 点赞: 692 | 下载: 45,698  
  MiniCPM 系列第五代 1B 参数小模型，性能接近 7B 级别，专为端侧与低成本推理设计，本周下载增长迅速。

- **LiquidAI/LFM2.5-8B-A1B**  
  https://huggingface.co/LiquidAI/LFM2.5-8B-A1B  
  作者: LiquidAI | 点赞: 397 | 下载: 37,893  
  Liquid AI 官方 MoE 模型，仅 1B 活跃参数但性能对标 8B Dense 模型，体现 MoE 在效率上的优势。

- **sapientinc/HRM-Text-1B**  
  https://huggingface.co/sapientinc/HRM-Text-1B  
  作者: sapientinc | 点赞: 439 | 下载: 149,543  
  专为人力资源管理场景优化的文本生成模型，1B 参数在垂直任务上表现突出，下载量较高体现行业需求。

- **openai/privacy-filter**  
  https://huggingface.co/openai/privacy-filter  
  作者: openai | 点赞: 1,579 | 下载: 316,092  
  OpenAI 开源的隐私过滤模型（token 分类），用于检测并移除文本中的敏感信息，填补了安全侧的空白。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **Qwen/Qwen3.6-27B**  
  https://huggingface.co/Qwen/Qwen3.6-27B  
  作者: Qwen | 点赞: 1,568 | 下载: 5,154,729  
  阿里通义千问最新视觉语言模型，支持图像+文本输入，27B MoE 架构，本周下载量突破 500 万，社区最热多模态模型。

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**  
  https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive  
  作者: HauhauCS | 点赞: 1,225 | 下载: 2,533,393  
  基于 Qwen3.6 35B MoE 的 uncensored 版本，移除内容安全限制，标签包含 GGUF，适合研究或特定场景。

- **SulphurAI/Sulphur-2-base**  
  https://huggingface.co/SulphurAI/Sulphur-2-base  
  作者: SulphurAI | 点赞: 1,490 | 下载: 1,656,520  
  文本到视频生成模型，Diffusers 架构，支持 GGUF 量化，下载量巨大，代表社区对高质量视频生成的热切需求。

- **nvidia/LocateAnything-3B**  
  https://huggingface.co/nvidia/LocateAnything-3B  
  作者: nvidia | 点赞: 810 | 下载: 35,783  
  英伟达开源的通用定位模型，支持图像+文本输入，可定位任意物体，类似“Everything Detector”的开源实现。

- **openbmb/MiniCPM-V-4.6**  
  https://huggingface.co/openbmb/MiniCPM-V-4.6  
  作者: openbmb | 点赞: 1,088 | 下载: 459,188  
  MiniCPM 视觉语言模型升级版，多模态能力与更大模型竞争，支持端侧部署，下载量持续攀升。

- **bytedance-research/Lance**  
  https://huggingface.co/bytedance-research/Lance  
  作者: bytedance-research | 点赞: 1,002 | 下载: 3,041  
  字节跳动 Any-to-Any 多模态生成模型，支持图像、视频、音频的相互转换，下载量虽小但点赞数高，代表前沿研究方向。

- **NemoStation/Marlin-2B**  
  https://huggingface.co/NemoStation/Marlin-2B  
  作者: NemoStation | 点赞: 482 | 下载: 17,012  
  视频理解模型（video-text-to-text），基于 Qwen3.5，2B 参数，适合轻量级视频内容分析。

- **Supertone/supertonic-3**  
  https://huggingface.co/Supertone/supertonic-3  
  作者: Supertone | 点赞: 771 | 下载: 57,627  
  TTS 模型第三版，支持 ONNX 格式，合成音质优秀，适合语音应用，点赞数高。

- **meituan-longcat/LongCat-Video-Avatar-1.5**  
  https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5  
  作者: meituan-longcat | 点赞: 468 | 下载: 0  
  美团开源的数字人视频生成模型，支持音频/图像输入生成说话视频，虽刚发布无下载但热度高。

- **stepfun-ai/Step-3.7-Flash**  
  https://huggingface.co/stepfun-ai/Step-3.7-Flash  
  作者: stepfun-ai | 点赞: 195 | 下载: 9,256  
  阶跃星辰的视觉语言模型，Flash 版本强调推理速度，在端侧多模态竞争中占位。

- **nvidia/PiD**  
  https://huggingface.co/nvidia/PiD  
  作者: nvidia | 点赞: 239 | 下载: 577  
  超分辨率模型（image-to-image），基于扩散模型，可将低分辨率图像修复，适合图像增强场景。

### 🔧 专用模型（翻译、OCR、语音、说话人分离等）

- **tencent/Hy-MT2-1.8B**  
  https://huggingface.co/tencent/Hy-MT2-1.8B  
  作者: tencent | 点赞: 1,100 | 下载: 18,131  
  腾讯混元翻译模型 1.8B，支持多语种翻译，精度高且小巧，本周翻译赛道下载突出。

- **tencent/Hy-MT2-30B-A3B**  
  https://huggingface.co/tencent/Hy-MT2-30B-A3B  
  作者: tencent | 点赞: 444 | 下载: 4,458  
  腾讯混元翻译旗舰版，30B MoE（3B 活跃），翻译质量对标大模型，适合企业级场景。

- **PaddlePaddle/PaddleOCR-VL-1.6**  
  https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6  
  作者: PaddlePaddle | 点赞: 156 | 下载: 3,190  
  百度 PaddleOCR 视觉语言版，结合 ERNIE4.5 进行图文理解与 OCR，延续 OCR 经典系列。

- **pyannote/speaker-diarization-3.1**  
  https://huggingface.co/pyannote/speaker-diarization-3.1  
  作者: pyannote | 点赞: 2,107 | 下载: 9,591,005  
  说话人分离 v3.1，音频处理标杆模型，本周下载近千万，会议转录等场景刚需。

- **OpenMOSS-Team/MOSS-TTS-v1.5**  
  https://huggingface.co/OpenMOSS-Team/MOSS-TTS-v1.5  
  作者: OpenMOSS-Team | 点赞: 94 | 下载: 18,564  
  中文 TTS 模型，v1.5 优化延迟，支持自定义代码，适合中文语音合成。

- **Kwai-Keye/Keye-VL-2.0-30B-A3B**  
  https://huggingface.co/Kwai-Keye/Keye-VL-2.0-30B-A3B  
  作者: Kwai-Keye | 点赞: 88 | 下载: 784  
  快手视觉语言模型 2.0，30B MoE 参数，专注特征提取与多模态理解，卡位视频理解赛道。

- **nvidia/Cosmos3-Nano**  
  https://huggingface.co/nvidia/Cosmos3-Nano  
  作者: nvidia | 点赞: 77 | 下载: 6,261  
  英伟达 Cosmos 系列第三代，NiMo 版本（可能为 3D 或全模态），适合物理世界理解，标签含 cosmos3_omni。

- **prism-ml/bonsai-image-ternary-4B-gemlite-2bit**  
  https://huggingface.co/prism-ml/bonsai-image-ternary-4B-gemlite-2bit  
  作者: prism-ml | 点赞: 91 | 下载: 0  
  三值量化图像生成模型（1.58-bit），使用 GemLite 技术，探索极低比特扩散模型的边界。

### 📦 微调与量化（社区微调、GGUF、AWQ）

- **unsloth/Qwen3.6-27B-MTP-GGUF**  
  https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF  
  作者: unsloth | 点赞: 595 | 下载: 952,188  
  Unsloth 对 Qwen3.6-27B 的 MTP（Multi-Turn Prompt）量化版，GGUF 格式，下载近百万，快速消费级部署首选。

- **LiquidAI/LFM2.5-8B-A1B-GGUF**  
  https://huggingface.co/LiquidAI/LFM2.5-8B-A1B-GGUF  
  作者: LiquidAI | 点赞: 145 | 下载: 55,212  
  LFM2.5 MoE 的官方 GGUF 量化版，适配 llama.cpp，边缘设备可用，体现官方对量化生态的重视。

- **nvidia/Qwen3.6-35B-A3B-NVFP4**  
  https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4  
  作者: nvidia | 点赞: 121 | 下载: 171,588  
  英伟达官方使用 Model Optimizer 对 Qwen3.6 MoE 的 NVFP4 量化版，极大降低显存占用，单卡即可运行 35B 模型。

- **Jackrong/Qwopus3.6-27B-v2-MTP-GGUF**  
  https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-MTP-GGUF  
  作者: Jackrong | 点赞: 184 | 下载: 139,952  
  社区对 Qwen3.6-27B 的二次微调并量化 GGUF，加入 MTP 支持，是个人开发者推动的典型。

- **stepfun-ai/Step-3.7-Flash-GGUF**  
  https://huggingface.co/stepfun-ai/Step-3.7-Flash-GGUF  
  作者: stepfun-ai | 点赞: 86 | 下载: 37,533  
  阶跃星辰官方发布的 Step-3.7-Flash GGUF 量化版，配合 llama.cpp 实现本地部署。

## 生态信号

- **Qwen3.6 家族势头最盛**：从原版 Qwen3.6-27B（500 万下载）到社区 uncensored 版（250 万下载）再到英伟达 NVFP4 量化版（17 万下载），以及 unsloth 和 Jackrong 的 GGUF 版，形成了从训练到量化的完整生态链。Qwen 系列已超越 Llama 成为当前 HuggingFace 最活跃的基座模型家族。

- **MoE 架构全面普及**：本周前 30 个模型中，MoE（混合专家) 模型超过 10 个，包括 LiquidAI、Qwen3.6、Keye-VL、Hy-MT2 等。MoE 以更低计算成本实现更高参数量，成为一线模型厂商（腾讯、快手、阶跃星辰）的默认选型。

- **开源权重持续领先闭源**：DeepSeek-V4-Pro 以 MIT 协议发布，下载接近 600 万；pyannote 说话人分离模型下载 960 万；OpenAI 甚至开源了隐私过滤模型。闭源模型（如 GPT-4）在榜单上完全缺席，社区主导的开源生态已形成良性循环。

- **量化/微调密集化**：超过 1/3 的模型以 GGUF 或专有量化格式存在。Quantization-aware 的 NVFP4 和 1.58-bit ternary 量化实验表明，产业界和学术界正共同探索极限压缩方案，推动大模型向边缘端下沉。

## 值得探索

1. **Qwen/Qwen3.6-27B** — 当前最火的多模态 MoE 模型，权重公开、社区支持丰富，适合作为多模态应用基座。从视觉问答到图文检索，性能接近闭源竞品，强烈推荐上手体验。

2. **nvidia/Qwen3.6-35B-A3B-NVFP4** — 英伟达结合 Model Optimizer 的 4-bit 量化 MoE 模型，35B 参数仅需约 20GB 显存，是单卡推理中高端模型的代表性方案，适合资源有限的团队探索 MoE 落地。

3. **SulphurAI/Sulphur-2-base** — 文本到视频生成的最新开源方案，下载量已超 160 万，证明社区对视频生成工具的巨大需求。基于 Diffusers 与 GGUF，易于扩展，适合研究视频生成或构建多媒体创作应用。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*