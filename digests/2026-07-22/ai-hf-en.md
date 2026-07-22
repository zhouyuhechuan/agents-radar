# Hugging Face Trending Models Digest 2026-07-22

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-22 01:56 UTC

---

# Hugging Face Trending Models Digest — 2026-07-22

## Today’s Highlights
This week’s top movers showcase a clear tilt toward extreme quantization and MoE architectures. **GLM-5.2** (4.3K likes) and **Gemma-4-31B-it** (3.3K likes, 12M downloads) lead the popularity charts, while **prism-ml**’s ternary and 1-bit Bonsai variants demonstrate that ultra-low-bit inference is becoming mainstream. Multimodal OCR models (Baidu’s Unlimited-OCR, OvisOCR2) and robotics vision-language-action models (MiniCPM-RobotManip) signal growing infrastructure for real-world applications. Notably, an influx of “uncensored” Qwen3.6 fine-tunes (HauhauCS, DavidAU) and Claude-flavored thinking models (empero-ai, GnLOLot) reflect a strong community appetite for personalized, reasoning-oriented chat models.

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — *prism-ml* | ❤️ 899 | ⬇️ 432K  
  A 27B model quantized to 2-bit ternary weights, pushing the frontier of aggressive compression for CPU inference.

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — *zai-org* | ❤️ 4,281 | ⬇️ 545K  
  Zhipu AI’s latest MoE model with Dynamic Sparse Attention, trending for its strong reasoning and Chinese-language performance.

- **[poolside/Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1)** — *poolside* | ❤️ 194 | ⬇️ 3K  
  A 2.1 version of poolside’s code-oriented LLM, gaining traction among developers for software engineering tasks.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF)** — *GnLOLot* | ❤️ 147 | ⬇️ 52K  
  A 1B parameter thinking model GGUF – blends MiniCPM5 with Claude-inspired reasoning chains for efficient on-device use.

- **[Motif-Technologies/Motif-3-Beta](https://huggingface.co/Motif-Technologies/Motif-3-Beta)** — *Motif-Technologies* | ❤️ 127 | ⬇️ 125  
  A new transformer for feature extraction and generation, positioned as a modular foundation model.

- **[AngelSlim/Hy3-GGUF](https://huggingface.co/AngelSlim/Hy3-GGUF)** — *AngelSlim* | ❤️ 156 | ⬇️ 145K  
  Community GGUF of Tencent’s Hy3 model, popular for its Apache-2.0 license and strong performance per parameter.

- **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** — *Nanbeige* | ❤️ 77 | ⬇️ 0  
  A lightweight 3B LLM optimized for Chinese language tasks, newly released.

- **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** — *Cactus-Compute* | ❤️ 298 | ⬇️ 1K  
  A JAX-based model focused on function calling and tool use, appealing to agent workflows.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** — *thinkingmachines* | ❤️ 1,366 | ⬇️ 16K  
  A multimodal conversational model (image+text I/O) designed for interactive visual reasoning.

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — *baidu* | ❤️ 2,609 | ⬇️ 2.2M  
  Baidu’s end-to-end OCR model processing images to text, widely downloaded for document digitization.

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** — *DavidAU* | ❤️ 249 | ⬇️ 63K  
  A heavily fine-tuned 27B Qwen3.6 GGUF for uncensored vision-language tasks, part of a popular “Fable” series.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — *HauhauCS* | ❤️ 2,971 | ⬇️ 2M  
  One of the most downloaded uncensored Qwen3.6 MoE fine-tunes, blending vision and aggressive chat.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — *empero-ai* | ❤️ 2,388 | ⬇️ 2.1M  
  A reasoning-heavy 9B model (Qwen3.5 backbone) combined with Claude-inspired mythos, extremely popular in the GGUF community.

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** — *ATH-MaaS* | ❤️ 237 | ⬇️ 17K  
  A fine-tuned Qwen3.5 model specialized for OCR tasks, rivaling Baidu’s offering.

- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — *bottlecapai* | ❤️ 491 | ⬇️ 12K  
  A 27B multimodal model with enhanced “thinking” capabilities, built on Qwen3.6.

- **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** — *openbmb* | ❤️ 147 | ⬇️ 58  
  A vision-language-action model for robotic manipulation tasks, using MiniCPM backbone.

- **[unsloth/inkling-GGUF](https://huggingface.co/unsloth/inkling-GGUF)** — *unsloth* | ❤️ 116 | ⬇️ 7K  
  A quantized MoE GGUF of the Inkling model, supporting image, text, and audio inputs.

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — *OpenMOSS-Team* | ❤️ 299 | ⬇️ 92K  
  A speech-to-text model with speaker diarization, built on the MOSS architecture.

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — *moonshotai* | ❤️ 1,200 | ⬇️ 722K  
  Code-specialized version of Kimi K2.5 with compressed tensors, supporting image + code understanding.

- **[openbmb/MiniCPM-RobotTrack](https://huggingface.co/openbmb/MiniCPM-RobotTrack)** — *openbmb* | ❤️ 107 | ⬇️ 72  
  A companion model to RobotManip for object tracking in robotic vision-action pipelines.

- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — *google* | ❤️ 3,314 | ⬇️ 12.1M  
  Google’s latest open-weight multimodal model, instruction-tuned, dominating downloads with broad community support.

- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** — *Alissonerdx* | ❤️ 222 | ⬇️ 0  
  A LoRA for identity-preserving text-to-video (LTX-Video), enabling reference-to-video face generation.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — *nvidia* | ❤️ 903 | ⬇️ 590K  
  A streaming ASR model from Nvidia, efficient for real-time speech recognition.

### 🔧 Specialized Models (embeddings, code, tool-use)

- **[nvidia/Nemotron-3-Embed-1B-BF16](https://huggingface.co/nvidia/Nemotron-3-Embed-1B-BF16)** — *nvidia* | ❤️ 96 | ⬇️ 93K  
  A sentence transformer embedding model (1B parameters) from Nvidia, for semantic similarity and retrieval.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, MLX)

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — *prism-ml* | ❤️ 570 | ⬇️ 1.4M  
  1-bit quantization of a 27B model using llama-cpp – extreme compression for local deployment.

- **[prism-ml/Bonsai-27B-mlx-1bit](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)** — *prism-ml* | ❤️ 161 | ⬇️ 25K  
  MLX-compatible 1-bit version of Bonsai for Apple Silicon devices, expanding cross-platform reach.

- **[prism-ml/Ternary-Bonsai-27B-mlx-2bit](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-mlx-2bit)** — *prism-ml* | ❤️ 135 | ⬇️ 20K  
  Ternary 2-bit MLX variant – balances compression and quality for Mac users.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking)** — *GnLOLot* | ❤️ 166 | ⬇️ 6K  
  Base safetensors version of the 1B thinking model (without GGUF), a lighter alternative for experimentation.

- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** — *conradlocke* | ❤️ 476 | ⬇️ 0  
  A LoRA for

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*