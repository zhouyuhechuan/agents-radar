# Hugging Face Trending Models Digest 2026-07-21

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-21 01:57 UTC

---

# Hugging Face Trending Models Digest — July 21, 2026

## Today's Highlights

This week’s Hugging Face trending board is dominated by **extreme quantization breakthroughs** and **multimodal MoE architectures**. Most notably, `zai-org/GLM-5.2` leads by likes (4,226) as a major dense-sparse MoE release from Zhipu AI, while **prism-ml’s Bonsai family** pushes compression to 1-bit and ternary (2-bit) levels, amassing over 1.6M combined downloads. Google’s `gemma-4-31B-it` quietly dominates raw downloads at nearly 12M, signaling strong enterprise adoption. Meanwhile, **community fine-tuning of Qwen 3.5/3.6** remains the hottest trend—uncensored, finetuned, and GGUF-quantized variants make up over a third of the list. A surprise signal: **robotics models** from OpenMOSS and OpenBMB appear for the first time, suggesting a growing VLA (vision-language-action) pipeline ecosystem.

---

## Trending Models

### 🧠 Language Models (LLMs, Chat Models, Instruction-Tuned)

- **zai-org/GLM-5.2** — *4,226 likes · 531,947 downloads*  
  A large-scale MoE generation model from Zhipu AI featuring dense-sparse attention (DSA), topping the weekly likes chart as the most anticipated open-weight Chinese LLM release.  
  [Link](https://huggingface.co/zai-org/GLM-5.2)

- **google/gemma-4-31B-it** — *3,297 likes · 11,987,240 downloads*  
  Google’s instruction-tuned 31B multimodal model leading total downloads by a wide margin; a key open-weight competitor to GPT-4-class systems.  
  [Link](https://huggingface.co/google/gemma-4-31B-it)

- **tencent/Hy3** — *847 likes · 13,698 downloads*  
  Tencent’s latest Hunyuan v3 text-generation model, gaining steady attention as a strong performer for enterprise Chinese/English chat.  
  [Link](https://huggingface.co/tencent/Hy3)

- **AngelSlim/Hy3-GGUF** — *149 likes · 109,749 downloads*  
  Community GGUF quantization of Tencent’s Hy3 for efficient local inference with llama.cpp.  
  [Link](https://huggingface.co/AngelSlim/Hy3-GGUF)

- **GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking** — *159 likes · 5,494 downloads*  
  A small 1B “thinking” model distilled from Claude Opus + Fable5, gaining traction for its reasoning capability despite tiny size.  
  [Link](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking)

- **GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF** — *134 likes · 28,012 downloads*  
  GGUF variant of the above, optimized for CPU/local deployment.  
  [Link](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF)

- **Cactus-Compute/needle** — *292 likes · 950 downloads*  
  A JAX-native function-calling and tool-use model, attracting early adopters interested in agentic workflows.  
  [Link](https://huggingface.co/Cactus-Compute/needle)

---

### 🎨 Multimodal & Generation (Image, Video, Audio, Text-to-X)

- **moonshotai/Kimi-K2.7-Code** — *1,175 likes · 713,992 downloads*  
  Kimi’s latest multimodal code model with compressed tensors, trending for strong coding performance in a vision-language pipeline.  
  [Link](https://huggingface.co/moonshotai/Kimi-K2.7-Code)

- **baidu/Unlimited-OCR** — *2,441 likes · 2,122,848 downloads*  
  Baidu’s state-of-the-art universal OCR model supporting 100+ languages and document layouts; a top download in the image-to-text category.  
  [Link](https://huggingface.co/baidu/Unlimited-OCR)

- **thinkingmachines/Inkling** — *1,269 likes · 13,462 downloads*  
  A generalist multimodal MoE model from Thinking Machines matching image, text, and audio inputs; strong community buzz as a GPT-4o alternative.  
  [Link](https://huggingface.co/thinkingmachines/Inkling)

- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** — *2,369 likes · 2,117,323 downloads*  
  A Qwen 3.5-based reasoning model distilled with Claude Mythos data, extremely popular for its quantized small-footprint reasoning.  
  [Link](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** — *2,937 likes · 2,007,025 downloads*  
  Qwen 3.6 MoE (35B total, 3B active) aggressively fine-tuned for uncensored generation; one of the fastest-growing community models.  
  [Link](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)

- **bottlecapai/ThinkingCap-Qwen3.6-27B** — *482 likes · 10,647 downloads*  
  A Qwen 3.6-based vision-language model with enhanced reasoning via “thinking cap” fine-tuning.  
  [Link](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)

- **ATH-MaaS/OvisOCR2** — *217 likes · 14,587 downloads*  
  A specialized Qwen 3.5-based OCR model for document and scene text recognition.  
  [Link](https://huggingface.co/ATH-MaaS/OvisOCR2)

- **DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF** — *157 likes · 16,719 downloads*  
  An extensively merged/fused Qwen 3.6 variant with uncensored fine-tuning, illustrating the extreme community customization trend.  
  [Link](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)

- **LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V3-GGUF** — *85 likes · 15,148 downloads*  
  Another Qwen 3.6 MoE GGUF variant, blending Hermes and Genesis datasets for uncensored chat.  
  [Link](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V3-GGUF)

- **empero-ai/Qwythos-9B-v2-GGUF** — *197 likes · 105,749 downloads*  
  Second generation of the Qwythos reasoning model in GGUF format with improved Claude adaptation.  
  [Link](https://huggingface.co/empero-ai/Qwythos-9B-v2-GGUF)

- **Wan-AI/Wan-Dancer-14B** — *145 likes · 2,408 downloads*  
  An image-to-video diffusion model for high-quality motion generation, part of the emerging “video generation” trend.  
  [Link](https://huggingface.co/Wan-AI/Wan-Dancer-14B)

- **Alissonerdx/LTX-Best-Face-ID** — *214 likes · 0 downloads*  
  A LoRA for identity-preserving reference-to-video generation (LTX-Video pipeline), notable for zero download count indicating very recent upload.  
  [Link](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)

- **unsloth/inkling-GGUF** — *111 likes · 6,771 downloads*  
  Unsloth’s optimized GGUF quantization of the Inkling multimodal MoE model, enabling fast local inference.  
  [Link](https://huggingface.co/unsloth/inkling-GGUF)

- **OpenMOSS-Team/MOSS-Transcribe-Diarize** — *291 likes · 87,533 downloads*  
  An audio-text-to-text model for transcription + speaker diarization, leveraging the MOSS architecture for real-time ASR.  
  [Link](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)

- **OpenMOSS-Team/MOSS-VL-Realtime** — *89 likes · 544 downloads*  
  A real-time video-text-to-text model for streaming multimodal inference.  
  [Link](https://huggingface.co/OpenMOSS-Team/MOSS-VL-Realtime)

---

### 🔧 Specialized Models (Code, Math, Medical, Embeddings, Robotics, OCR)

- **nvidia/Nemotron-3-Embed-1B-BF16** — *87 likes · 61,708 downloads*  
  NVIDIA’s next-gen sentence embedding model (1B, Ministral3-based) for retrieval and semantic similarity, gaining adoption in RAG pipelines.  
  [Link](https://huggingface.co/nvidia/Nemotron-3-Embed-1B-BF16)

- **openbmb/MiniCPM-RobotManip** — *135 likes · 0 downloads*  
  A vision-language-action model for robotic manipulation, marking OpenBMB’s entry into embodied AI with MiniCPM VLA.  
  [Link](https://huggingface.co/openbmb/MiniCPM-RobotManip)

- **openbmb/MiniCPM-RobotTrack** — *100 likes · 0 downloads*  
  Companion robot tracking model for VLA pipelines, focusing on object/path tracking.  
  [Link](https://huggingface.co/openbmb/MiniCPM-RobotTrack)

- **moonshotai/Kimi-K2.7-Code** — already listed above, cross-category for code generation.

- **baidu/Unlimited-OCR** — already listed above, cross-category for OCR.

- **Cactus-Compute/needle** — already listed above, cross-category for function-calling.

---

### 📦 Fine-tunes & Quantizations (GGUF, AWQ, LoRA, Community Merge)

- **prism-ml/Ternary-Bonsai-27B-gguf** — *855 likes · 338,945 downloads*  
  A 27B Qwen 3.5 model quantized to 2-bit ternary precision; one of the most efficient LLMs for its size, pivotal for on-device AI.  
  [Link](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)

- **prism-ml/Bonsai-27B-gguf** — *542 likes · 1,262,894 downloads*  
  The original 1-bit Bonsai model, the most downloaded GGUF on the list, showcasing extreme quantization viability for daily use.  
  [Link](https://huggingface.co/prism-ml/Bonsai-27B-gguf)

- **prism-ml/Bonsai-27B-mlx-1bit** — *154 likes · 21,690 downloads*  
  MLX-format 1-bit version of Bonsai for Apple Silicon user adoption.  
  [Link](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)

- **prism-ml/Ternary-Bonsai-27B-mlx-2bit** — *130 likes · 17,869 downloads*  
  MLX-format 2-bit ternary Bonsai for Apple ecosystem.  
  [Link](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-mlx-2bit)

- **conradlocke/krea2-identity-edit** — *458 likes · 0 downloads*  
  A LoRA for Krea-2-Raw enabling identity-preserving image editing, likely a fresh upload with high interest.  
  [Link](https://huggingface.co/conradlocke/krea2-identity-edit)

- **all Qwen 3.5/3.6 GGUF variants** (Qwythos, HauhauCS, DavidAU, LuffyTheFox, empero-ai) — listed above under Multimodal; they are also fine-tunes/quantizations.

- **unsloth/inkling-GGUF** — listed above.

---

## Ecosystem Signal

Several structural trends emerge this week:

**1. Extreme quantization is now mainstream.** The Bonsai family (1-bit and 2-bit ternary) demonstrates that 27B models can run on consumer hardware with acceptable quality. Over 1.6M downloads across four Bonsai repos confirm user appetite for compressed models—not just as experiments but as daily drivers.

**2. Qwen 3.5/3.6 is the foundation of the moment.** More than a third of the trending list is derived from Qwen architectures, with the community layering uncensored fine-tuning, Claude-style reasoning, and aggressive merges (e.g., “Fable Fusion,” “Hermes-Genesis”). This mirrors the earlier Llama 3 ecosystem playbook.

**3. Multimodal MoE is the default architecture.** Five of the top 10 models by likes (GLM-5.2, Inkling, Qwen3.6-35B-A3B, Gemma-4, Kimi-K2.7-Code) are MoE or multimodal. The “image-text-to

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*