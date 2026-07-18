# ArXiv AI 研究日报 2026-07-18

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-07-18 01:49 UTC

---

# ArXiv AI 研究日报（2026-07-18）

## 今日速览

今日投稿显示了几个关键突破：**RoboTTT** 将机器人视觉运动上下文窗口扩展到 8000 时间步，比现有方法提升三个数量级；**Partition, Prompt, Aggregate** 从统计自一致性角度重新解释了上下文学习，为语言模型不确定性估计提供了新框架；**BadWAM** 揭示了世界-动作模型可能“梦对但做错”的致命缺陷，引发对具身智能安全性反思；**Subjective Risk Decomposition** 提出了基于高阶建模决策的不确定性度量新视角；**Grokipedia vs Wikipedia** 则首次大规模审计了 LLM 生成百科内容的政治中立性。此外，多篇论文关注多智能体协作、医疗 AI 安全边界以及低资源语言词汇扩展。

## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

1. **Partition, Prompt, Aggregate: Statistical Self-Consistency in Language Models**  
   [http://arxiv.org/abs/2607.15277v1](http://arxiv.org/abs/2607.15277v1)  
   Wolf, Kleine Buening, Krause et al.  
   ▶ 通过分块、提示、聚合的框架，将语言模型输出视为条件分布估计，并形式化证明了自一致性概率公理，为理解上下文学习提供了严格的统计学基础。

2. **In-Place Tokenizer Expansion for Pre-trained LLMs**  
   [http://arxiv.org/abs/2607.15232v1](http://arxiv.org/abs/2607.15232v1)  
   Smith, Dakhran, Cabrera et al.  
   ▶ 提出一种无需重训即可扩展预训练 LLM 分词器词汇表的方法，解决了低资源语言和后续添加语言的分词碎片化问题，降低延迟与计算成本。

3. **Mask-Aware Policy Gradients for Diffusion Language Models**  
   [http://arxiv.org/abs/2607.15200v1](http://arxiv.org/abs/2607.15200v1)  
   Raajesh, Shah, Klivans et al.  
   ▶ 针对掩码扩散语言模型（MDLM）设计强化学习策略梯度方法，通过近似对数似然解决训练中的不可计算性，提升推理能力。

4. **T^2MLR: Transformer with Temporal Middle-Layer Recurrence**  
   [http://arxiv.org/abs/2607.15178v1](http://arxiv.org/abs/2607.15178v1)  
   Cai, Zhu, Dong et al.  
   ▶ 在 Transformer 中间层引入时间维度的循环连接，使推理状态得以跨时间步持续，缓解自回归解码的信息压缩问题。

5. **On-Policy Delta Distillation**  
   [http://arxiv.org/abs/2607.15161v1](http://arxiv.org/abs/2607.15161v1)  
   Heo, Hwang, Yun et al.  
   ▶ 深入分析 on-policy 蒸馏的理论基础，证明其在 token 级教师监督下的收敛性质，为无需奖励模型的 post-training 提供新视角。

6. **Can We Trust Item Response Theory for AI Evaluation?**  
   [http://arxiv.org/abs/2607.15190v1](http://arxiv.org/abs/2607.15190v1)  
   Jiang, Kwon, Luo et al.  
   ▶ 系统论证了 AI 基准数据偏离人类测试假设时，项目反应理论（IRT）的估计偏差和排名失真，对当前 AI 评估实践提出重要警示。

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

7. **RoboTTT: Context Scaling for Robot Policies**  
   [http://arxiv.org/abs/2607.15275v1](http://arxiv.org/abs/2607.15275v1)  
   Jiang, Chebotar, Zheng et al.  
   ▶ 将机器人策略的视觉运动上下文扩展到 8000 时间步（三数量级提升），利用测试时训练实现长程记忆与实时适应，是机器人基础模型的重要进步。

8. **SearchOS-V1: Towards Robust Open-Domain Information-Seeking Agent Collaboration**  
   [http://arxiv.org/abs/2607.15257v1](http://arxiv.org/abs/2607.15257v1)  
   Zhang, Gao, Wu et al.  
   ▶ 提出多智能体搜索操作系统，通过任务追踪和协作机制解决长交互历史中信息搜索代理的任务漂移问题。

9. **BadWAM: When World-Action Models Dream Right but Act Wrong**  
   [http://arxiv.org/abs/2607.15207v1](http://arxiv.org/abs/2607.15207v1)  
   Li, Yang, Wang et al.  
   ▶ 发现世界-动作模型（WAM）可能正确预测未来但生成错误动作，揭示耦合表示中的潜在安全隐患，对具身智能可靠性提出警告。

10. **AutoSynthesis: An agentic system for automated meta-analysis**  
    [http://arxiv.org/abs/2607.15247v1](http://arxiv.org/abs/2607.15247v1)  
    Taherinezhad, Maier, Vitagliano et al.  
    ▶ 端到端多智能体系统，实现从文献检索到效应量合并的自动元分析，显著提升证据合成的可扩展性。

11. **Plover: Steering GUI Agents through Plan-Centric Interaction**  
    [http://arxiv.org/abs/2607.15193v1](http://arxiv.org/abs/2607.15193v1)  
    Venkatesan, Wen, Guo et al.  
    ▶ 以计划为中心的 GUI 自动化框架，通过显式计划表示引导智能体，在动态界面中减少漂移，提升任务完成鲁棒性。

### 🔧 方法与框架（新技术、基准测试、效率优化）

12. **Subjective Risk Decomposition: A New View for Uncertainty Quantification**  
    [http://arxiv.org/abs/2607.15196v1](http://arxiv.org/abs/2607.15196v1)  
    Alamri, Caprio, Brown  
    ▶ 将不确定性度量视为高阶建模决策的衍生物，通过主观风险分解导出认知和偶然不确定性，提供了更统一的框架。

13. **RTS Smoother-Guided Learning of Physics-Based Neural Differential Models**  
    [http://arxiv.org/abs/2607.15180v1](http://arxiv.org/abs/2607.15180v1)  
    Demirkaya, Stratis, Imbiriba et al.  
    ▶ 结合 RTS 平滑器与神经微分方程，从部分观测数据中学习混合物理-神经网络模型，适用于仅有部分状态可测的动力系统。

14. **NeuronSoup: Evolving Asynchronous, Shared-Neuron Temporal Graphs without Backpropagation**  
    [http://arxiv.org/abs/2607.15217v1](http://arxiv.org/abs/2607.15217v1)  
    Kalia  
    ▶ 提出异步、延迟介导的神经网络架构，通过共享神经元池和演化策略替代反向传播，为类脑计算提供新思路。

### 📊 应用（垂直领域、多模态、代码生成）

15. **SceneBind: Binding What and Where Across Vision, Audio and Language**  
    [http://arxiv.org/abs/2607.15265v1](http://arxiv.org/abs/2607.15265v1)  
    Chen, Cui, Zhang et al.  
    ▶ 提出跨视觉、音频和语言的全面全模态表示，同时理解场景中“有什么”和“在哪里”，填补现有 omni-modal 编码器的空间结构缺失。

16. **MedFailBench: A Clinician-Built Open-Source Benchmark for Medical AI Safety Boundary Inspection**  
    [http://arxiv.org/abs/2607.15166v1](http://arxiv.org/abs/2607.15166v1)  
    Ozkan  
    ▶ 由临床医生构建的医疗 AI 失败基准，按严重程度和安全门类型标注错误，推动模型从“知道答案”转向“知道边界”。

17. **Grokipedia vs Wikipedia: An LLM-Based Audit of Political Neutrality along Ideologies**  
    [http://arxiv.org/abs/2607.15146v1](http://arxiv.org/abs/2607.15146v1)  
    Vlahos, Bied, De Bie  
    ▶ 首项对 LLM 生成百科（Grokipedia）与 Wikipedia 的政治中立性大规模审计，揭示意识形态偏差，具有重要社会意义。

18. **Symbal: Detecting Systematic Misalignments in Model-Generated Captions**  
    [http://arxiv.org/abs/2607.15216v1](http://arxiv.org/abs/2607.15216v1)  
    Varma, Delbrouck, Ostmeier et al.  
    ▶ 系统性地检测多模态大模型图像描述中的“系统性偏差”，即与特定视觉属性紧密关联的重复错误，提升多模态对齐质量。

## 研究趋势信号

今日投稿中观察到以下新兴方向：  
1) **统计自一致性**：将语言模型视为贝叶斯推断机器，深入理论化 in-context learning 的概率基础；  
2) **超长上下文智能体**：机器人策略和搜索代理均开始探索数千步的长程记忆与上下文缩放；  
3) **世界-动作耦合缺陷分析**：对具身模型展开批评性检查，揭示“预测正确但行为错误”的风险；  
4) **AI 安全评估范式转变**：从单点准确率转向成本感知、边界检测、安全门分级等多维度评价；  
5) **多智能体科学自动化**：自动元分析、自动脑研究等系统成为 agentic AI 的重要落地场景；  
6) **低资源语言词汇扩展**：结合深度学习与传统语言学方法，提升非拉丁文字语言的模型表现；  
7) **LLM 政治中立性审计**：社会计算方向持续升温，利用 LLM 评估 LLM 生成的百科内容成为新课题。

## 值得精读

- **Partition, Prompt, Aggregate** — 该论文为理解上下文学习提供了严谨的统计学框架，将概率自一致性条件化，对 LLM 校准、不确定性估计及安全部署具有深远影响，值得精读其理论推导部分。  
- **RoboTTT** — 将测试时训练技术引入机器人策略，实现了前所未有的大规模上下文缩放，方法设计清晰（TTT-MLP 与 TTT-Linear），实验充分，代表了机器人基础模型的重要进展。  
- **BadWAM** — 通过精心设计的实验揭示了世界-动作模型的系统性失败模式（“dream right, act wrong”），对于所有从事具身智能和世界模型研究的学者而言，这是一篇必须一读的“提醒”式论文。

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*