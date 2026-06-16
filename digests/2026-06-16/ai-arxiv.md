# ArXiv AI 研究日报 2026-06-16

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-06-16 02:59 UTC

---

# ArXiv AI 研究日报 | 2026-06-16

---

## 今日速览

今日投稿重点关注 Agentic AI 路由基础设施的信任问题，首篇论文提出“信任原生”架构以防范中间人攻击。大语言模型安全方面，出现“知识蜜罐”防御策略，以低迁移性知识诱导模型窃取攻击。离散扩散语言模型的并行解码取得突破，通过平均场理论提升生成质量。此外，视觉自回归模型概念擦除、多智能体路径规划的未分配代理问题、以及机器人世界动作模型（Latent World Action Models）均有显著进展。安全与对齐、多模态与机器人、以及持续学习仍是活跃方向。

---

## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

**1. TrustedARI: Towards Trust-Native Agentic Routing Infrastructure for Agentic AI**  
作者: Qi Li et al.  
链接: http://arxiv.org/abs/2606.15822v1  
一句话说明：首次系统分析 Agentic AI 路由基础设施的信任风险，提出“信任原生”架构，防止中间人获取明文查询和响应。

**2. The Truth Stays in the Family: Enhancing Contextual Grounding via Inherited Truthful Heads in Model Lineages**  
作者: Miso Choi et al.  
链接: http://arxiv.org/abs/2606.15821v1  
一句话说明：揭示基础LLM与下游多模态变体之间的“真实头”继承关系，通过遗传机制提升上下文对齐。

**3. Let Them Steal: Trapping Large Language Model Extraction Attacks with Knowledge Honeypot**  
作者: Yuyang Dai, Yushun Dong  
链接: http://arxiv.org/abs/2606.15810v1  
一句话说明：提出“知识蜜罐”防御，用低迁移性知识作为诱饵，诱导模型窃取攻击并降低攻击成功率。

**4. Mean-Field Parallel Decoding for Discrete Diffusion Language Models**  
作者: Tamim Zoabi et al.  
链接: http://arxiv.org/abs/2606.15805v1  
一句话说明：用平均场理论建模 token 间的依赖，实现离散扩散语言模型的高质量并行生成，显著降低自回归延迟。

**5. GAS-Leak-LLM: Genetic Algorithm-Based Suffix Optimization for Black-Box LLM Jailbreaking**  
作者: Aman Anifer et al.  
链接: http://arxiv.org/abs/2606.15788v1  
一句话说明：基于遗传算法搜索后缀，实现黑盒大语言模型越狱攻击，效率优于现有方法。

**6. Snyk VulnBench JS 1.0: Can LLMs Find the Same Bugs Twice?**  
作者: Liran Tal et al.  
链接: http://arxiv.org/abs/2606.15762v1  
一句话说明：300次重复漏洞扫描实验表明，大语言模型安全审查的可重复性不稳定，仅约一半发现能稳定复现。

---

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

**7. Unassigned Agents in Compilation-based Multi-agent Path Finding**  
作者: Pavel Surynek  
链接: http://arxiv.org/abs/2606.15797v1  
一句话说明：首次形式化处理编译式多智能体路径规划中的“未分配智能体”问题，在部分未指定目标时仍能完成总体任务。

**8. RoboPIN: Grounded Embodied Reasoning via Pinned Chain-of-Thought**  
作者: Yaoting Huang et al.  
链接: http://arxiv.org/abs/2606.15753v1  
一句话说明：通过“钉住”视觉特征引用链，解决多步推理中实体漂移问题，提升具身推理的视觉接地稳定性。

**9. Multi-agent Framework for Time-Sensitive Complementary Collaboration in Minecraft**  
作者: Juheon Yi et al.  
链接: http://arxiv.org/abs/2606.15684v1  
一句话说明：构建基于Minecraft的时间敏感互补协作基准，强调异构智能体强制协作、动态环境和严格时间约束。

**10. DYNA: Dynamic Episodic Memory Networks for Augmenting LLMs with Temporal Knowledge Graphs**  
作者: Ali Sarabadani, Mahtab Tajvidiyan  
链接: http://arxiv.org/abs/2606.15778v1  
一句话说明：用轻量级时序知识图注入持续学习框架，让冻结LLM能吸收新事件知识，避免灾难性遗忘。

---

### 🔧 方法与框架（新技术、基准测试、效率优化）

**11. SACE: Concept Erasure at the Semantic Singularity in Visual Autoregressive Models**  
作者: Siya Yang et al.  
链接: http://arxiv.org/abs/2606.15819v1  
一句话说明：在视觉自回归模型中识别“语义奇点”，实现概念擦除而不引发灾难性语义崩溃。

**12. How to Score Experts for One-Shot MoE Expert Pruning: A Unified Formulation and Selection Principle**  
作者: Zongfang Liu et al.  
链接: http://arxiv.org/abs/2606.15716v1  
一句话说明：统一现有MoE剪枝打分标准，推导出基于贡献度与多样性的最优选择原理，内存压缩达40%以上。

**13. ReQAT: Achieving Full-Precision Reasoning Accuracy with 4-bit Floating-Point Quantization-Aware Training**  
作者: Janghwan Lee et al.  
链接: http://arxiv.org/abs/2606.15682v1  
一句话说明：提出全量化感知训练方案，在4位浮点精度下首次实现推理精度与全精度持平，大幅降低KV缓存开销。

**14. The Reservoir Attention Network: Cross-Pass State in Pretrained Transformers via Content-Addressable Reservoir Injection**  
作者: Emma Leonhart  
链接: http://arxiv.org/abs/2606.15678v1  
一句话说明：在预训练Transformer中注入固定随机储层作为跨前向传播的状态载体，无需额外训练即可实现长程记忆。

**15. Retrievable Gradients: Continual Post-Training Without Cumulative Weight Drift**  
作者: Weihang Su et al.  
链接: http://arxiv.org/abs/2606.15734v1  
一句话说明：用检索代替直接参数更新，避免持续后训练中的权重漂移和遗忘，保留通用能力。

---

### 📊 应用（垂直领域、多模态、代码生成）

**16. LaWAM: Latent World Action Models for Efficient Dynamics-Aware Robot Policies**  
作者: Jialei Chen et al.  
链接: http://arxiv.org/abs/2606.15768v1  
一句话说明：在潜空间中预测动作后果，使视觉-语言-动作模型具备显式物理世界前瞻，提升机器人策略准确性。

**17. Beyond English: Uncovering the Multilingual Gap in Vision-Language-Action Models**  
作者: Hanyang Chen et al.  
链接: http://arxiv.org/abs/2606.15714v1  
一句话说明：系统评估现有VLA模型在多语言指令下的显著性能下降，揭示机器人策略的语言泛化瓶颈。

**18. EHRNote-ChatQA: A Benchmark for Evidence-Grounded Multi-Turn Clinical Question Answering**  
作者: Jiyoun Kim et al.  
链接: http://arxiv.org/abs/2606.15735v1  
一句话说明：构建基于出院小结的多轮临床问答基准，要求模型在长病程历史中检索并综合证据回答。

**19. Continuous Cross-Domain Traffic State Prediction via Memory-Augmented Graph Liquid Time-Constant Networks**  
作者: Jinrong Xiang, Ming Xu  
链接: http://arxiv.org/abs/2606.15807v1  
一句话说明：用记忆增强的图液体时间常数网络实现跨域交通状态预测，解决数据稀疏区域的迁移难题。

**20. Mitigating Visual Hallucinations in Multimodal Systems through Retrieval-Augmented Reliability-Aware Inference**  
作者: Pratheswaran Hariharan et al.  
链接: http://arxiv.org/abs/2606.15782v1  
一句话说明：引入检索增强的可靠性感知推理，在视觉证据不足时主动降低置信度，减少多模态幻觉。

---

## 研究趋势信号

从今日投稿中可观察到以下新兴方向：
- **安全基础设施信任**：Agentic AI 路由（ARI）的信任原生设计成为新焦点，与模型提取防御形成互补。
- **离散扩散并行解码**：平均场理论被引入扩散语言模型，使高质量并行生成成为可能，或将改变推理延迟瓶颈。
- **世界动作模型**：在潜空间预测动作后果的范式（LaWAM）延续了“预测-条件”策略，向更高效、更鲁棒的机器人控制发展。
- **可重复性审计**：Snyk VulnBench 揭示大模型安全评估的不稳定性，推动更严格的基准设计和实验规范。
- **储层计算再兴起**：Reservoir Attention Network 将随机固定储层注入Transformer，为跨前向传播状态保持提供轻量方案。

---

## 值得精读

1. **TrustedARI**（cs.AI, cs.CR）  
作为首篇系统研究 Agentic AI 路由信任问题的工作，提出了“信任原生”架构，对于理解未来多智能体协作的安全基座具有奠基意义。

2. **Mean-Field Parallel Decoding for Discrete Diffusion Language Models**（cs.LG）  
利用平均场理论解决离散扩散模型中 token 独立生成的冲突问题，在速度与质量间取得突破，是生成模型结构创新的重要进展。

3. **Snyk VulnBench JS 1.0**（cs.CR, cs.AI, cs.SE）  
300次重复实验揭示大模型代码漏洞发现的可重复性严重不足，结果对LLM在安全关键领域的可靠部署提出严肃质疑，值得所有从业者关注。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*