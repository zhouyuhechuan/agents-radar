# Hugging Face Trending Models Digest 2026-07-23

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-23 02:04 UTC

---

Here is the structured digest of the top trending Hugging Face models for July 23, 2026.

---

### 1. Today's Highlights

This week’s trends are defined by the rapid rise of ternary and 1-bit quantization (especially the **prism-ml** family and **DavidAU** merges) alongside the explosive popularity of vision-language MoE models like **GLM-5.2** and **Qwen3.6-35B-A3B**. Google’s **gemma-4-31B-it** continues to dominate raw download velocity, while the ecosystem sees a significant push toward specialized robotics and identity-preserving generation models. The community is heavily engaged in "uncensored" fine-tunes and aggressive quantization, with GGUF formats continuing to be the primary vehicle for local deployment.

### 2. Trending Models

#### 🧠 Language Models (LLMs, chat models, instruction-tuned)
- **zai-org/GLM-5.2** ([link](https://huggingface.co/zai-org/GLM-5.2)) — Author: zai-org | Likes: 4,339 | Downloads: 545,109. A next-generation MoE model with dynamic sparse attention (DSA); trending for its massive community adoption and strong reasoning performance.
- **upstage/Solar-Open2-250B** ([link](https://huggingface.co/upstage/Solar-Open2-250B)) — Author: upstage | Likes: 263 | Downloads: 0. A 250B open-weight model; trending for its scale and the promise of an open competitor to proprietary giants.
- **Nanbeige/Nanbeige4.2-3B** ([link](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)) — Author: Nanbeige | Likes: 234 | Downloads: 0. A compact 3B LLM from a rising Chinese lab; notable for its efficiency in a landscape shifting toward smaller, capable models.
- **Motif-Technologies/Motif-3-Beta** ([link](https://huggingface.co/Motif-Technologies/Motif-3-Beta)) — Author: Motif-Technologies | Likes: 161 | Downloads: 125. An early-stage feature extraction model; trending due to speculative interest in its architectural innovations.
- **GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF** ([link](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF)) — Author: GnLOLot | Likes: 153 | Downloads: 51,746. A 1B "thinking" model distilled from larger sources; popular for its tiny footprint and reported reasoning capabilities.

#### 🎨 Multimodal & Generation (image, video, audio, text-to-X)
- **baidu/Unlimited-OCR** ([link](https://huggingface.co/baidu/Unlimited-OCR)) — Author: baidu | Likes: 2,716 | Downloads: 2,237,351. A state-of-the-art OCR model; trending for its utility in document processing and massive download count.
- **google/gemma-4-31B-it** ([link](https://huggingface.co/google/gemma-4-31B-it)) — Author: google | Likes: 3,328 | Downloads: 12,113,203. The latest open-weight flagship from Google; dominating downloads due to its strong performance and permissive license.
- **conradlocke/krea2-identity-edit** ([link](https://huggingface.co/conradlocke/krea2-identity-edit)) — Author: conradlocke | Likes: 497 | Downloads: 0. A LoRA for identity-preserving image editing on Krea-2; trending in the ComfyUI community for face-swap and edit tasks.
- **microsoft/Mage-Flow** ([link](https://huggingface.co/microsoft/Mage-Flow)) — Author: microsoft | Likes: 126 | Downloads: 0. A new text-to-image/editing pipeline from Microsoft; notable for its unified diffusion framework.
- **nvidia/Cosmos3-Edge** ([link](https://huggingface.co/nvidia/Cosmos3-Edge)) — Author: nvidia | Likes: 90 | Downloads: 6,623. An edge-optimized Cosmos diffusion model; relevant for on-device generation.
- **Alissonerdx/LTX-Best-Face-ID** ([link](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)) — Author: Alissonerdx | Likes: 235 | Downloads: 0. A LoRA for identity preservation in text-to-video generation; trending for its reference-to-video capability.

#### 🔧 Specialized Models (code, math, medical, embeddings, robotics, ASR)
- **openbmb/MiniCPM-RobotManip** ([link](https://huggingface.co/openbmb/MiniCPM-RobotManip)) — Author: openbmb | Likes: 154 | Downloads: 58. A Vision-Language-Action (VLA) model for robotic manipulation; a key signal of the VLA trend.
- **openbmb/MiniCPM-RobotTrack** ([link](https://huggingface.co/openbmb/MiniCPM-RobotTrack)) — Author: openbmb | Likes: 114 | Downloads: 72. A companion VLA model for object tracking in robotics; part of the growing "robot foundation model" push.
- **moonshotai/Kimi-K2.7-Code** ([link](https://huggingface.co/moonshotai/Kimi-K2.7-Code)) — Author: moonshotai | Likes: 1,225 | Downloads: 722,058. A specialized code model using compressed tensors; trending for its strong coding benchmarks and efficient architecture.
- **nvidia/nemotron-3.5-asr-streaming-0.6b** ([link](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)) — Author: nvidia | Likes: 914 | Downloads: 590,230. A streaming ASR model with a compact 0.6B size; dominating speech recognition downloads.
- **OpenMOSS-Team/MOSS-Transcribe-Diarize** ([link](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)) — Author: OpenMOSS-Team | Likes: 308 | Downloads: 92,265. An audio-to-text model combining transcription and speaker diarization; useful for meeting analysis.

#### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)
- **prism-ml/Ternary-Bonsai-27B-gguf** ([link](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)) — Author: prism-ml | Likes: 946 | Downloads: 432,196. A 2-bit ternary GGUF; leading the "extreme compression" trend for running large models on consumer hardware.
- **prism-ml/Bonsai-27B-gguf** ([link](https://huggingface.co/prism-ml/Bonsai-27B-gguf)) — Author: prism-ml | Likes: 596 | Downloads: 1,404,962. A 1-bit GGUF of Bonsai-27B; extremely popular for its insane compression ratio.
- **DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF** ([link](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)) — Author: DavidAU | Likes: 323 | Downloads: 62,842. A heavily merged, uncensored GGUF fine-tune; representative of the "uncensored" fine-tuning subculture.
- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** ([link](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)) — Author: HauhauCS | Likes: 3,003 | Downloads: 1,997,690. A MoE vision model aggressively quantized to GGUF; trending for its uncensored nature and massive download count.
- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** ([link](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)) — Author: empero-ai | Likes: 2,417 | Downloads: 2,133,420. A GGUF of a heavily merged reasoning model; one of the most downloaded models this week.
- **bottlecapai/ThinkingCap-Qwen3.6-27B** ([link](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)) — Author: bottlecapai | Likes: 514 | Downloads: 12,002. A fine-tune enhancing the reasoning capabilities of Qwen3.6-27B; popular for its "thinking" behavior.
- **poolside/Laguna-S-2.1** variants ([link](https://huggingface.co/poolside/Laguna-S-2.1), [GGUF](https://huggingface.co/poolside/Laguna-S-2.1-GGUF), [NVFP4](https://huggingface.co/poolside/Laguna-S-2.1-NVFP4), [Unsloth variant](https://huggingface.co/unsloth/Laguna-S-2.1-GGUF)) — Author: poolside | Likes: ~100-400 each. A code-focused model family released in multiple formats; trending due to active quantization (GGUF, NVFP4) and Unsloth support.
- **unsloth/inkling-GGUF** ([link](https://huggingface.co/unsloth/inkling-GGUF)) — Author: unsloth | Likes: 120 | Downloads: 7,377. A GGUF of **thinkingmachines/Inkling**, a MoE vision model; popular for enabling local deployment of a top-ranked multimodal model.

### 3. Ecosystem Signal

The ecosystem is currently defined by three major trends: **extreme quantization**, **MoE dominance**, and **community-driven fine-tuning**. The **prism-ml** family of Bonsai models (1-bit and ternary) is leading a paradigm shift where 27B parameters fit on a laptop, making large models accessible to consumers. This is complemented by a wave of **GGUF releases** for nearly every popular model, from Qwen3.6 variants to the new Laguna-S family.

**Open-weight momentum** is strong, with Google’s Gemma-4 and Upstage’s Solar-Open2-250B challenging proprietary leaders, while **GLM-5.2** demonstrates that community-favorite model families can rival corporate releases in engagement. **"Uncensored" fine-tunes** (like DavidAU’s merges and HauhauCS’s aggressive Qwen3.6 variant) represent a persistent sub-current, often gaining high likes and downloads despite their niche nature. Finally, the emergence of **vision-language-action (VLA)** models from openbmb signals a growing interest in grounding LLMs in physical interaction, a key direction for embodied AI.

### 4. Worth Exploring

1. **prism-ml/Ternary-Bonsai-27B-gguf** ([link](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)) — Worth studying as the current benchmark for extreme quantization. Understanding how ternary representations (1.58-bit equivalents) preserve coherence in a 27B model is critical for anyone working on on-device or edge AI deployment.

2. **zai-org/GLM-5.2** ([link](https://huggingface.co/zai-org/GLM-5.2)) — With the highest likes on this list, this MoE architecture with dynamic sparse attention warrants a deep dive. It represents a strong contender against mainstream architectures like LLaMA and Qwen, and its community enthusiasm suggests real performance gains.

3. **openbmb/MiniCPM-RobotManip** ([link](https://huggingface.co/openbmb/MiniCPM-RobotManip)) — A first-class signal of the next frontier: grounding LLMs in robotics. This Vision-Language-Action model is small enough to study and represents the convergence of multimodal and robotics research.

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*