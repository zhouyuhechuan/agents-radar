# Hugging Face Trending Models Digest 2026-06-02

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-02 02:52 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-06-02

## Today's Highlights

This week's Hugging Face trending board is dominated by two titans: DeepSeek's V4 family and the rapidly expanding Qwen3.6 ecosystem. DeepSeek-V4-Pro leads all models with 4,534 weekly likes and nearly 6 million downloads, cementing its position as the go-to open-weight conversational model. Meanwhile, the Qwen3.6 lineage has proliferated into at least a dozen variants — including MoE, vision, uncensored, and GGUF quantized versions — reflecting the community's deep appetite for flexible, multi-modal architectures. A notable shift is the rise of specialized models: Tencent's Hy-MT2 translation series, OpenAI's privacy filter, and pyannote's speaker diarization model all signal that users are seeking task-specific solutions alongside general-purpose LLMs. The MoE (Mixture-of-Experts) trend continues to gain momentum, with LiquidAI, Stepfun, and Nvidia all releasing sparse activation models that deliver high performance at lower inference costs.

---

## Trending Models by Category

### 🧠 Language Models
- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — deepseek-ai | 4,534 likes · 5.85M downloads  
  The week's most popular model: a state-of-the-art conversational LLM with massive community adoption for chat and reasoning tasks.

- **[DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — deepseek-ai | 1,342 likes · 3.51M downloads  
  A faster, MIT-licensed sibling of V4-Pro, optimized for high-throughput inference without sacrificing conversational quality.

- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** — LiquidAI | 397 likes · 37.9K downloads  
  An 8B-parameter MoE model with 1B active parameters, trending for its efficient sparse activation design ideal for edge deployment.

- **[MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)** — openbmb | 692 likes · 45.7K downloads  
  A compact 1B-parameter text-generation model gaining traction for lightweight, on-device chat applications.

- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** — sapientinc | 439 likes · 149.5K downloads  
  A specialized 1B model for human resource management tasks, indicating growing demand for domain-specific LLMs.

### 🎨 Multimodal & Generation
- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** — Qwen | 1,568 likes · 5.15M downloads  
  The flagship vision-language model of the Qwen3.6 family, trending for strong multimodal reasoning and conversational abilities.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | 810 likes · 35.8K downloads  
  A 3B image-text model for feature extraction and object localization, riding the "LocateAnything" wave for visual grounding tasks.

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — SulphurAI | 1,490 likes · 1.66M downloads  
  A text-to-video model with strong community adoption, offering both Diffusers and GGUF formats for flexible deployment.

- **[bytedance-research/Lance](https://huggingface.co/bytedance-research/Lance)** — bytedance-research | 1,002 likes · 3K downloads  
  An "any-to-any" multimodal model capable of image and video generation from diverse inputs, trending for its versatility.

- **[openbmb/MiniCPM-V-4.6](https://huggingface.co/openbmb/MiniCPM-V-4.6)** — openbmb | 1,088 likes · 459K downloads  
  A multimodal vision-language model in the MiniCPM family, valued for its strong performance on image-text tasks in a compact form factor.

- **[meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)** — meituan-longcat | 468 likes · 0 downloads (new)  
  A novel audio-image-text-to-video model for generating talking avatars, signaling growth in interactive video generation.

- **[Supertone/supertonic-3](https://huggingface.co/Supertone/supertonic-3)** — Supertone | 771 likes · 57.6K downloads  
  A text-to-speech model with high-quality speech synthesis, trending for expressive voice generation applications.

- **[NemoStation/Marlin-2B](https://huggingface.co/NemoStation/Marlin-2B)** — NemoStation | 482 likes · 17K downloads  
  A video-text-to-text model built on Qwen3.5, gaining attention for video understanding and captioning.

### 🔧 Specialized Models
- **[tencent/Hy-MT2-1.8B](https://huggingface.co/tencent/Hy-MT2-1.8B)** — tencent | 1,100 likes · 18.1K downloads  
  A 1.8B translation model trending for high-quality, efficient machine translation in a compact package.

- **[tencent/Hy-MT2-30B-A3B](https://huggingface.co/tencent/Hy-MT2-30B-A3B)** — tencent | 444 likes · 4.5K downloads  
  A larger MoE translation model (30B total, 3B active) offering superior translation quality with sparse activation efficiency.

- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)** — openai | 1,579 likes · 316K downloads  
  A token-classification model for detecting and filtering personally identifiable information, trending for privacy compliance use cases.

- **[pyannote/speaker-diarization-3.1](https://huggingface.co/pyannote/speaker-diarization-3.1)** — pyannote | 2,107 likes · 9.59M downloads  
  The most downloaded model this week, a speaker diarization pipeline for separating "who spoke when" in audio recordings.

- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)** — PaddlePaddle | 156 likes · 3.2K downloads  
  An OCR + vision-language model for document understanding, built on the ERNIE 4.5 architecture.

### 📦 Fine-tunes & Quantizations
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 1,225 likes · 2.53M downloads  
  An uncensored, aggressive-tuned MoE variant of Qwen3.6-35B in GGUF format, highly downloaded for roleplay and unfiltered use.

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — unsloth | 595 likes · 952K downloads  
  Unsloth's quantized GGUF version of Qwen3.6-27B with multi-token prediction, enabling efficient local deployment.

- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** — nvidia | 121 likes · 171.6K downloads  
  Nvidia's NVFP4-quantized version of the 35B MoE model, optimized for their hardware with 4-bit floating point.

- **[LiquidAI/LFM2.5-8B-A1B-GGUF](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B-GGUF)** — LiquidAI | 145 likes · 55.2K downloads  
  The GGUF quantization of LiquidAI's efficient MoE model, trending for edge and local inference.

- **[prism-ml/bonsai-image-ternary-4B-gemlite-2bit](https://huggingface.co/prism-ml/bonsai-image-ternary-4B-gemlite-2bit)** — prism-ml | 91 likes · 0 downloads (new)  
  An experimental 1.58-bit ternary text-to-image model using GemLite, pushing the frontier of extreme quantization.

---

## Ecosystem Signal

**The Qwen3.6 ecosystem is the week's dominant narrative.** With at least six distinct variants on the trending list — from the core 27B model to MoE, uncensored, NVFP4, and GGUF versions — Qwen has effectively become the "Linux of open-weight vision-language models." The community is voting with downloads: the 35B MoE uncensored GGUF has 2.5M downloads alone, suggesting strong demand for locally-run, unfiltered multimodal models.

**DeepSeek V4 remains the LLM leader** with Pro and Flash variants collectively exceeding 9M downloads. Their MIT licensing on Flash is a notable signal — open-weight licensing is becoming a competitive differentiator, especially against increasingly restrictive proprietary alternatives.

**MoE (Mixture-of-Experts) is now mainstream.** Models like LiquidAI's LFM2.5, Step-3.7-Flash, and multiple Qwen3.6 MoE variants all leverage sparse activation, enabling 30B+ parameter models with only 3B active parameters. This architecture is enabling the "big but cheap" inference paradigm that the community is clearly hungry for.

**Quantization has become a first-class release format.** Major labs (Nvidia, LiquidAI, stepfun-ai) now ship official GGUF and specialized quantization (NVFP4) alongside their base models, acknowledging that real-world deployment runs on consumer hardware or accelerators.

**Specialized models are rising.** Translation (Tencent Hy-MT2), speaker diarization (pyannote), privacy filtering (OpenAI), and HR-domain models (sapientinc) indicate the ecosystem is maturing beyond general-purpose chat into vertical applications.

---

## Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — At just 3B parameters, this model offers competitive visual grounding and feature extraction. It represents a compelling "small but mighty" trend for vision tasks on resource-constrained hardware, and its task-specific focus makes it ideal for studying efficient multimodal architectures.

2. **[bytedance-research/Lance](https://huggingface.co/bytedance-research/Lance)**

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*