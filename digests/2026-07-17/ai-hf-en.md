# Hugging Face Trending Models Digest 2026-07-17

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-17 01:59 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-07-17

## Today's Highlights

This week's trending models center on two dominant forces: **extreme quantization pushing deployment boundaries** and **the Qwen family becoming the de facto base for vision-language fine-tuning**. The most striking launch is **zai-org/GLM-5.2** (4,029 likes), a massive MoE model that signals China's continued push into open-weight frontier models. Equally notable is **prism-ml's Bonsai series**, where 1-bit and ternary quantizations of a 27B model are seeing massive download counts (559K+ for Bonsai-27B-gguf), indicating real-world appetite for running capable LLMs on consumer hardware. Meanwhile, **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** leads raw downloads at over 2 million, showing the community is eagerly adopting Qwen3.5-based fine-tunes for reasoning tasks. The vision-language trend is unmistakable: 10 of the top 30 models carry `image-text-to-text` pipelines, up sharply from previous weeks.

---

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** — thinkingmachines | Likes: 812 | Downloads: 4 — A new image-text-to-text conversational model built on an "Inkling" multimodal architecture, trending for its claim of improved visual reasoning despite very early-stage downloads.

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | Likes: 4,029 | Downloads: 513,061 — A MoE-based text-generation model from Zhipu AI, trending as one of the highest-liked releases this week, signaling strong interest in Chinese open-weight MoE architectures.

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** — tencent | Likes: 813 | Downloads: 11,849 — Tencent's third-generation Hunyuan model (Hy-V3), a text-generation LLM gaining traction for its enterprise-grade performance and Tencent's backing.

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — InternScience | Likes: 568 | Downloads: 33,400 — A Qwen3.5-based MoE model designed for agentic workflows, trending as the community explores specialized agent models.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking)** — GnLOLot | Likes: 131 | Downloads: 4,117 — A tiny 1B parameter thinking model fine-tuned from MiniCPM5, notable for packing chain-of-thought reasoning into a sub-2B footprint.

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — deepreinforce-ai | Likes: 902 | Downloads: 1,785,575 — A 35B GGUF-quantized text-generation model with MIT license, trending for its strong endpoint compatibility and massive download count.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | Likes: 2,237 | Downloads: 2,042,670 — The most-downloaded model this week: a Qwen3.5-based vision-language model GGUF-quantized and fine-tuned for reasoning, trending due to its combination of vision capability and efficient deployment.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | Likes: 2,787 | Downloads: 2,328,315 — An uncensored Qwen3.6-based MoE vision model with aggressive fine-tuning, trending for its large vision-language MoE architecture and high download volume.

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** — ATH-MaaS | Likes: 136 | Downloads: 3,678 — A Qwen3.5-based OCR-specific vision model, trending for specialized document understanding.

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | Likes: 2,010 | Downloads: 1,852,722 — Baidu's unlimited OCR model with a feature-extraction pipeline, trending for breaking OCR accuracy benchmarks and strong enterprise adoption.

- **[unsloth/Qwen3.6-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.6-27B-NVFP4)** — unsloth | Likes: 216 | Downloads: 1,712,974 — An unsloth-optimized NVFP4 quantization of Qwen3.6-27B, trending for efficient vision-language inference on NVIDIA hardware.

- **[Wan-AI/Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)** — Wan-AI | Likes: 92 | Downloads: 1,884 — An image-to-video generation model using diffusers, trending for dance video generation and reference-based animation.

- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** — Alissonerdx | Likes: 167 | Downloads: 0 — A text-to-video LoRA focused on identity preservation, trending for personalized video generation with LTX.

- **[Cseti/LTX2.3-22B_IC-LoRA-CrossView-Prompt](https://huggingface.co/Cseti/LTX2.3-22B_IC-LoRA-CrossView-Prompt)** — Cseti | Likes: 77 | Downloads: 0 — An IC-LoRA for novel-view synthesis in video generation, trending for multi-view video research.

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — OpenMOSS-Team | Likes: 232 | Downloads: 75,105 — An audio-text-to-text model for transcription and speaker diarization, trending for real-time meeting transcription use cases.

### 🔧 Specialized Models (code, math, OCR, agentic, embeddings)

- **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** — Cactus-Compute | Likes: 248 | Downloads: 733 — A JAX-based model for function calling and tool use, trending for its specialized agentic capabilities with JAX backend.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 | Likes: 1,208 | Downloads: 506,068 — A GGUF-quantized Gemma 4-based agentic model fine-tuned for coding and terminal use, trending for practical developer tooling.

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — froggeric | Likes: 924 | Downloads: 0 — A utility model providing corrected Jinja chat templates for Qwen3.5 models, trending as a community fix for common template issues.

- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** — conradlocke | Likes: 322 | Downloads: 0 — A LoRA for image editing with identity preservation based on Krea-2, trending for controllable face editing in ComfyUI.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ, MLX)

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — prism-ml | Likes: 607 | Downloads: 74,007 — A 2-bit ternary quantization of a 27B model, trending as the first production-ready ternary LLM GGUF with llama.cpp support.

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — prism-ml | Likes: 341 | Downloads: 559,267 — A 1-bit quantization of a 27B model, trending for enabling LLM inference on extremely resource-constrained devices.

- **[empero-ai/Qwythos-9B-v2-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-v2-GGUF)** — empero-ai | Likes: 150 | Downloads: 89,107 — The GGUF quantization of the Qwythos-9B-v2 vision-language model, trending alongside its sister model for fine-tuned vision reasoning.

- **[empero-ai/Qwythos-9B-v2](https://huggingface.co/empero-ai/Qwythos-9B-v2)** — empero-ai | Likes: 129 | Downloads: 6,220 — The base safetensors version of Qwythos-9B-v2, a Qwen3.5 fine-tune for vision-language tasks.

- **[AngelSlim/Hy3-GGUF](https://huggingface.co/AngelSlim/Hy3-GGUF)** — AngelSlim | Likes: 117 | Downloads: 80,796 — Community GGUF quantization of Tencent's Hy3 model, trending for making Hy3 accessible on llama.cpp.

- **[jlnsrk/GLM-5.2-colibri-int4](https://huggingface.co/jlnsrk/GLM-5.2-colibri-int4)** — jlnsrk | Likes: 119 | Downloads: 2,621 — An int4 CPU-optimized quantization of GLM-5.2 using expert-streaming (Colibri), trending for on-device MoE deployment.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)** — GnLOLot | Likes: 264 | Downloads: 121,296 — GGUF versions of the 1B thinking model, trending for chain-of-thought reasoning on edge devices.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF)** — GnLOLot | Likes: 95 | Downloads: 3,691 — V2 GGUF of the 1B thinking model, iterating on reasoning improvements.

- **[prism-ml/Ternary-Bonsai-27B-mlx-2bit](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-mlx-2bit)** — prism-ml | Likes: 84 | Downloads: 7,622 — MLX port of the ternary Bonsai quantization, trending for Apple Silicon deployment.

- **[prism-ml/Bonsai-27B-mlx-1bit](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)** — prism-ml | Likes: 82 | Downloads: 10,760 — MLX port of the 1-bit Bonsai model, enabling extreme quantization on Mac hardware.

---

## Ecosystem Signal

The clearest signal this week is **Qwen's market dominance**: 8 of the top 30 models are explicitly Qwen3.5 or Qwen3.6 based, spanning vision-language models, MoE variants, chat templates, and GGUF quantizations. The Qwen ecosystem now functions as a platform, not just a model—community members build fine-tunes, fix templates, and create quantizations independently.

**Extreme quantization has gone mainstream.** The Bonsai series (1-bit and ternary) represents a new category: models that are nearly unusable in theory (1-bit weights) but function well enough in practice that users are downloading them by the hundreds of thousands. This suggests real demand for on-device inference where model quality tradeoffs are acceptable for reduced memory.

**Open-weight models continue to eclipse proprietary fine-tunes.** While models like Gemma 4 and MiniCPM5 appear, the community overwhelmingly prefers Qwen-based foundations—likely due to permissive licenses (MIT/Apache-2.0) and strong base models.

**MoE architectures are proliferating.** GLM-5.2, Qwen3.6-35B-A3B, InternScience/Agents-A1, and the Bonsai series all employ mixture-of-experts, indicating that the community has adopted MoE as the default architecture for efficient scaling.

**Video generation is emerging as a growth area.** LTX-based LoRAs (identity, cross-view) and Wan-AI's dancer model signal increasing interest in controllable video generation, though downloads remain low compared to text and vision models.

---

## Worth Exploring

1. **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — With 4,029 likes in a single week, this is the most influential model release of the period. It represents China's strongest open-weight MoE offering and uses a novel DSA (Dynamic Sparse Attention) mechanism. Worth studying for anyone tracking

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*