# Hugging Face 热门模型日报 2026-07-15

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-15 01:45 UTC

---

# Hugging Face 热门模型日报 — 2026-07-15

## 📌 今日速览

- **GLM-5.2**（zai-org）凭 3,948 赞登顶周榜，其 MoE 架构和高下载量（48.9 万）表明社区对稀疏激活大模型的兴趣持续升温。  
- **Qwen 3.5/3.6 生态爆发**：Qwen 衍生品占据榜单近 1/3，包括多模态（Qwythos、ThinkingCap）、量化版（unsloth 的 NVFP4/GGUF）以及未审查变体（HauhauCS），显示 Qwen 已成为最活跃的基座系列。  
- **量化与高效的极致追求**：2-bit（Ternary-Bonsai）、1-bit（Bonsai）以及 NVFP4 等极端量化模型大量出现，表明边缘部署和低成本推理成为核心需求。  
- **视频与身份保留生成崛起**：lingbot‑world‑v2（i2v）和 LTX‑Best‑Face‑ID（text‑to‑video + 人脸保持）上榜，多模态生成方向从静态图像向动态视频加速延伸。  

---

## 📊 热门模型分类

### 🧠 语言模型（LLM、对话、指令微调）

1. **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**  
   - 作者：zai-org | 👍 3,948 | ⬇️ 489,611  
   - 通用对话 MoE 模型，采用 DSA 稀疏架构，本周点赞最高。

2. **[tencent/Hy3](https://huggingface.co/tencent/Hy3)**  
   - 作者：tencent | 👍 781 | ⬇️ 10,406  
   - 腾讯 Hunyuan 系列第三代文本生成模型，支持长上下文与多轮对话。

3. **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)**  
   - 作者：yuxinlu1 | 👍 1,189 | ⬇️ 468,629  
   - 基于 Gemma‑4 的 Agent 微调版，GGUF 量化，专为终端/代码任务优化。

4. **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)**  
   - 作者：deepreinforce-ai | 👍 880 | ⬇️ 1,533,354  
   - 35B 参数通用 LLM 的 GGUF 量化版，MIT 协议，下载量巨大。

5. **[nvidia/Nemotron-Labs-Audex-30B-A3B](https://huggingface.co/nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4)**  
   - 作者：nvidia | 👍 149 | ⬇️ 1,332  
   - NVIDIA 原生的 30B 稠密语言模型，3B 激活的 MoE 变体，专注高质量文本生成。

---

### 🎨 多模态与生成（图像、视频、音频、文本到X）

1. **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**  
   - 作者：empero-ai | 👍 2,156 | ⬇️ 2,006,265  
   - Qwen3.5 基座的视觉语言模型 GGUF 版，支持图文理解与推理，下载量超 200 万。

2. **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)**  
   - 作者：bottlecapai | 👍 341 | ⬇️ 6,208  
   - 基于 Qwen3.6 的连锁思维（CoT）增强视觉 LLM，擅长复杂视觉推理。

3. **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)**  
   - 作者：InternScience | 👍 538 | ⬇️ 30,539  
   - MoE 架构的智能体视觉语言模型，专为多工具调用和视觉代理场景设计。

4. **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**  
   - 作者：baidu | 👍 1,983 | ⬇️ 1,715,301  
   - 百度出品的高精度 OCR 模型，支持任意语言与版式，下载超 170 万。

5. **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
   - 作者：HauhauCS | 👍 2,731 | ⬇️ 2,443,871  
   - 未审查版的 Qwen3.6 MoE 多模态模型，去除了安全过滤，社区争议与关注并存。

6. **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)**  
   - 作者：OpenMOSS-Team | 👍 189 | ⬇️ 65,109  
   - 端到端语音转录 + 说话人识别模型，适用于会议记录与多说话人场景。

7. **[robbyant/lingbot-video-moe-30b-a3b](https://huggingface.co/robbyant/lingbot-video-moe-30b-a3b)**  
   - 作者：robbyant | 👍 104 | ⬇️ 700  
   - 30B 参数 MoE 视频扩散模型，支持高质量视频生成。

8. **[robbyant/lingbot-world-v2-14b-causal-fast](https://huggingface.co/robbyant/lingbot-world-v2-14b-causal-fast)**  
   - 作者：robbyant | 👍 96 | ⬇️ 0  
   - 图像到视频的世界模型，因果建模风格，尤其适合交互式视频生成。

9. **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)**  
   - 作者：Alissonerdx | 👍 141 | ⬇️ 0  
   - LTX-Video 的面部身份保持 LoRA，实现参考到视频的人脸一致性。

10. **[mgwr/M87](https://huggingface.co/mgwr/M87)**  
    - 作者：mgwr | 👍 107 | ⬇️ 2,408  
    - 基于 Krea‑2 的图像生成 LoRA，风格化能力强，适合创意设计。

---

### 🔧 专用模型（代码、数学、医疗、嵌入等）

1. **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)**  
   - 作者：froggeric | 👍 903 | ⬇️ 0  
   -

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*