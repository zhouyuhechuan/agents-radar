# Hugging Face Trending Models Digest 2026-07-27

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-27 02:11 UTC

---

# Hugging Face Trending Models Digest — July 27, 2026

## Today's Highlights

This week’s Hugging Face landscape is dominated by **extreme quantization breakthroughs** and **vision-language fusion**. zai-org’s GLM-5.2 leads in likes (4,477), while massive GPU-efficient models like the 1-bit Bonsai-27B-gguf (2.1M downloads) and Ternary-Bonsai-27B show the community’s hunger for deployable, ultra-low-precision LLMs. Qualcomm-friendly NVFP4 quantizations of Laguna-S-2.1 and GLM-5.2-Vision signal a push toward edge and mobile inference. On the multimodal side, Qwen3.6-based uncensored fine-tunes (e.g., from HauhauCS and DavidAU) and the new Inkling conversational model are generating strong traction, alongside Microsoft’s Mage-Flow for text-to-image and computer-use models like Fara1.5-27B. OpenBMB’s robotics MiniCPM models also hint at growing VLA (vision-language-action) interest.

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[poolside/Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1)** — poolside, 701 likes, 56k downloads. A new flagship LLM for enterprise-grade text generation, gaining traction alongside its many quantization variants.
- **[upstage/Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** — upstage, 596 likes, 3.3k downloads. A massive 250B-parameter open-weight model vying for leadership in the high-end open LLM space.
- **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** — Nanbeige, 449 likes, 14k downloads. A compact 3B model demonstrating strong performance for its size, ideal for resource-constrained deployments.
- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org, 4,477 likes, 827k downloads. The week’s most-liked model overall; a large MoE conversational LLM with strong reasoning and multilingual capabilities.
- **[Motif-Technologies/Motif-3-Beta](https://huggingface.co/Motif-Technologies/Motif-3-Beta)** — Motif-Technologies, 193 likes, 2.4k downloads. A feature-extraction focused model, possibly for retrieval-augmented generation pipelines.
- **[fdtn-ai/antares-1b](https://huggingface.co/fdtn-ai/antares-1b)** — fdtn-ai, 187 likes, 6k downloads. A 1B security-tuned LLM, indicating a niche for domain-specific safety models.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu, 3,207 likes, 2.6M downloads. A state-of-the-art OCR model handling image-text-to-text tasks, trending for high-volume document processing.
- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** — thinkingmachines, 1,579 likes, 34.5k downloads. A conversational multimodal model integrating vision and language, gaining buzz as a general-purpose assistant.
- **[microsoft/Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)** — microsoft, 335 likes, 1.4k downloads. A text-to-image diffusion model focused on high-quality generation and editing, part of a growing family.
- **[owensong/Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2)** — owensong, 180 likes, 298 downloads. A tiny text-to-speech model optimized for CPU and edge AI, ideal for on-device voice synthesis.
- **[nvidia/Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge)** — nvidia, 125 likes, 32.7k downloads. Nvidia’s latest world-model diffusion model for video simulation and autonomous driving research.
- **[microsoft/Mage-Flow-Edit-Turbo](https://huggingface.co/microsoft/Mage-Flow-Edit-Turbo)** — microsoft, 89 likes, 946 downloads. An instruction-based image-to-image editing turbo variant of Mage-Flow.
- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — bottlecapai, 554 likes, 27.8k downloads. A Qwen3.6-based vision-language model emphasizing reasoning, competitive with OpenAI’s GPT-4o.

### 🔧 Specialized Models (code, math, medical, embeddings, OCR, robotics)

- **[Kwaipilot/KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev)** — Kwaipilot, 198 likes, 3.8k downloads. A MoE code-focused model built on Qwen3.5, trending for developer tooling.
- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — moonshotai, 1,298 likes, 730k downloads. A top code-generation model with vision support, using compressed-tensors for efficiency.
- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** — ATH-MaaS, 309 likes, 35.6k downloads. An OCR-specific vision-language model optimized for document understanding.
- **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** — openbmb, 177 likes, 643 downloads. A vision-language-action model for robotic manipulation, part of MiniCPM’s robotics push.
- **[openbmb/MiniCPM-RobotTrack](https://huggingface.co/openbmb/MiniCPM-RobotTrack)** — openbmb, 130 likes, 398 downloads. A companion model for robot tracking, extending the VLA family for embodied AI.
- **[microsoft/Fara1.5-27B](https://huggingface.co/microsoft/Fara1.5-27B)** — microsoft, 110 likes, 1.2k downloads. A computer-use model (agentic UI navigation) based on Qwen3.5, signaling a trend toward GUI agents.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ, LoRA)

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** — DavidAU, 638 likes, 552k downloads. An extensively fine-tuned, uncensored Qwen3.6 vision variant in GGUF, popular for

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*