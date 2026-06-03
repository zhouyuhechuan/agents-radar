# Hugging Face Trending Models Digest 2026-06-03

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-03 03:26 UTC

---

# Hugging Face Trending Models Digest – June 3, 2026

## Today’s Highlights
The Hugging Face ecosystem this week is dominated by the massive release of **DeepSeek-V4-Pro** (4,577 likes, 5.8M downloads) and its lighter sibling **DeepSeek-V4-Flash** (1,367 likes), setting new standards for open-weight MoE language models. Meanwhile, **Qwen/Qwen3.6-27B** (1,579 likes, 5.2M downloads) cements the Qwen family’s leadership in vision-language tasks, and **bytedance-research/Lance** (1,012 likes) pushes boundaries with an any-to-any multimodal generation model. Surprising entrants include **openai/privacy-filter** (1,595 likes), a token-classification model for identifying sensitive content, and **SulphurAI/Sulphur-2-base** (1,512 likes, 1.6M downloads) signaling strong community interest in open text-to-video generation. The continued wave of GGUF and exotic quantizations (ternary, NVFP4) also reflects a maturing deployment landscape.

---

## Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** – deepseek-ai | Likes: 4,577 | Downloads: 5.8M  
  A flagship dense-MoE hybrid conversational model with industry-leading benchmarks, driving the week’s highest engagement.

- **[DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** – deepseek-ai | Likes: 1,367 | Downloads: 3.5M  
  A faster, MIT-licensed variant of DeepSeek-V4 optimized for latency-critical applications.

- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** – LiquidAI | Likes: 444 | Downloads: 47.7k  
  An 8B-parameter MoE model from Liquid AI, trending for its efficient architecture and strong reasoning capabilities.

- **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)** – openbmb | Likes: 737 | Downloads: 57.7k  
  A tiny 1B-parameter Llama‑style model gaining traction for on-device deployment.

- **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** – JetBrains | Likes: 142 | Downloads: 799  
  A 12B MoE model with a dedicated “thinking” mode, aimed at code and conversation.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** – Qwen | Likes: 1,579 | Downloads: 5.2M  
  The official Qwen 3.6 vision-language model, combining strong image understanding with text generation.

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** – SulphurAI | Likes: 1,512 | Downloads: 1.6M  
  A high-quality text-to-video model built on LTX‑2.3, trending due to its impressive output quality.

- **[bytedance-research/Lance](https://huggingface.co/bytedance-research/Lance)** – bytedance-research | Likes: 1,012 | Downloads: 3.2k  
  A pioneering any-to-any model handling text, image, video, and audio generation from any input modality.

- **[NemoStation/Marlin-2B](https://huggingface.co/NemoStation/Marlin-2B)** – NemoStation | Likes: 498 | Downloads: 17.6k  
  A compact video-text-to-text model for video understanding, based on Qwen3.5 architecture.

- **[meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)** – meituan-longcat | Likes: 492 | Downloads: 174  
  A novel audio-image-text-to-video avatar generation model from Meituan.

- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** – stepfun-ai | Likes: 217 | Downloads: 12.9k  
  A vision-language MoE model optimized for fast inference, part of the Step‑series.

- **[nvidia/Cosmos3-Super](https://huggingface.co/nvidia/Cosmos3-Super)** – nvidia | Likes: 100 | Downloads: 2.8k  
  Part of NVIDIA’s Cosmos3 omni-family, supporting text-to-image, image-to-video, and more (listed components: Super-Text2Image, Super-Image2Video).

- **[Supertone/supertonic-3](https://huggingface.co/Supertone/supertonic-3)** – Supertone | Likes: 782 | Downloads: 59k  
  A leading Korean English TTS model with expressive speech synthesis.

- **[OpenMOSS-Team/MOSS-TTS-v1.5](https://huggingface.co/OpenMOSS-Team/MOSS-TTS-v1.5)** – OpenMOSS-Team | Likes: 123 | Downloads: 20.6k  
  A Chinese-focused text-to-speech model with custom code for delay‑based prosody.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** – nvidia | Likes: 999 | Downloads: 61.6k  
  A 3B vision-language model specialized in object localization and feature extraction.

### 🔧 Specialized Models (code, math, medical, embeddings, safety)

- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)** – openai | Likes: 1,595 | Downloads: 300k  
  A token-classification model trained to detect personally identifiable information (PII), trending due to OpenAI’s direct release.

- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)** – PaddlePaddle | Likes: 190 | Downloads: 4k  
  An OCR vision-language model built on ERNIE 4.5, enabling end-to-end text detection and recognition.

- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** – sapientinc | Likes: 476 | Downloads: 153k  
  A 1B-parameter language model fine-tuned for human resources management tasks (resume analysis, screening).

- **[nvidia/PiD](https://huggingface.co/nvidia/PiD)** – nvidia | Likes: 268 | Downloads: 646  
  A diffusion-based super-resolution model (image-to-image) featuring NVIDIA’s PiD architecture.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** – HauhauCS | Likes: 1,284 | Downloads: 2.5M  
  An uncensored, aggressively fine-tuned Qwen3.6 MoE variant, highly popular despite controversial filtering.

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** – unsloth | Likes: 610 | Downloads: 982k  
  GGUF quantization of Qwen3.6-27B with multi‑token prediction, enabling efficient local deployment.

- **[LiquidAI/LFM2.5-8B-A1B-GGUF](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B-GGUF)** – LiquidAI | Likes: 162 | Downloads: 70.9k  
  Official GGUF version of the LFM2.5 MoE, optimized for edge hardware via llama.cpp.

- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** – nvidia | Likes: 139 | Downloads: 313k  
  NVIDIA’s 4‑bit floating point quantization of Qwen3.6 MoE, using Model Optimizer for high throughput.

- **[stepfun-ai/Step-3.7-Flash-GGUF](https://huggingface.co/stepfun-ai/Step-3.7-Flash-GGUF)** – stepfun-ai | Likes: 95 | Downloads: 39.3k  
  GGUF quantized version of Step‑3.7‑Flash, enabling vision-language MoE on consumer GPUs.

- **[Jackrong/Qwopus3.6-27B-v2-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-MTP-GGUF)** – Jackrong | Likes: 197 | Downloads: 156k  
  Another community GGUF of Qwen3.6 (variant named Qwopus) with multi‑token prediction.

- **[prism-ml/bonsai-image-ternary-4B-gemlite-2bit](https://huggingface.co/prism-ml/bonsai-image-ternary-4B-gemlite-2bit)** – prism-ml | Likes: 101 | Downloads: 41  
  A 1.58‑bit ternary quantized text-to-image

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*