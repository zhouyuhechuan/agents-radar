# ArXiv AI Research Digest 2026-06-10

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-06-10 02:43 UTC

---

# Structured ArXiv AI Research Digest — 2026-06-10

## Today’s Highlights

Supervised fine-tuning (SFT) receives a unifying theoretical lens that challenges the conventional one-hot target paradigm, while a phase diagram for multimodal learning provides systematic guidance on when alignment or prediction is optimal. Several papers expose hidden costs of turning instruction-tuned LLMs into reasoning models—attention amnesia in hybrid architectures and degraded alignment safety—prompting urgent re-evaluation of post-training practices. On the agent front, test-time prompt learning and long-horizon professional-workflow benchmarks mark a shift from static evaluations to dynamic, real-world agent assessment. Finally, novel approaches to audio internalization (LoRA-based) and controlled reasoning steering open promising new avenues for model control and multimodal integration.

## Key Papers

### 🧠 Large Language Models

- **A Unifying Lens on Supervised Fine-Tuning Through Target Distribution Design** ([2606.11189v1](http://arxiv.org/abs/2606.11189v1))  
  *Tong Xie, Yuanhao Ban, Yunqi Hong et al.*  
  Challenges the default token-level likelihood maximization in SFT and proposes a principled target distribution framework—a foundational contribution that could reshape post-training practice.

- **When to Align, When to Predict: A Phase Diagram for Multimodal Learning** ([2606.11190v1](http://arxiv.org/abs/2606.11190v1))  
  *Ilay Kamai, Hugues Van Assel, Aviv Regev et al.*  
  Provides the first systematic understanding of when cross-modal alignment versus prediction succeeds or fails, giving practitioners a map for multimodal representation learning.

- **Predicting Future Behaviors in Reasoning Models Enables Better Steering** ([2606.11172v1](http://arxiv.org/abs/2606.11172v1))  
  *Evgenii Kortukov, Piotr Komorowski, Florian Klein et al.*  
  Proposes to steer large reasoning models by predicting future behavior from internal features, offering more stable control than current intervention methods.

- **Attention Amnesia in Hybrid LLMs: When CoT Fine-Tuning Breaks Long-Range Recall, and How to Fix It** ([2606.11052v1](http://arxiv.org/abs/2606.11052v1))  
  *Xinyu Zhou, Boyu Zhu, Yi Xu et al.*  
  Reveals that chain-of-thought SFT systematically degrades long-context recall in hybrid linear-attention models—a critical finding for reasoning model deployments.

- **Does Reasoning Preserve Alignment? On the Trustworthiness of Large Reasoning Models** ([2606.11046v1](http://arxiv.org/abs/2606.11046v1))  
  *Prajakta Kini, Avinash Reddy, Souradip Chakraborty et al.*  
  Shows that converting instruction-tuned LLMs into reasoning models can erode safe refusal behaviors, raising urgent safety concerns for reasoning model adoption.

### 🤖 Agents & Reasoning

- **EEVEE: Towards Test-time Prompt Learning in the Real World for Self-Improving Agents** ([2606.11182v1](http://arxiv.org/abs/2606.11182v1))  
  *Weixian Xu, Shilong Liu, Mengdi Wang*  
  First multi-dataset test-time prompt learning framework for LLM agents, enabling adaptation to heterogeneous real-world task streams without retraining.

- **A History-Aware Visually Grounded Critic for Computer Use Agents** ([2606.11078v1](http://arxiv.org/abs/2606.11078v1))  
  *Jaewoo Lee, Zaid Khan, Archiki Prasad et al.*  
  Introduces a critic model that leverages interaction history and visual context to evaluate pre-execution actions, significantly boosting computer-use agent reliability.

- **T1-Bench: Benchmarking Multi-Scenario Agents in Real-World Domains** ([2606.11070v1](http://arxiv.org/abs/2606.11070v1))  
  *Genta Indra Winata, Amartya Chakraborty, Yuzhen Lin et al.*  
  A comprehensive benchmark covering diverse professional domains with realistic, multi-step agent tasks—sets a new standard for agent evaluation.

- **Workflow-GYM: Towards Long-Horizon Evaluation of Computer-use Agentic tasks in Real-World Professional Fields** ([2606.11042v1](http://arxiv.org/abs/2606.11042v1))  
  *Liya Zhu, Jingzhe Ding, Jian Zhang et al.*  
  Evaluates GUI-based agents on long-horizon, high-value workflows (e.g., accounting, design) with verifiable outcomes, filling a critical gap in agent assessment.

- **ABC-Bench: An Agentic Bio-Capabilities Benchmark for Biosecurity** ([2606.11150v1](http://arxiv.org/abs/2606.11150v1))  
  *Andrew Bo Liu, Samira Nedungadi, Bryce Cai et al.*  
  Measures LLM agents’ ability to perform in silico biology tasks, providing a necessary safety benchmark for dual-use capabilities.

- **The Shibboleth Effect: Auditing the Cross-Lingual Distributional Skew of Large Language Models** ([2606.11082v1](http://arxiv.org/abs/2606.11082v1))  
  *Hakan Mehmetcik*  
  Uses a multi-agent geopolitical wargame to expose severe cross-lingual performance skews in frontier LLMs—important for equitable deployment.

### 🔧 Methods & Frameworks

- **ReasonAlloc: Hierarchical Decoding-Time KV Cache Budget Allocation for Reasoning Models** ([2606.11164v1](http://arxiv.org/abs/2606.11164v1))  
  *Wenhao Liu, Hao Shi, Yunhe Li et al.*  
  Introduces a hierarchical budget allocation for key-value cache during decoding, dramatically reducing memory overhead for long CoT reasoning without performance loss.

- **Provenance-Grounded Gating and Adaptive Recovery in Synthetic Post-Training Data Curation** ([2606.11127v1](http://arxiv.org/abs/2606.11127v1))  
  *Soham Bhattacharjee, Karun Sharma, Vinay Kumar Sankarapu et al.*  
  Proposes a filtering mechanism that grounds rejection signals in source evidence and recovers rejected samples adaptively—practical and principled synthetic data curation.

- **Itô maps for any-step SDEs** ([2606.11156v1](http://arxiv.org/abs/2606.11156v1))  
  *Zhengkai Pan, Peter Potaptchik, Wenxi Yao et al.*  
  Extends deterministic flow distillation to stochastic dynamics via Itô maps, enabling exact distillation for score-based and diffusion models.

- **TRACE: A Unified Rollout Budget Allocation Framework for Efficient Agentic Reinforcement Learning** ([2606.11119v1](http://arxiv.org/abs/2606.11119v1))  
  *Heming Zou, Qi Wang, Yun Qu et al.*  
  Addresses rollout inefficiency in RL with verifiable rewards (RLVR) by dynamically allocating budget based on reward contrast, improving sample efficiency for reasoning and agent training.

### 📊 Applications

- **AuRA: Internalizing Audio Understanding into LLMs as LoRA** ([2606.11033v1](http://arxiv.org/abs/2606.11033v1))  
  *Bo Cheng, Lei Shi, Zhanyu Ma et al.*  
  A lightweight LoRA-based method to internalize audio understanding directly into LLMs, bypassing cascaded ASR pipelines—promising for efficient speech-language integration.

## Research Trend Signal

A clear convergence of themes emerges: **reasoning models** are under intense scrutiny. Multiple papers simultaneously address steering (Paper 6), memory degradation (Paper 45), alignment preservation (Paper 46), and inference efficiency (Paper 11). This suggests the field is maturing beyond simply adding "think step-by-step

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*