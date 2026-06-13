# Hugging Face Trending Models Digest 2026-06-13

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-13 02:42 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-06-13

## Today's Highlights

The week is dominated by **DeepSeek-V4-Pro** (#25), which leads all models with 4,796 weekly likes and 3.38M downloads — a landmark open-weight release that is clearly the most impactful launch of the week. Google continues its Gemma-4 family rollout with **gemma-4-12B-it** (#4, 970 likes, 911k downloads) and its base variant, while the community has responded with an enormous wave of quantized and fine-tuned derivatives. **NVIDIA's LocateAnything-3B** (#2) stands out as a high-engagement specialist model with 1,927 likes and 149k downloads, signaling strong demand for grounded vision-language capabilities. The **Ideogram-4** family (#10, #19, #27, #28) shows sustained momentum in text-to-image, while **ByteDance's Bernini-R** (#30) introduces a novel image-text-to-video pipeline. Multimodal and "any-to-any" architectures continue to reshape the landscape, with image-text-to-text now a dominant pipeline type across the top 30.

---

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — *deepseek-ai* | 4,796 likes | 3,384,418 downloads  
  A massive conversational MoE model that is the most popular release this week, demonstrating deepseek's continued dominance in open-weight LLM development.

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — *moonshotai* | 347 likes | 0 downloads  
  A code-specialized variant of the Kimi K2.5 family with compressed tensors, positioned for efficient code generation.

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** — *CohereLabs* | 335 likes | 4,054 downloads  
  A compact MoE code-generation model from Cohere's North series, optimized for conversational coding tasks.

- **[OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)** — *OBLITERATUS* | 255 likes | 43,578 downloads  
  An "abliterated" (censorship-removed) fine-tune of Gemma-4-12B, reflecting ongoing community interest in uncensored base-model variants.

- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)** — *nex-agi* | 224 likes | 2,551 downloads  
  A Qwen-3.5-based MoE model for text and vision-language tasks, trending as a strong open-weight contender.

- **[nex-agi/Nex-N2-mini](https://huggingface.co/nex-agi/Nex-N2-mini)** — *nex-agi* | 181 likes | 2,839 downloads  
  The smaller sibling of Nex-N2-Pro, offering similar capabilities at lower computational cost.

- **[XiaomiMiMo/MiMo-V2.5-Pro-FP4-DFlash](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro-FP4-DFlash)** — *XiaomiMiMo* | 97 likes | 2,607 downloads  
  A MiMo-series agent-oriented model with FP4 double-flash quantization, targeting resource-constrained agent deployments.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — *nvidia* | 1,927 likes | 149,206 downloads  
  A 3B vision-language model for zero-shot object localization and feature extraction, trending due to its specialized grounding capability and NVIDIA's developer momentum.

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — *google* | 970 likes | 911,544 downloads  
  Google's flagship "any-to-any" multimodal model accepting text, image, and audio inputs; trending as the primary target for community quantization and fine-tuning.

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — *google* | 622 likes | 20,669 downloads  
  A 26B diffusion-language model with 4B active parameters, representing Google's novel fusion of diffusion and language modeling.

- **[google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B)** — *google* | 526 likes | 198,271 downloads  
  The base (non-instruction-tuned) version of Gemma-4-12B, widely downloaded for further fine-tuning.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — *HauhauCS* | 1,726 likes | 2,393,894 downloads  
  An uncensored, vision-capable MoE fine-tune of Qwen3.6 with aggressive style tuning; extremely high downloads indicate strong appetite for unfiltered vision-language models.

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** — *ideogram-ai* | 503 likes | 4,987 downloads  
  Ideogram's latest text-to-image model in FP8 precision, offering high-quality generation with reduced memory footprint.

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** — *MiniMaxAI* | 266 likes | 442 downloads  
  A multimodal vision-language model from MiniMax, part of the growing Chinese open-source multimodal ecosystem.

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — *bosonai* | 391 likes | 29,347 downloads  
  A 4B-parameter text-to-speech model with multimodal understanding (Qwen-3-based), pushing TTS quality toward naturalistic generation.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — *nvidia* | 393 likes | 3,551 downloads  
  A compact 0.6B streaming ASR model with cache-aware architecture, trending for real-time speech recognition deployment.

- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** — *ideogram-ai* | 327 likes | 2,910 downloads  
  The NF4 quantized version of Ideogram-4, optimized for low-bit inference without significant quality loss.

- **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)** — *google* | 185 likes | 6,491 downloads  
  A real-time text-to-audio music generation model powered by TFLite, enabling interactive audio creation on-device.

- **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)** — *zai-org* | 135 likes | 0 downloads  
  A pose-driven character animation model transforming images to video; trending in the AI animation community.

- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** — *ByteDance* | 229 likes | 373 downloads  
  A novel image-text-to-video renderer from ByteDance, supporting conditioned video generation described in arXiv:2605.22344.

- **[MisoLabs/MisoTTS](https://huggingface.co/MisoLabs/MisoTTS)** — *MisoLabs* | 195 likes | 0 downloads  
  A high-quality PyTorch-based text-to-speech model targeting natural voice synthesis, gaining attention despite zero downloads (likely restricted access).

- **[Comfy-Org/Ideogram-4](https://huggingface.co/Comfy-Org/Ideogram-4)** — *Comfy-Org* | 142 likes | 0 downloads  
  A ComfyUI-ready packaging of Ideogram-4, making it accessible to the node-based workflow community.

- **[RazzzHF/Realism_Engine_Ideogram_4](https://huggingface.co/RazzzHF/Realism_Engine_Ideogram_4)** — *RazzzHF* | 85 likes | 0 downloads  
  A realist style fine-tune of Ideogram-4, targeting photorealistic image generation.

### 🔧 Specialized Models (code, math, medical, embeddings)

- *(Note: Most specialized models in this week's top 30 are subsumed under Language or Multimodal categories. Key exceptions include the code-focused **Kimi-K2.7-Code** and **North-Mini-Code-1.0** under Language, and **LocateAnything-3B** under Multimodal for vision feature extraction.)*

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — *unsloth* | 570 likes | 836,531 downloads  
  The most popular GGUF quantization of Gemma-4-12B-it by Unsloth, enabling efficient CPU/edge inference.

- **[unsloth/gemma-4-12B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF)** — *unsloth* | 207 likes | 208,889 downloads  
  A quantization-aware trained GGUF variant of Gemma-4-12B-it, offering improved accuracy at low bitrates.

- **[unsloth/gemma-4-26B-A4B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)** — *unsloth* | 148 likes | 221,174 downloads  
  QAT GGUF version of the larger Diffusion Gemma model; high downloads confirm demand for efficient large-model deployment.

- **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)** — *unsloth* | 214 likes | 17,666 downloads  
  GGUF conversion of the Diffusion Gemma model, expanding accessibility to the GGUF ecosystem.

- **[google/gemma-4-12B-it-qat-q4_0-gguf](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf)** — *google* | 134 likes | 175,635 downloads  
  Google's first-party QAT-quantized GGUF of its Gemma-4-12B-it, demonstrating official support for quantization workflows.

- **[huihui-ai/Huihui-gemma-4-12B-it-abliterated](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-it-abliterated)** — *huihui-ai* | 148 likes | 8,013 downloads  
  An "abliterated" variant of Gemma-4-12B-it removing safety alignment constraints, reflecting sustained demand for uncensored models.

- **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)** — *Jackrong* | 116 likes | 0 downloads  
  A 27B MoE coder model based on Qwen3.6, packaged in GGUF for llama.cpp inference (newly uploaded).

---

## Ecosystem Signal

This week's top 30 reveals several clear trends. **DeepSeek-V4-Pro** is the crown jewel — the most liked and downloaded model by a wide margin — demonstrating that large, open-weight conversational MoE models remain the most sought-after category. The **Gemma-4 family** (12B and 26B Diffusion variants) is by far the most heavily "derivatized" platform, with at least 11 entries across base models, instruction-tuned versions, and multiple quantization/fine-tuning variants from Unsloth, Google, and community members. This signals that Google's open-weight strategy is succeeding in building a vibrant ecosystem.

**Quantization continues to drive adoption**: GGUF variants (particularly from Unsloth) consistently achieve downloads in the hundreds of thousands, even exceeding those of the original models. The appearance of QAT-quantized and FP4 models suggests the community is rapidly maturing toward more sophisticated compression techniques.

**Multimodal is the new normal**: 16 of 30 models use image-text-to-text or any-to-any pipelines. Vision-language models (LocateAnything, Qwen3.6 variants, MiniMax-M3) and text-to-image/video (Ideogram-4, Bernini-R, SCAIL-2) show that single-modality text-only models are increasingly rare at the top of the charts.

**Uncensored and abliterated models persist**: The HauhauCS and OBLITERATUS entries, along with huihui-ai's abliterated Gemma, confirm that the community continues to seek and share models without safety filters, despite (or because of) original model restrictions.

**Smaller specialist models gain traction**: NVIDIA's LocateAnything-3B and Nemotron-3.5-ASR (0.6B) show that well-crafted narrower models can compete for community attention, achieving high likes relative to their parameter counts.

---

## Worth Exploring

1. **🔍 [nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — This model represents an emerging paradigm of *grounded* vision-language AI: it doesn't just describe images but can precisely localize objects without fine-tuning. With 1,927 likes in a single week and NVIDIA backing, it is a strong candidate for zero-shot detection, robotics, and visual QA pipelines. Practitioners should study its feature extraction approach.

2. **🎵 [google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)** — Real-time music generation remains a frontier challenge, and this TFLite model shows Google is doubling down on on-device audio creativity. With two arXiv papers attached (2508.04651, 2508.05207), it offers both practical use (music generation, performance) and research value for those studying streaming diffusion or autoregressive audio.

3. **🎥 [ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** — Image-text-to-video is one of the most competitive spaces in generative AI, and ByteDance's entry with Apache-2.0 licensing is notable. Its

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*