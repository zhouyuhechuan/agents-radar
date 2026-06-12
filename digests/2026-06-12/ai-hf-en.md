# Hugging Face Trending Models Digest 2026-06-12

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-12 02:50 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-06-12

## 1. Today's Highlights

DeepSeek-V4-Pro dominates the charts this week with 4,783 likes and over 4 million downloads, cementing its position as the most-watched open-weight language model release of the quarter. Nvidia is making a strong multimodal push with **LocateAnything-3B** (1,876 likes) — a powerful grounding/detection model that bridges vision and language — and the massive **Nemotron-3 Ultra 550B** MoE flagship. Google's Gemma-4 family continues to generate massive ecosystem activity, with the instruction-tuned 12B variant racking up 675K+ downloads and spawning a wave of community quantizations, abliterations, and GGUF conversions from Unsloth and others. Notably, the uncensored **Qwen3.6-35B-A3B** from HauhauCS has seen explosive downloads (3M+) despite modest likes, suggesting heavy automated or API-driven consumption.

---

## 2. Trending Models by Category

### 🧠 Language Models

- **DeepSeek-V4-Pro** by deepseek-ai — **4,783 likes**, 4,061,006 downloads  
  [→ HF Link](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)  
  The flagship 4th-gen MoE conversational model from DeepSeek, trending due to exceptional benchmark performance and aggressive open-weight licensing.

- **CohereLabs/North-Mini-Code-1.0** by CohereLabs — **309 likes**, 1,859 downloads  
  [→ HF Link](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)  
  A compact Cohere 2 MoE model specialized for code generation, gaining traction among developers for its efficiency.

- **sapientinc/HRM-Text-1B** by sapientinc — **750 likes**, 134,752 downloads  
  [→ HF Link](https://huggingface.co/sapientinc/HRM-Text-1B)  
  A 1B-parameter HR management domain model, notable for demonstrating that enterprise vertical models can achieve strong pull outside general-purpose releases.

- **OBLITERATUS/Gemma-4-12B-OBLITERATED** by OBLITERATUS — **234 likes**, 14,838 downloads  
  [→ HF Link](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)  
  An "abliterated"/uncensored variant of Gemma-4-12B, reflecting sustained community demand for less-restrictive fine-tunes.

- **nex-agi/Nex-N2-Pro** by nex-agi — **206 likes**, 1,185 downloads  
  [→ HF Link](https://huggingface.co/nex-agi/Nex-N2-Pro)  
  A Qwen3.5-based MoE model optimized for agentic workflows, attracting interest from the growing agent-systems community.

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** by HauhauCS — **1,681 likes**, 3,057,541 downloads  
  [→ HF Link](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)  
  A massively downloaded uncensored MoE vision-language model, popular for its aggressive creative generation capabilities despite content policy concerns.

- **XiaomiMiMo/MiMo-V2.5-Pro-FP4-DFlash** by XiaomiMiMo — **87 likes**, 660 downloads  
  [→ HF Link](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro-FP4-DFlash)  
  Xiaomi's latest MiMo model in FP4 quantization, targeting on-device agent deployment with a focus on flash decoding.

- **nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16** by nvidia — **198 likes**, 59,066 downloads  
  [→ HF Link](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)  
  Nvidia's largest Nemotron-3 offering — a 550B-parameter MoE (55B active) — released in BF16, underscoring the enterprise push toward massive open-weight models.

- **nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4** by nvidia — **168 likes**, 91,117 downloads  
  [→ HF Link](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)  
  NVFP4-quantized version of the Nemotron-3 Ultra, enabling the 550B model to run on fewer GPUs — explanation for higher downloads than the BF16 version.

- **stepfun-ai/Step-3.7-Flash** by stepfun-ai — **368 likes**, 50,187 downloads  
  [→ HF Link](https://huggingface.co/stepfun-ai/Step-3.7-Flash)  
  A fast vision-language model from StepFun, gaining likes for its competitive speed-to-quality ratio.

---

### 🎨 Multimodal & Generation

- **nvidia/LocateAnything-3B** by nvidia — **1,876 likes**, 131,794 downloads  
  [→ HF Link](https://huggingface.co/nvidia/LocateAnything-3B)  
  An image-text-to-text model for visual grounding and object localization, trending as the top multimodal release this week.

- **google/diffusiongemma-26B-A4B-it** by google — **505 likes**, 0 downloads  
  [→ HF Link](https://huggingface.co/google/diffusiongemma-26B-A4B-it)  
  Google's diffusion-based language model (26B MoE, 4B active), representing a novel architecture that blends autoregressive text generation with diffusion — high interest despite no downloads yet.

- **google/gemma-4-12B-it** by google — **942 likes**, 675,936 downloads  
  [→ HF Link](https://huggingface.co/google/gemma-4-12B-it)  
  The flagship Gemma-4 instruction-tuned model with any-to-any capabilities, the most downloaded model in its weight class this week.

- **google/gemma-4-12B** by google — **518 likes**, 140,221 downloads  
  [→ HF Link](https://huggingface.co/google/gemma-4-12B)  
  Base (non-instruction) Gemma-4-12B, still drawing significant attention as the foundation for fine-tuning.

- **huihui-ai/Huihui-gemma-4-12B-it-abliterated** by huihui-ai — **144 likes**, 6,400 downloads  
  [→ HF Link](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-it-abliterated)  
  An abliterated version of Gemma-4-12B-it, representing the community's push to remove alignment constraints for creative and uncensored use cases.

- **ideogram-ai/ideogram-4-fp8** by ideogram-ai — **487 likes**, 7,170 downloads  
  [→ HF Link](https://huggingface.co/ideogram-ai/ideogram-4-fp8)  
  FP8-quantized version of Ideogram-4, a leading text-to-image diffusion model, popular for its quality and reduced memory footprint.

- **ideogram-ai/ideogram-4-nf4** by ideogram-ai — **317 likes**, 6,124 downloads  
  [→ HF Link](https://huggingface.co/ideogram-ai/ideogram-4-nf4)  
  NF4-quantized variant of Ideogram-4, further pushing accessibility of high-quality image generation on consumer hardware.

- **ByteDance/Bernini-R** by ByteDance — **222 likes**, 305 downloads  
  [→ HF Link](https://huggingface.co/ByteDance/Bernini-R)  
  An image-text-to-video model with a novel "renderer" approach, attracting attention for its potential in video generation from static images and prompts.

- **google/magenta-realtime-2** by google — **178 likes**, 19,806 downloads  
  [→ HF Link](https://huggingface.co/google/magenta-realtime-2)  
  Google's real-time text-to-audio music generation model (TFLite), gaining traction among music producers and creative tool builders.

- **zai-org/SCAIL-2** by zai-org — **118 likes**, 0 downloads  
  [→ HF Link](https://huggingface.co/zai-org/SCAIL-2)  
  A pose-driven character animation diffusion model for image-to-video, novel in its focus on controllable skeletal animation.

---

### 🔧 Specialized Models

- **bosonai/higgs-audio-v3-tts-4b** by bosonai — **360 likes**, 19,948 downloads  
  [→ HF Link](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)  
  A 4B-parameter multimodal TTS model built on Qwen3, trending for its natural prosody and low latency.

- **nvidia/nemotron-3.5-asr-streaming-0.6b** by nvidia — **372 likes**, 4,965 downloads  
  [→ HF Link](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)  
  A compact 0.6B streaming ASR model with cache-aware architecture, important for real-time speech recognition deployments.

- **MisoLabs/MisoTTS** by MisoLabs — **194 likes**, 0 downloads  
  [→ HF Link](https://huggingface.co/MisoLabs/MisoTTS)  
  A new text-to-speech model with high-fidelity voice synthesis, generating buzz for its sample quality despite zero downloads so far.

- **Comfy-Org/Ideogram-4** by Comfy-Org — **135 likes**, 0 downloads  
  [→ HF Link](https://huggingface.co/Comfy-Org/Ideogram-4)  
  ComfyUI integration wrapper for Ideogram-4, trending among the ComfyUI ecosystem for streamlined image generation pipelines.

---

### 📦 Fine-tunes & Quantizations

- **unsloth/gemma-4-12b-it-GGUF** by unsloth — **562 likes**, 711,706 downloads  
  [→ HF Link](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)  
  GGUF-quantized Gemma-4-12B-it from Unsloth, the most downloaded GGUF model this week — enabling CPU-friendly inference.

- **unsloth/gemma-4-12B-it-qat-GGUF** by unsloth — **200 likes**, 148,252 downloads  
  [→ HF Link](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF)  
  QAT (quantization-aware training) version of the Gemma-4 GGUF, offering improved accuracy over post-training quantization.

- **unsloth/diffusiongemma-26B-A4B-it-GGUF** by unsloth — **184 likes**, 0 downloads  
  [→ HF Link](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)  
  The first GGUF quantization of the new diffusion-based Gemma architecture, early-stage but notable for opening novel architecture to local inference.

- **unsloth/gemma-4-26B-A4B-it-qat-GGUF** by unsloth — **143 likes**, 129,110 downloads  
  [→ HF Link](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)  
  The larger 26B variant of Gemma-4 in QAT GGUF format, providing a strong compute-to-quality trade-off for advanced users.

- **google/gemma-4-12B-it-qat-q4_0-gguf** by google — **130 likes**, 96,749 downloads  
  [→ HF Link](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf)  
  Official Google GGUF release with QAT and q4_0 quantization, marking Google's growing support for compressed model distribution.

---

## 3. Ecosystem Signal

**Gemma-4 ecosystem dominates.** Google's Gemma-4 family — 12B and 26B variants — appears in 10 of the 30 models on this list across base, instruction-tuned, quantized, abliterated, and GGUF formats. This signals that the community has placed a massive bet on Gemma-4 as the open-weight model of the season, comparable to the Llama-3 frenzy in 2024.

**MoE is the new norm.** DeepSeek-V4-Pro, Nemotron-3 Ultra (550B MoE), Qwen3.6-35B-A3B, Nex-N2-Pro, diffusiongemma-26B — almost every major release this week uses a Mixture-of-Experts architecture. The trend is clear: the community has accepted MoE trade-offs (larger total params, smaller active params) as the path to frontier performance.

**Diffusion meets language.** Google's diffusiongemma is the most architecturally novel model this week, merging diffusion with autoregressive text generation. Even with zero downloads (likely due to licensing or documentation gaps), its 505 likes indicate intense curiosity about non-autoregressive LLM architectures.

**Quantization ecosystem deepens.** Unsloth continues to dominate GGUF conversion with 5 entries, while Nvidia pushes NVFP4 for enterprise-scale models. The emergence of QAT (quantization-aware training) variants from both Unsloth and Google suggests that post-training quantization is being supplemented by pre-trained quantized checkpoints.

**Enterprise and vertical models are gaining ground.** sapientinc/HRM-Text-1B (HR domain), Cohere's code model, and Nvidia's streaming ASR model show that specialized, smaller models can compete for attention when they solve concrete enterprise needs.

**Uncensored / abliterated models remain a strong niche.** HauhauCS's Qwen3.6 uncensored variant has 3M+ downloads, and OBLITERATUS and huihui-ai both release abliterated Gemma-4 variants, indicating sustained appetite for unrestricted generation capabilities.

---

## 4. Worth Exploring

1. **nvidia/LocateAnything-3B** — The standout multimodal model this week. Its grounding/detection capabilities combined with a 3B parameter size make it immediately useful for vision-language applications like object counting, referring expression comprehension, and robotics. A strong candidate for fine-tuning on custom detection tasks.

2. **google/diffusiongemma-26B-A4B-it** — Despite zero downloads, this is the most architecturally interesting model on the list. It represents a potential paradigm shift — using diffusion for text generation. Worth studying the paper and trying once access is available. If diffusion-based LLMs work at scale, they could change inference economics.

3. **unsloth/gemma-4-12b-it-GGUF** — The practical winner. With 711K downloads, this is clearly the community's go-to Gemma-4 variant. If you want to run Gemma-4 locally on a CPU or with limited VRAM, this is the first download to try. Its popularity also makes it a good base for community-supported fine-tunes.

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*