# Hugging Face 热门模型日报 2026-07-21

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-21 01:57 UTC

---

好的，作为AI模型生态分析师，以下是基于2026年7月21日数据生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026年7月21日**

#### **今日速览**

本周 Hugging Face 趋势榜呈现“巨头发力、社区狂欢”的态势。Google **Gemma-4-31B-it** 凭借惊人的近1200万下载量稳坐流量头把交椅，而 **zai-org/GLM-5.2** 则以超过4200的点赞数领跑社区热度，证明国内大模型开源生态的强劲势头。多模态模型成为绝对主流，近半数热门模型涉及图像与视频理解/生成。值得注意的是，**1-bit/2-bit** 及 **Ternary（三值）** 的极端量化技术（如 prism-ml 的 Bonsai 系列）异军突起，显示社区对在消费级硬件上运行“恐怖”大模型的渴望已从“可能”变为“可行”。

#### **热门模型**

**🧠 语言模型（LLM、对话模型、指令微调）**

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** | 作者: tencent | 点赞: 847 | 下载: 13,698
  腾讯发布的全新基础语言模型，作为文本生成模型受到了社区的高度关注，其衍生量化版本也已迅速跟进。
- **[AngelSlim/Hy3-GGUF](https://huggingface.co/AngelSlim/Hy3-GGUF)** | 作者: AngelSlim | 点赞: 149 | 下载: 109,749
  腾讯 Hy3 模型的 GGUF 量化版本，因其高下载量反映出社区对本地化部署热门新模型的迫切需求。

**🎨 多模态与生成（图像、视频、音频、文本到X）**

- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** | 作者: google | 点赞: 3,297 | 下载: 11,987,240
  Google 的旗舰级多模态模型，凭借强大的性能和谷歌的生态影响力，成为本周下载量之王。
- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** | 作者: zai-org | 点赞: 4,226 | 下载: 531,947
  智谱AI推出的最新MoE模型，凭借强大的对话与推理能力，成为本周社区互动最热烈的模型。
- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** | 作者: baidu | 点赞: 2,441 | 下载: 2,122,848
  百度发布的OCR专用多模态模型，精准解决长尾、复杂场景的文字识别问题，需求旺盛。
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** | 作者: HauhauCS | 点赞: 2,937 | 下载: 2,007,025
  基于Qwen3.6的热门社区微调，以“无审查”和“激进风格”为卖点，体现了社区对模型个性化和“破限”的强烈偏好。
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** | 作者: empero-ai | 点赞: 2,369 | 下载: 2,117,323
  基于Qwen3.5的社区融合微调模型，主打融合Claude风格的叙事与推理能力，GGUF格式使其易于部署。
- **[Wan-AI/Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)** | 作者: Wan-AI | 点赞: 145 | 下载: 2,408
  专注于图像到视频（I2V）生成的模型，特别针对舞蹈动作生成进行优化，是AI视频生成领域的重要补充。
- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** | 作者: OpenMOSS-Team | 点赞: 291 | 下载: 87,533
  MOSS团队的音频转写与说话人分离模型，将强大的语音理解能力集成到了文本生成框架中。
- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** | 作者: Alissonerdx | 点赞: 214 | 下载: 0
  专注于视频生成中的人物身份保持，是基于LTX-Video的LoRA模型，解决了AI视频换脸和一致性难题。

**🔧 专用模型（代码、数学、医疗、嵌入）**

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** | 作者: moonshotai | 点赞: 1,175 | 下载: 713,992
  月之暗面推出的代码专用模型，带有压缩张量技术，专注于提升编程任务的性能与效率。
- **[nvidia/Nemotron-3-Embed-1B-BF16](https://huggingface.co/nvidia/Nemotron-3-Embed-1B-BF16)** | 作者: nvidia | 点赞: 87 | 下载: 61,708
  NVIDIA发布的先进嵌入模型，专为检索增强生成（RAG）和语义搜索任务设计，是企业级应用的基石。
- **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** | 作者: openbmb | 点赞: 135 | 下载: 0
  面壁智能发布的机器人操作VLA（视觉-语言-动作）模型，探索AI从虚拟走向物理世界的前沿。

**📦 微调与量化（社区微调、GGUF、AWQ）**

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** | 作者: prism-ml | 点赞: 855 | 下载: 338,945
  **现象级模型**。通过对Bonsai-27B进行三值化量化，实现了仅2bits的极致压缩，引爆了社区对“小模型跑大参数”的关注。
- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** | 作者: prism-ml | 点赞: 542 | 下载: 1,262,894
  Bonsai-27B的1-bit极端量化版本，下载量惊人，展示了社区对用最低资源运行大模型的狂热追求。
- **[LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V3-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V3-GGUF)** | 作者: LuffyTheFox | 点赞: 85 | 下载: 15,148
  Qwen3.6 MoE模型的一系列社区微调GGUF版本，融合了多种社区配方（如Hermes），是社区“模型杂交”文化的代表。

#### **生态信号**

本周生态趋势非常清晰：

1.  **Qwen家族统治地位巩固**：无论是原始模型的更新（Qwen3.5/3.6），还是海量的社区微调和量化版本（Qwythos、HauhauCS、DavidAU的变体），Qwen系列已经成为社区生态的中流砥柱，几乎每三个热门模型就有一个与Qwen相关。
2.  **MoE与极端量化成双热点**：GLM-5.2 和 Qwen3.6-35B-A3B 证明了稀疏MoE架构是提升模型效率的主流方向。而 prism-ml 的 Bonsai 系列（1-bit 和 Ternary）则将“下放”模型能力推向了极致，虽然牺牲了一定质量，但证明了在手机上运行27B模型并非天方夜谭。
3.  **开源依然强势，但权重分发格式分化**：开源社区极其活跃，所有模型均开源权重。但分发形式明显分化：追求性能的官方模型多用 `safetensors`，而社区消费级部署则几乎完全转向了 `gguf` 和 `mlx` 格式，HF 已成为这些量化格式模型的事实分发中心。

#### **值得探索**

1.  **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)**：作为本周流量冠军，它代表了谷歌在多模态生成领域的顶尖水平。任何对基础多模态能力上限感兴趣的研究者或开发者都应当体验。
2.  **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)**：如果你是边缘计算或端侧部署的研究者，这个1-bit模型将帮你重新定义模型压缩的边界。其下载量证明了这不是玩具而是社区刚需。
3.  **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)**：作为一个全新的多模态原生模型家族（Inkling），它以1269的周点赞数迅速占领头条。在Gemma和Qwen的光芒下，这个新面孔可能代表了多模态融合的新路线，值得深入研究其架构设计。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*