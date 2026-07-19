# Hugging Face Trending Models Digest 2026-07-19

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-19 01:58 UTC

---

# Hugging Face Trending Models Digest — 2026-07-19

## Today's Highlights

Google's **Gemma-4-31B-it** leads downloads by a wide margin (12.6M+), signaling strong enterprise interest in open-weight multimodal models. The **Qwen 3.6** ecosystem continues its explosive growth, with multiple fine-tunes and GGUF variants appearing across the top 30, including the aggressively tuned **HauhauCS/Qwen3.6-35B-A3B-Uncensored** (2.2M downloads). **Prism-ML** pushes quantization frontiers with their sub-2-bit **Bonsai** series, while **Zhipu AI's GLM-5.2** demonstrates that new MoE architecture can still capture community attention (4.1K likes). Audio and video models are gaining traction, with **MOSS-Transcribe-Diarize** and **Wan-Dancer-14B** representing a multimodal diversification beyond text.

---

## Trending Models

### 🧠 Language Models

- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 4,126 likes | 541,662 downloads  
  A new MoE-DSA architecture from Zhipu AI that achieves strong reasoning capabilities with efficient expert routing, trending as a major open-weight competitor.

- **[ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — prism-ml | 737 likes | 301,893 downloads  
  An extreme quantization (2-bit ternary) of a 27B model, demonstrating that sub-2-bit compression can preserve useful conversational quality.

- **[Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — prism-ml | 444 likes | 1,218,815 downloads  
  A 1-bit quantized 27B model in GGUF format, enabling near-universal deployment; the 1.2M downloads reflect massive community interest in ultra-low-bit LLMs.

- **[MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)** — GnLOLot | 277 likes | 172,409 downloads  
  A 1B parameter thinking-style model distilled from larger systems, proving that small models with reasoning fine-tuning can achieve high adoption.

- **[Hy3](https://huggingface.co/tencent/Hy3)** — tencent | 829 likes | 13,571 downloads  
  Tencent's latest Hunyuan-generation text model, gaining attention as a powerful open-weight alternative from a major Chinese lab.

- **[Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — InternScience | 579 likes | 35,575 downloads  
  A Qwen3.5-MoE fine-tune optimized for agent and tool-use scenarios, trending as the community shifts toward deployable agentic models.

- **[MiniCPM5-1B-Claude-Opus-Fable5-Thinking](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking)** — GnLOLot | 143 likes | 5,271 downloads  
  The full-precision sibling of the GGUF version above, representing a trend toward compact, reasoning-capable language models.

- **[Bonsai-27B-mlx-1bit](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)** — prism-ml | 127 likes | 20,639 downloads  
  Apple MLX-format 1-bit variant of Bonsai, targeting Apple Silicon users who want extreme model compression without sacrifice.

- **[ternary-Bonsai-27B-mlx-2bit](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-mlx-2bit)** — prism-ml | 111 likes | 17,063 downloads  
  MLX-format 2-bit ternary Bonsai, offering a middle ground between compression and quality for the Apple ecosystem.

---

### 🎨 Multimodal & Generation

- **[Gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — google | 3,263 likes | 12,608,008 downloads  
  Google's first multimodal Gemma release with vision-language capabilities, dominating downloads as the community embraces open Google models.

- **[Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | 2,315 likes | 2,112,869 downloads  
  A reasoning-enhanced, quantized Qwen3.5 vision-language model; its massive download count indicates surging demand for multimodal GGUF models.

- **[Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 2,865 likes | 2,190,398 downloads  
  An uncensored, aggressive-tuned Qwen3.6 MoE vision model, signaling strong community appetite for less-restricted multimodal systems.

- **[Baitu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | 2,025 likes | 2,088,470 downloads  
  A specialized OCR model from Baidu achieving near-universal text recognition, trending for its practical utility and high accuracy.

- **[Inkling](https://huggingface.co/thinkingmachines/Inkling)** — thinkingmachines | 1,063 likes | 12,456 downloads  
  A new image-text-to-text MoE model that combines vision and text understanding in a conversational interface, gaining rapid traction.

- **[ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — bottlecapai | 437 likes | 10,445 downloads  
  A reasoning-focused fine-tune of Qwen3.6 with vision capabilities, representing the convergence of multimodal and chain-of-thought.

- **[OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** — ATH-MaaS | 170 likes | 13,750 downloads  
  A Qwen3.5-based OCR model optimized for document understanding, filling a niche for high-quality text extraction.

- **[Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)** — Wan-AI | 114 likes | 2,328 downloads  
  A diffusion-based image-to-video model, trending as the community explores video generation beyond text prompts.

- **[MOSS-VL-Realtime](https://huggingface.co/OpenMOSS-Team/MOSS-VL-Realtime)** — OpenMOSS-Team | 77 likes | 529 downloads  
  A real-time video-text-to-text model, pushing boundaries on low-latency multimodal understanding.

---

### 🔧 Specialized Models

- **[needle](https://huggingface.co/Cactus-Compute/needle)** — Cactus-Compute | 268 likes | 935 downloads  
  A Jax-based model optimized for function-calling and tool-use, reflecting growing interest in non-chat LLM applications.

- **[MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — OpenMOSS-Team | 259 likes | 86,385 downloads  
  An audio-text-to-text model combining transcription with speaker diarization, filling a gap in end-to-end audio processing.

- **[krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** — conradlocke | 395 likes | 0 downloads  
  A LoRA for identity-preserving image editing on Krea-2, trending for enabling consistent character editing in workflows.

- **[Cseti/LTX2.3-22B_IC-LoRA-CrossView-Prompt](https://huggingface.co/Cseti/LTX2.3-22B_IC-LoRA-CrossView-Prompt)** — Cseti | 91 likes | 0 downloads  
  A LoRA for novel-view synthesis in video generation, representing research-oriented interest in spatial reasoning.

- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** — Alissonerdx | 187 likes | 0 downloads  
  An identity-preservation LoRA for text-to-video, showing demand for controllable character consistency in generated videos.

- **[Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — froggeric | 941 likes | 0 downloads  
  A utility model providing corrected Jinja chat templates for Qwen models, highlighting community attention to inference infrastructure.

- **[GLM-5.2-colibri-int4](https://huggingface.co/jlnsrk/GLM-5.2-colibri-int4)** — jlnsrk | 132 likes | 3,869 downloads  
  An INT4 CPU-optimized variant of GLM-5.2 using expert streaming, enabling large MoE models to run on consumer hardware.

---

### 📦 Fine-tunes & Quantizations

- **[Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — prism-ml | 444 likes | 1,218,815 downloads  
  The flagship 1-bit quantization of Bonsai; its massive downloads define the extreme quantization trend.

- **[Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — prism-ml | 737 likes | 301,893 downloads  
  Ternary 2-bit variant offering a step up in quality while remaining highly compressed.

- **[Qwythos-9B-v2](https://huggingface.co/empero-ai/Qwythos-9B-v2)** — empero-ai | 140 likes | 9,060 downloads  
  The full-precision base model behind the Qwythos GGUF variants, representing the foundation fine-tune.

- **[Qwythos-9B-v2-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-v2-GGUF)** — empero-ai | 169 likes | 103,504 downloads  
  GGUF quantized version of the Qwythos v2 vision-language model, enabling local deployment.

- **[Hy3-GGUF](https://huggingface.co/AngelSlim/Hy3-GGUF)** — AngelSlim | 127 likes | 100,768 downloads  
  Community quantization of Tencent's Hy3, making the model accessible via llama.cpp infrastructure.

- **[Unsloth/inkling-GGUF](https://huggingface.co/unsloth/inkling-GGUF)** — unsloth | 96 likes | 6,461 downloads  
  Unsloth's official GGUF of the Inkling multimodal MoE, ensuring optimized local inference.

- **[MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)** — GnLOLot | 277 likes | 172,409 downloads  
  GGUF quantization of the 1B thinking model, proving small models benefit from quantization too.

- **[MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF)** — GnLOLot | 114 likes | 19,279 downloads  
  A refined version of the V2 thinking model in GGUF format, part of an iterative release pattern.



---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*