# ArXiv AI Research Digest 2026-07-15

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-07-15 01:45 UTC

---

# ArXiv AI Research Digest — 2026-07-15

## Today's Highlights

Today's submissions reveal a strong push toward *mechanistic interpretability and internal-state analysis* of large models, with two notable papers providing representation-level accounts of LLM judges and state-space model routing. A second major thread is **safety vulnerabilities in deployed multi-agent systems**, particularly a striking demonstration that distributed backdoors can evade per-message monitoring. On the theoretical side, new work offers a unified framework for inductive reasoning dynamics in Transformers and an exact instrument for Mamba state analysis. Finally, we see a surge in **frugal and self-supervised compression techniques**, including a novel method that uses self-generated training data to push model compression beyond prior limits.

---

## Key Papers

### 🧠 Large Language Models (architecture, training, alignment, evaluation)

**1. Metacognition in LLMs: Foundations, Progress, and Opportunities**
http://arxiv.org/abs/2607.11881v1 — *Gabrielle Kaili-May Liu et al.*
A comprehensive survey arguing that metacognition—often overlooked in LLM research—is a foundational capability for transparent, self-aware AI systems, and maps progress and open challenges.

**2. Inside the Unfair Judge: A Mechanistic Interpretability Account of LLM-as-Judge Bias**
http://arxiv.org/abs/2607.11871v1 — *Zixiang Xu et al.*
Provides a *representation-level* explanation for scoring biases in LLM judges, showing that bias patterns are encoded in hidden states, offering a path beyond input-level mitigation.

**3. An Exact Instrument for State Usage in Selective State-Space Models, and the Input-Driven Migration It Reveals**
http://arxiv.org/abs/2607.11796v1 — *Raktim Bhattacharya*
Introduces a precise measurement tool for how Mamba models use their first-order modes, revealing that activated modes shift dynamically based on input content—a key insight for understanding state-space model internals.

**4. Invariant Learning Dynamics of Transformers in Inductive Reasoning Tasks**
http://arxiv.org/abs/2607.11875v1 — *Tiberiu Musat et al.*
Provides a theoretical framework unified across multiple inductive tasks, explaining how Transformers develop reasoning abilities during training with testable predictions about learning trajectories.

**5. How Temperature Shapes Ideological Discourse in Retrieval-Augmented Generation?**
http://arxiv.org/abs/2607.11783v1 — *Elmira Salari et al.*
Shows that the temperature parameter in RAG systems can amplify or suppress ideological biases in retrieved content, a previously overlooked source of output polarization.

---

### 🤖 Agents & Reasoning (planning, tool use, multi-agent, chain-of-thought)

**6. MM-ToolSandBox: A Unified Framework for Evaluating Visual Tool-Calling Agents**
http://arxiv.org/abs/2607.11818v1 — *Kaixin Ma et al.*
A benchmark with 500+ tools across 16 domains for visually grounded tool-calling agents, enabling multi-image, multi-turn evaluation where agents must accumulate evidence across interactions.

**7. When Local Monitors Miss Compositional Harm: Diagnosing Distributed Backdoors in Multi-Agent Systems**
http://arxiv.org/abs/2607.11751v1 — *Yibo Hu, Ren Wang*
Demonstrates a critical vulnerability: harmful payloads can be split across agents so that per-message monitors pass, while the assembled action is malicious—a fundamental blind spot in current safety nets.

**8. Think Through a Bottleneck: Hourglass Reasoning for Rigorous Induction**
http://arxiv.org/abs/2607.11696v1 — *Huan Zhu*
Shows that enforcing a structural bottleneck between reasoning stages—forcing information through a compressed representation—significantly improves few-shot inductive reasoning over standard self-refinement.

**9. An Explainable Agentic System for Detection of Conversational Scams with Summary-Based Memory**
http://arxiv.org/abs/2607.11707v1 — *Ahmed Omar Salim Adnan et al.*
A multi-agent detection system for long-duration conversational scams that uses summary-based memory to maintain context across weeks of interaction, with built-in explainability.

---

### 🔧 Methods & Frameworks (new techniques, benchmarks, efficiency improvements)

**10. Requential Coding: Pushing the Limits of Model Compression with Self-Generated Training Data**
http://arxiv.org/abs/2607.11883v1 — *Shikai Qiu et al.*
Achieves state-of-the-art compression by having a model generate its own compact training codes, leveraging the principle that compression and generalization are deeply linked.

**11. From Global to Factor-Wise Expert Composition in Discrete Diffusion Models**
http://arxiv.org/abs/2607.11758v1 — *Haozhe Huang et al.*
Introduces factor-wise expert composition for discrete diffusion, enabling modular reasoning that generalizes beyond joint training data—a step toward compositional generative reasoning.

**12. LoRA-Based Cascaded Multimodal Fusion for Action Recognition in Medical Training Environments**
http://arxiv.org/abs/2607.11839v1 — *Divya Mereddy et al.*
A parameter-efficient, cascaded fusion framework for multimodal action recognition in healthcare training, showing that sequential, LoRA-based adaptation can match or exceed full fine-tuning.

**13. From Expressivity to Sample Complexity: Narrow Teachers for Transformers via C-RASP**
http://arxiv.org/abs/2607.11760v1 — *Michael Rizvi-Martel et al.*
Bridges expressivity and sample complexity by constructing narrow (small-width) Transformers that can serve as teachers for larger models, providing theoretical guarantees on learnability.

**14. HiFi-LLP: High-Fidelity, Low-Cost Latency Predictors with Confidence for Robust HW-NAS**
http://arxiv.org/abs/2607.11746v1 — *Shambhavi Balamuthu Sampath et al.*
Provides hardware-aware latency predictors that are both accurate and confidence-aware, enabling more robust neural architecture search for edge deployment.

**15. How to Tame Grokking: Representation Geometry as a Control Signal**
http://arxiv.org/abs/2607.11666v1 — *Maksim A Kazanskii*
Finds that the geometric properties of learned representations can serve as early indicators and control signals for grokking, potentially allowing practitioners to predict or accelerate the delayed generalization phenomenon.

---

### 📊 Applications (domain-specific, multimodal, code generation)

**16. AdvancedMathBench: A Benchmark Suite for Advanced Mathematical Proof Generation and Verification**
http://arxiv.org/abs/2607.11849v1 — *Lingkai Kong et al.*
A comprehensive benchmark spanning graduate-level mathematics, testing LLMs' ability to generate and verify formal proofs across multiple mathematical disciplines.

**17. Evidence-Backed Video Question Answering**
http://arxiv.org/abs/2607.11862v1 — *Shijie Wang et al.*
Introduces verifiable visual grounding for Video LLMs, moving beyond black-box Q&A to produce outputs backed by spatiotemporal evidence in video.

**18. STEP: Career-Path Recommendation via Temporal and Educational Trajectory Modeling**
http://arxiv.org/abs/2607.11722v1 — *Iman Johary et al.*
Models career transitions as temporal trajectories from unstructured resume data, enabling personalized career path recommendations grounded in real labor market patterns.

**19. A multi-scale feature enhanced graph neural network for fluid dynamics prediction in complex geometries**
http://arxiv.org/abs/2607.11672v1 — *Li Xiao et al.*
A GNN architecture that captures multi-scale flow features for predicting fluid dynamics in complex geometries, offering substantial speedups over traditional CFD simulations.

**20. Imputation-free transformer learning enables robust Alzheimer's disease prediction and calibrated uncertainty quantification across heterogeneous clinical cohorts**
http://arxiv.org/abs/2607.11656v1 — *Christelle Schneuwly Diaz et al.*
A transformer-based approach that handles missing clinical data natively (without imputation), enabling robust Alzheimer's prediction with well-calibrated uncertainty across diverse real-world cohorts.

---

## Research Trend Signal

Several emerging directions stand out from today's submissions. **Mechanistic interpretability is moving from post-hoc analysis to predictive control**: the Mamba state instrument (Bhattacharya), the LLM-as-judge hidden-state bias account (Xu et al.), and the grokking representation-geometry control signal (Kazanskii) all point toward a future where we can *diagnose and intervene* in model internals at runtime. Meanwhile, **multi-agent safety is undergoing a stress test**—the distributed backdoor paper (Hu & Wang) and the agent-hacks-agent red-teaming framework (Mao et al.) reveal that current per-message safety monitors are fundamentally inadequate for compositional agent behaviors. On the methods side, **frugal AI** continues to gain traction: LoRA-based cascaded fusion, self-generated compression codes, and cost-effective latency predictors all suggest that the field is actively seeking to decouple capability from compute. Finally, **benchmarks are becoming more rigorous and domain-specific**, with AdvancedMathBench, the visual tool-calling sandbox, and the speech spoofing detection benchmark (VoxENES 2026) each raising the bar for evaluation in their respective domains.

---

## Worth Deep Reading

**1. "Metacognition in LLMs: Foundations, Progress, and Opportunities"** (Liu et al.)
This survey is likely to become a reference point for an emerging subfield. By framing metacognition—knowing about one's own knowledge and reasoning—as a missing capability in LLMs, it connects psychology, AI alignment, and interpretability in a way that has both immediate practical implications (self-correction, calibration) and long-term research directions.

**2. "Inside the Unfair Judge: A Mechanistic Interpretability Account of LLM-as-Judge Bias"** (Xu et al.)
This paper shifts the debate on LLM evaluation bias from "what perturbations affect scores" to "where and how bias lives in model representations." It opens the door for representation-level debiasing techniques and provides a methodology that could generalize to other forms of model bias.

**3. "When Local Monitors Miss Compositional Harm: Diagnosing Distributed Backdoors in Multi-Agent Systems"** (Hu & Wang)
This is an urgent safety contribution. As multi-agent LLM systems move toward production, the demonstrated vulnerability—harm that is invisible at the message level but catastrophic at the assembly level—demands new, compositional monitoring architectures. The paper's impact extends beyond its specific attack to highlight a fundamental blind spot in current agent safety infrastructure.

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*