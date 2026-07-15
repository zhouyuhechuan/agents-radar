# Hugging Face Trending Models Digest 2026-07-15

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-15 01:45 UTC

---

# Hugging Face Trending Models Digest — 2026-07-15

## Today's Highlights

This week's trending models are overwhelmingly dominated by **quantized variants of the Qwen 3.5/3.6 family**, with multiple GGUF entries (Qwythos-9B, Qwen3.6-27B, Qwen3.6-35B-MoE) racking up millions of downloads each. The most liked model overall is **zai-org/GLM-5.2** (3,948 likes), Zhipu AI's new Mixture-of-Experts architecture, signaling strong interest in MoE language models optimized for conversational use. Meanwhile, **baidu/Unlimited-OCR** (1,983 likes, 1.7M downloads) is a standout specialized model, reflecting sustained demand for high-quality OCR pipelines. Notably, the "GGUF revolution" continues: nearly half the trending list consists of quantized models designed for local inference via llama.cpp, with community fine-tunes like **Ornith-1.0-35B-GGUF** and **gemma-4-12B-agentic** also seeing strong uptake. NVIDIA is making a push with its Nemotron-Labs family, and several video-generation fine-tunes (LTX, LingBot) point to growing interest in controllable video from images or text.

---

## Trending Models

### 🧠 Language Models

- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — *zai-org* • 3,948 likes • 489,611 downloads  
  Zhipu AI's latest MoE architecture for conversational AI, currently the most-liked model on the hub this week.

- **[Hy3](https://huggingface.co/tencent/Hy3)** — *tencent* • 781 likes • 10,406 downloads  
  Tencent's Hunyuan-v3-based text-generation model, representing one of the few major proprietary-to-open-weight transitions.

- **[NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4)** — *nvidia* • 117 likes • 41,755 downloads  
  NVIDIA's massive 75B MoE model with only 9B active parameters, using NVFP4 quantization for efficient deployment.

- **[Nemotron-Labs-Audex-30B-A3B](https://huggingface.co/nvidia/NVIDIA-Nemotron-Labs-Audex-30B-A3B)** — *nvidia* • 149 likes • 1,332 downloads  
  A smaller Nemotron variant (30B total, 3B active) optimized for audio-augmented reasoning.

- **[Qwythos-9B-v2](https://huggingface.co/empero-ai/Qwythos-9B-v2)** — *empero-ai* • 115 likes • 3,959 downloads  
  The base full-precision version of the popular Qwythos fine-tune, blending Qwen3.5 with Claude-Mythos-style training data.

- **[Tess-4-27B](https://huggingface.co/migtissera/Tess-4-27B)** — *migtissera* • 112 likes • 1,262 downloads  
  A Qwen3.5-based vision-language model fine-tuned for improved instruction following and creative reasoning.

### 🎨 Multimodal & Generation

- **[Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — *empero-ai* • 2,156 likes • 2,006,265 downloads  
  A highly popular GGUF-quantized vision-language model combining Qwen3.5 with Claude Mythos-style reasoning, driving massive download counts.

- **[Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — *baidu* • 1,983 likes • 1,715,301 downloads  
  Baidu's state-of-the-art OCR model processing unlimited-length documents, a rare specialized model achieving mainstream traction.

- **[MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — *OpenMOSS-Team* • 189 likes • 65,109 downloads  
  An audio-to-text pipeline that transcribes and diarizes multi-speaker conversations, built on the MOSS architecture.

- **[lingbot-video-moe-30b-a3b](https://huggingface.co/robbyant/lingbot-video-moe-30b-a3b)** — *robbyant* • 104 likes • 700 downloads  
  A video-generation MoE diffusion model with 30B parameters (3B active), representing the trend toward efficient video generation.

- **[lingbot-world-v2-14b-causal-fast](https://huggingface.co/robbyant/lingbot-world-v2-14b-causal-fast)** — *robbyant* • 96 likes • 0 downloads  
  A world-model video generator built on a 14B causal diffusion architecture, optimized for fast image-to-video inference.

- **[LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** — *Alissonerdx* • 141 likes • 0 downloads  
  A LoRA fine-tune for LTX-Video enabling identity-preserving text-to-video with subject consistency.

- **[M87](https://huggingface.co/mgwr/M87)** — *mgwr* • 107 likes • 2,408 downloads  
  A diffusion LoRA for Krea-2-Turbo focused on custom text-to-image generation.

- **[OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** — *ATH-MaaS* • 85 likes • 745 downloads  
  A Qwen3.5-based OCR model optimized for document understanding and extraction.

### 🔧 Specialized Models

- **[Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — *InternScience* • 538 likes • 30,539 downloads  
  A Qwen3.5-MoE model fine-tuned for agentic workflows, combining vision-language capabilities with tool-use reasoning.

- **[gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — *yuxinlu1* • 1,189 likes • 468,629 downloads  
  A GGUF-quantized Gemma-4 fine-tune optimized for coding and terminal-based agentic tasks, extremely popular among developers.

- **[ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — *bottlecapai* • 341 likes • 6,208 downloads  
  A vision-language model fine-tuned for explicit chain-of-thought reasoning, extending Qwen3.6 with structured thinking tokens.

- **[Giga-World-1](https://huggingface.co/open-gigaai/Giga-World-1)** — *open-gigaai* • 132 likes • 0 downloads  
  An open-weight world model from open-gigaai, built with diffusers for simulation and planning tasks.

- **[Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — *froggeric* • 903 likes • 0 downloads  
  A non-model resource providing corrected Jinja chat templates for Qwen models, addressing a common pain point for developers.

### 📦 Fine-tunes & Quantizations

- **[Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — *HauhauCS* • 2,731 likes • 2,443,871 downloads  
  A very high-download MoE vision-language model (35B total, 3B active) fine-tuned for uncensored output and aggressive reasoning.

- **[Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — *unsloth* • 1,091 likes • 2,904,515 downloads  
  Unsloth's GGUF-quantized Qwen3.6-27B with Multi-Token Prediction, the most downloaded model this week.

- **[Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — *deepreinforce-ai* • 880 likes • 1,533,354 downloads  
  A 35B open-weight model quantized to GGUF, designed for general-purpose text generation and instruction following.

- **[Qwen3.6-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.6-27B-NVFP4)** — *unsloth* • 204 likes • 1,599,150 downloads  
  Unsloth's NVFP4-quantized Qwen3.6-27B, leveraging NVIDIA's new floating-point 4-bit format for efficient inference.

- **[DeepSeek-V4-Flash-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-GGUF)** — *unsloth* • 172 likes • 55,222 downloads  
  A GGUF quant of DeepSeek-V4-Flash, the latest in the DeepSeek line, optimized for fast reasoning.

- **[Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — *prism-ml* • 159 likes • 23 downloads  
  A 2-bit ternary quantization of a 27B model, pushing the boundaries of extreme quantization for local deployment.

- **[Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — *prism-ml* • 96 likes • 513 downloads  
  A 1-bit quantized 27B model, demonstrating remarkable compression ratios (theoretically ~3x reduction vs 2-bit).

- **[MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)** — *GnLOLot* • 233 likes • 89,892 downloads  
  A creatively-named 1B parameter GGUF model, showing that even tiny quantized models can attract significant attention.

- **[Qwythos-9B-v2-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-v2-GGUF)** — *empero-ai* • 129 likes • 70,260 downloads  
  The GGUF variant of Qwythos-9B-v2, rounding out the empero-ai family's dominance in quantization.

- **[GLM-5.2-colibri-int4](https://hug

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*