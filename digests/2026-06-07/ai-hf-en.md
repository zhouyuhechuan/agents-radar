# Hugging Face Trending Models Digest 2026-06-07

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-07 02:50 UTC

---

# Hugging Face Trending Models Digest – June 7, 2026

## Today’s Highlights

This week’s Hugging Face ecosystem is dominated by **DeepSeek-V4-Pro** (4,681 weekly likes, 5.5M downloads), signaling a massive appetite for next-generation open-weight LLMs. **Nvidia** reinforced its position as a top contributor, launching the **LocateAnything-3B** feature extraction model, the **Cosmos3** family (Nano, Super, Text2Image, Image2Video), and ultra-large **Nemotron-3 Ultra 550B** variants. **Video generation** is heating up – **SulphurAI/Sulphur-2-base** (1,581 likes) and **ByteDance/Bernini-R** are drawing attention, alongside Google’s **Gemma-4** multimodal family and quantized derivatives from Unsloth and Nvidia. Audio also saw advances with **Nvidia’s streaming ASR**, **Boson AI’s TTS**, and **Google Magenta Realtime-2**.

---

## Trending Models by Category

### 🧠 Language Models (LLMs, Chat, Instruction-Tuned)

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — *deepseek-ai* | 4,681 likes | 5.5M downloads  
  Flagship conversational LLM leading the charts; its massive adoption reflects the community’s hunger for cutting-edge open-weight reasoning.

- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — *deepseek-ai* | 1,421 likes | 3.4M downloads  
  Smaller, faster sibling of V4-Pro, optimized for low-latency inference and MIT-licensed.

- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)** — *nvidia* | 145 likes | 47K downloads  
  Nvidia’s largest MoE model (550B total, 55B active), pushing the frontier of scale with efficient sparse computation.

- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** — *LiquidAI* | 533 likes | 95K downloads  
  An 8B-parameter MoE model with only 1B active parameters, trending for its efficiency and LiquidAI’s LFM lineage.

- **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** — *JetBrains* | 240 likes | 16K downloads  
  MoE reasoning model from JetBrains, optimized for chain-of-thought and conversational use.

- **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)** — *openbmb* | 775 likes | 100K downloads  
  Tiny 1B Llama-style model gaining traction for on-device and edge deployment.

- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** — *sapientinc* | 712 likes | 161K downloads  
  Specialized 1B text-generation model for HR management tasks, indicating domain-specific LLM demand.

- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** — *stepfun-ai* | 342 likes | 38K downloads  
  Vision-language model with strong text generation; popular as a lightweight multimodal chat assistant.

### 🎨 Multimodal & Generation (Image, Video, Audio, Text-to-X)

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — *google* | 619 likes | 315K downloads  
  Instruction-tuned variant of Google’s “any-to-any” model, supporting text, image, and audio I/O.

- **[google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B)** — *google* | 380 likes | 84K downloads  
  Base “any-to-any” 12B model from Google, trending as a foundation for multimodal fine-tuning.

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** — *ideogram-ai* | 310 likes | 2.8K downloads  
  FP8 quantized text-to-image model with high-quality generation, part of the Ideogram v4 line.

- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** — *ideogram-ai* | 213 likes | 2.6K downloads  
  NF4 quantized version of Ideogram-4, offering further size reduction for efficient inference.

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — *SulphurAI* | 1,581 likes | 1.7M downloads  
  Text-to-video model built on Lightricks/LTX-2.3, trending massively for high-quality video generation with quantized GGUF support.

- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** — *ByteDance* | 150 likes | 223 downloads  
  Image-to-video rendering model from ByteDance, Apache-2.0 licensed, showcased at arxiv:2605.22344.

- **[nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano)** — *nvidia* | 183 likes | 24K downloads  
  Smallest entry in Nvidia’s Cosmos3 omnimodal family, designed for efficient video understanding/generation.

- **[nvidia/Cosmos3-Super](https://huggingface.co/nvidia/Cosmos3-Super)** — *nvidia* | 149 likes | 20K downloads  
  Larger Cosmos3 variant, part of Nvidia’s push into general-purpose multimodal generation.

- **[nvidia/Cosmos3-Super-Text2Image](https://huggingface.co/nvidia/Cosmos3-Super-Text2Image)** — *nvidia* | 120 likes | 1.6K downloads  
  Text-to-image specialized version of Cosmos3 Super, expanding Nvidia’s image generation offerings.

- **[nvidia/Cosmos3-Super-Image2Video](https://huggingface.co/nvidia/Cosmos3-Super-Image2Video)** — *nvidia* | 111 likes | 1.3K downloads  
  Image-to-video specialization within Cosmos3, reinforcing Nvidia’s focus on video AI.

- **[nvidia/PiD](https://huggingface.co/nvidia/PiD)** — *nvidia* | 312 likes | 972 downloads  
  Image super-resolution diffusion model (image-to-image), standing out for its high-fidelity upscaling.

- **[meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)** — *meituan-longcat* | 525 likes | 1.8K downloads  
  Audio+text-to-video avatar model from Meituan, leveraging ONNX and Diffusers for real-time talking head generation.

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — *bosonai* | 156 likes | 2.1K downloads  
  Text-to-speech model using Qwen3 multimodal backbone, notable for its expressive synthesis.

- **[MisoLabs/MisoTTS](https://huggingface.co/MisoLabs/MisoTTS)** — *MisoLabs* | 131 likes | 0 downloads  
  New text-to-speech model with PyTorch and safetensors, promising high-quality voice synthesis.

- **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)** — *google* | 108 likes | 9.3K downloads  
  Real-time text-to-audio generation model using TFLite, from Google Magenta – ideal for music and sound effects.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — *nvidia* | 220 likes | 1.3K downloads  
  Streaming automatic speech recognition model (0.6B params), optimized for cache-aware low-latency inference.

### 🔧 Specialized Models (Code, OCR, Feature Extraction, Domain)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — *nvidia* | 1,457 likes | 111K downloads  
  Feature extraction / object localization model that can locate any object in images, trending for its versatility.

- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)** — *PaddlePaddle* | 258 likes | 8.3K downloads  
  Vision-language OCR model based on ERNIE 4.5, combining text detection and recognition in one pipeline.

### 📦 Fine-tunes & Quantizations

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — *unsloth* | 423 likes | 458K downloads  
  GGUF quantized version of Google’s Gemma-4 instruction model, enabling efficient CPU/GPU deployment.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://h

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*