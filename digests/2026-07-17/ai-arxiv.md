# ArXiv AI 研究日报 2026-07-17

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-07-17 01:59 UTC

---

# ArXiv AI 研究日报 (2026-07-17)

## 今日速览

今日投稿聚焦两大方向：**世界行动模型（WAM）的鲁棒性分析与修复**（多篇论文从机理可解释性、控制论角度提升WAM可靠性）；**长上下文强化学习后训练**的突破（LongStraw实现2M tokens有限GPU训练，Long-Context Fine-Tuning与Hierarchical Attention结合降低VRAM需求）。此外，**多智能体协作与自动化科学发现**（BrainPilot、LQCDMaster、Digital Pantheon）成为新兴热点，LLM驱动的科研agent正从概念走向实践。多样性生成与AI安全边界评估也涌现了高质量基准。

## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

1. **Expanding the Lexicon of Ge'ez Based African Languages: A Comparative Study of Amharic and Tigrinya**  
   [http://arxiv.org/abs/2607.15209v1](http://arxiv.org/abs/2607.15209v1)  
   Hailay Kidu Teklehaymanot 等  
   **一句话**：提出 VEXMLM 方法，通过扩展词表大幅降低非拉丁文字（如阿姆哈拉语）的OOV率和子词碎片化，显著提升多语言PLM在低资源语言上的性能。

2. **Mask-Aware Policy Gradients for Diffusion Language Models**  
   [http://arxiv.org/abs/2607.15200v1](http://arxiv.org/abs/2607.15200v1)  
   Haran Raajesh 等  
   **一句话**：首次将强化学习应用于掩码扩散语言模型（MDLM），通过掩码感知策略梯度绕过log-likelihood估计的困难，在推理任务上取得提升。

3. **T²MLR: Transformer with Temporal Middle-Layer Recurrence**  
   [http://arxiv.org/abs/2607.15178v1](http://arxiv.org/abs/2607.15178v1)  
   Ziyang Cai 等  
   **一句话**：提出中间层时间递归机制，使Transformer中间推理状态跨时间步持续存在，突破自回归解码的信息压缩瓶颈，提升长程推理能力。

4. **LongStraw: Long-Context RL Beyond 2M Tokens under a Fixed GPU Budget**  
   [http://arxiv.org/abs/2607.14952v1](http://arxiv.org/abs/2607.14952v1)  
   Changhai Zhou 等  
   **一句话**：在固定GPU预算下实现超2M token的RL后训练，通过分段策略和计算调度弥合推理长上下文与训练短上下文之间的鸿沟，对AI agent至关重要。

5. **On-Policy Delta Distillation**  
   [http://arxiv.org/abs/2607.15161v1](http://arxiv.org/abs/2607.15161v1)  
   Byeongho Heo 等  
   **一句话**：在策略蒸馏中引入delta蒸馏（教师与学生差值），揭示其理论基础，为无需奖励模型的token级监督提供更高效替代方案。

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

6. **BadWAM: When World-Action Models Dream Right but Act Wrong**  
   [http://arxiv.org/abs/2607.15207v1](http://arxiv.org/abs/2607.15207v1)  
   Qi Li 等  
   **一句话**：系统揭示世界行动模型（WAM）存在“世界预测准确但行动失败”的鲁棒性危机，指出耦合表征在分布偏移下的脆弱性，为后续修复提供诊断基础。

7. **Plover: Steering GUI Agents through Plan-Centric Interaction**  
   [http://arxiv.org/abs/2607.15193v1](http://arxiv.org/abs/2607.15193v1)  
   Madhumitha Venkatesan 等  
   **一句话**：提出以计划为中心的交互范式，使GUI agent在动态环境中通过显式计划逐步修正行为，减少因界面状态突变导致的意图漂移。

8. **Digital Pantheon: Simulating and Auditing Coalition Formation with LLM Agents**  
   [http://arxiv.org/abs/2607.15095v1](http://arxiv.org/abs/2607.15095v1)  
   Dylan Van Mulders 等  
   **一句话**：利用LLM agent模拟政治联盟动态谈判，发现RLHF引入的中立性偏见和助人偏见影响了agent群体行为，为计算政治学提供了新审计工具。

9. **BrainPilot: Automating Brain Discovery with Agentic Research**  
   [http://arxiv.org/abs/2607.15079v1](http://arxiv.org/abs/2607.15079v1)  
   Haoxuan Li 等  
   **一句话**：构建自动化脑科学科研agent，覆盖文献回顾、数据分析到结果解读全流程，展示了AI agent在跨尺度、跨模态科学发现中的潜力。

10. **DriftWorld: Fast World Modeling through Drifting**  
    [http://arxiv.org/abs/2607.15065v1](http://arxiv.org/abs/2607.15065v1)  
    Susie Lu 等  
    **一句话**：提出“漂移”式快速世界建模，通过加速扩散模型的多步采样瓶颈，实现在线大规模动作搜索，显著提升机器人规划效率。

11. **OmniaBench: Benchmarking General AI Agents Across Diverse Scenarios**  
    [http://arxiv.org/abs/2607.14989v1](http://arxiv.org/abs/2607.14989v1)  
    Chengyu Shen 等  
    **一句话**：发布覆盖多工具生态、多交互模式的通用AI Agent基准，填补现有评测在场景多样性和交互复杂度上的空白。

### 🔧 方法与框架（新技术、基准测试、效率优化）

12. **Can We Trust Item Response Theory for AI Evaluation?**  
    [http://arxiv.org/abs/2607.15190v1](http://arxiv.org/abs/2607.15190v1)  
    Han Jiang 等  
    **一句话**：严格检验项目反应理论（IRT）在AI基准测试中的适用性，指出AI数据与人类测试数据分布差异导致IRT估计偏差，提醒社区谨慎使用。

13. **AlphaWiSE: Adaptive Weight Interpolation for Continual Multimodal Representation Learning**  
    [http://arxiv.org/abs/2607.15094v1](http://arxiv.org/abs/2607.15094v1)  
    Sarthak Jain 等  
    **一句话**：针对CLIP等模型在持续多模态学习中的模态对齐崩溃，提出自适应权重插值策略，在单一checkpoint中保持跨模态对齐的同时避免遗忘。

14. **Multi-Axis Max@K Reinforcement Learning for Representative Diversity in Text-to-Image Generation**  
    [http://arxiv.org/abs/2607.14962v1](http://arxiv.org/abs/2607.14962v1)  
    Ku Onoda 等  
    **一句话**：形式化文生图的代表性多样性问题，提出多轴Max@K强化学习，强制模型覆盖不同视觉模式，有效缓解性别/种族偏斜。

15. **CFM-Bench: A Unified Multi-Domain Multi-Task Benchmark for Channel Foundation Models**  
    [http://arxiv.org/abs/2607.14975v1](http://arxiv.org/abs/2607.14975v1)  
    Yuan Gao 等  
    **一句话**：首个统一的信道基础模型（CFM）基准，覆盖多无线电配置、多任务场景，终结了CFM评估中各自为政的局面。

### 📊 应用（垂直领域、多模态、代码生成）

16. **MM-IssueLoc: A Controlled Benchmark for Evaluating Visual Evidence in Multimodal Repository-Level Issue Localization**  
    [http://arxiv.org/abs/2607.15205v1](http://arxiv.org/abs/2607.15205v1)  
    Shaoxiong Zhan 等  
    **一句话**：首个包含截图、UI状态等视觉证据的仓库级问题定位基准，揭示现有纯文本评测的盲区，推动多模态软件开发工具进展。

17. **MedFailBench: A Clinician-Built Open-Source Benchmark for Medical AI Safety Boundary Inspection**  
    [http://arxiv.org/abs/2607.15166v1](http://arxiv.org/abs/2607.15166v1)  
    Goktug Ozkan  
    **一句话**：构建临床医生设计的医学AI安全边界基准，按严重等级和安全门类型标注错误，为安全评估提供结构化故障图谱。

18. **Demographically-Conditioned Synthetic Medical Images for Bias Mitigation and Bias Detection in Disease Classifiers**  
    [http://arxiv.org/abs/2607.14984v1](http://arxiv.org/abs/2607.14984v1)  
    Mahmoud Ibrahim 等  
    **一句话**：提出按人口统计学条件生成合成医学图像的方法，既解决少数群体测试样本不足导致的偏差审计置信区间过宽问题，又能直接缓解分类器偏差。

## 研究趋势信号

今日投稿呈现三个强信号：**世界模型与行动模型的耦合鲁棒性**成为热点（BadWAM、Steering Robustness），不再满足于“预测好”而追求“决策稳”，机理可解释性被用于定位激活空间中的脆弱点。**Agent驱动的科学自动化**从概念验证走向系统化（BrainPilot、LQCDMaster），LLM与专业工具的结合正重塑计算生物学和物理学的工作流。**长上下文RL训练的效率突破**（LongStraw、Long-Context Fine-Tuning）标志着后训练阶段正追赶推理阶段，为agent长期记忆和复杂规划提供实用基础。此外，**多样性生成**与**公平性审计**的方法创新（Multi-Axis RL、合成图像）显示社区对模型社会影响的关注从“检测”转向“干预”。

## 值得精读

1. **BadWAM: When World-Action Models Dream Right but Act Wrong**  
   [链接](http://arxiv.org/abs/2607.15207v1) — 深刻揭示了当前世界-行动模型范式的根本缺陷：世界预测能力与行动决策能力可以严重分离。论文通过精心设计的实验和理论分析，为后续鲁棒性修复奠定了关键基础，对具身智能社区具有警示和指导意义。

2. **AlphaWiSE: Adaptive Weight Interpolation for Continual Multimodal Representation Learning**  
   [链接](http://arxiv.org/abs/2607.15094v1) — 提出了一种优雅且高效的持续多模态学习方法。权重插值思路简单但有效，解决了CLIP等模型在增量数据上的模态对齐遗忘问题，实验结果扎实，值得关注其在多模态agent长期部署中的潜力。

3. **LongStraw: Long-Context RL Beyond 2M Tokens under a Fixed GPU Budget**  
   [链接](http://arxiv.org/abs/2607.14952v1) — 攻克了RL后训练中长上下文的内存瓶颈，将有效训练上下文长度从通常的256K推至2M以上。直接服务于需要长程记忆的AI agent场景，方法实用且具有较高的工程参考价值。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*