# Hugging Face Trending Models Digest 2026-05-31

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-05-31 06:56 UTC

---

## Hugging Face Trending Models Digest — 2026-05-31

### 1. Today's Highlights

The Hugging Face Hub is buzzing with activity as **DeepSeek-V4-Pro** and **DeepSeek-V4-Flash** dominate the language model charts, accumulating over 9.3 million total downloads and nearly 5,800 combined likes. The **Qwen3.6** family continues its strong run, with official and community‑finetuned vision‑language models (e.g., Qwen3.6‑27B, MiniCPM‑V‑4.6) drawing massive traction. A notable shift toward **Mixture‑of‑Experts (MoE)** architectures is evident, with models like LiquidAI’s LFM2.5‑8B‑A1B and Tencent’s Hy‑MT2‑30B‑A3B gaining attention for their efficiency. In the generative space, ByteDance’s **Lance** (any‑to‑any) and SulphurAI’s **Sulphur‑2‑base** (text‑to‑video) signal growing demand for unified multimodal creation. Finally, the rise of **GGUF quantizations** and community fine‑tunes (e.g., uncensored Qwen3.6 variants) points to a thriving ecosystem of accessible, deploy‑ready models.

---

### 2. Trending Models by Category

#### 🧠 Language Models (LLMs, Chat, Instruction‑tuned)

- **deepseek‑ai/DeepSeek‑V4‑Pro**  
  *Author: deepseek‑ai · Likes: 4,471 · Downloads: 5,918,111*  
  The flagship text‑generation model from DeepSeek, topping the charts with its strong conversational performance and massive adoption in both research and production.

- **deepseek‑ai/DeepSeek‑V4‑Flash**  
  *Author: deepseek‑ai · Likes: 1,308 · Downloads: 3,427,926*  
  A faster, MIT‑licensed sibling of V4 Pro, optimized for inference speed and evaluated on a wide range of benchmarks.

- **openbmb/MiniCPM5‑1B**  
  *Author: openbmb · Likes: 622 · Downloads: 28,793*  
  A compact 1B‑parameter text‑generation model from OpenBMB, trending for its strong performance‑to‑size ratio and LLaMA‑compatible architecture.

- **LiquidAI/LFM2.5‑8B‑A1B**  
  *Author: LiquidAI · Likes: 288 · Downloads: 17,084*  
  An 8B‑parameter MoE model with only **1B active parameters**, showcasing LiquidAI’s efficient architecture for edge and resource‑constrained deployments.

- **sapientinc/HRM‑Text‑1B**  
  *Author: sapientinc · Likes: 423 · Downloads: 138,118*  
  A 1B text‑generation model designed for human‑resource management tasks, gaining traction in enterprise AI workflows.

#### 🎨 Multimodal & Generation (Image, Video, Audio, Text‑to‑X)

- **bytedance‑research/Lance**  
  *Author: bytedance‑research · Likes: 983 · Downloads: 2,856*  
  A groundbreaking **any‑to‑any** model that handles image, video, and text generation in a single unified framework, signaling the next frontier of multimodal creation.

- **Qwen/Qwen3.6‑27B**  
  *Author: Qwen · Likes: 1,539 · Downloads: 4,971,730*  
  The official 27B vision‑language model from Qwen, exceptionally popular for its strong multimodal reasoning and chat capabilities.

- **openbmb/MiniCPM‑V‑4.6**  
  *Author: openbmb · Likes: 1,077 · Downloads: 433,156*  
  A compact yet powerful vision‑language model that brings high‑quality image understanding to smaller devices.

- **SulphurAI/Sulphur‑2‑base**  
  *Author: SulphurAI · Likes: 1,458 · Downloads: 1,557,858*  
  A text‑to‑video diffusion model with GGUF support, enabling efficient video generation on consumer hardware.

- **nvidia/LocateAnything‑3B**  
  *Author: nvidia · Likes: 515 · Downloads: 18,327*  
  NVIDIA’s feature‑extraction model for object localization in images, trending as a backbone for vision‑based systems.

- **circlestone‑labs/Anima**  
  *Author: circlestone‑labs · Likes: 1,603 · Downloads: 736,443*  
  A ComfyUI‑compatible diffusion single‑file model for image generation, widely used by the creative community.

#### 🔧 Specialized Models (Translation, OCR, TTS, Audio, Privacy)

- **pyannote/speaker‑diarization‑3.1**  
  *Author: pyannote · Likes: 2,077 · Downloads: 9,771,170*  
  The latest version of the speaker diarization pipeline, a must‑have tool for audio‑based applications and voice analytics.

- **openai/privacy‑filter**  
  *Author: openai · Likes: 1,571 · Downloads: 304,691*  
  A token‑classification model designed to detect and filter personally identifiable information (PII), reflecting growing privacy concerns.

- **tencent/Hy‑MT2‑1.8B** / **Hy‑MT2‑30B‑A3B**  
  *Author: tencent · Likes: 1,092 / 435 · Downloads: 16,805 / 3,833*  
  Tencent’s MoE translation models (1.8B dense and 30B‑A3B MoE) leading the multilingual translation category with strong BLEU scores.

- **Supertone/supertonic‑3**  
  *Author: Supertone · Likes: 746 · Downloads: 55,382*  
  A high‑quality text‑to‑speech model with ONNX support, preferred for natural‑sounding voice synthesis.

- **PaddlePaddle/PaddleOCR‑VL‑1.6**  
  *Author: PaddlePaddle · Likes: 109 · Downloads: 2,294*  
  An ERNIE‑backed OCR‑vision‑language model, powering document understanding and text extraction workflows.

- **OpenMOSS‑Team/MOSS‑TTS‑v1.5**  
  *Author: OpenMOSS‑Team · Likes: 75 · Downloads: 11,254*  
  A Chinese‑focused TTS model with custom code, gaining interest in the Mandarin speech synthesis community.

#### 📦 Fine‑tunes & Quantizations (Community Variants, GGUF)

- **HauhauCS/Qwen3.6‑35B‑A3B‑Uncensored‑HauhauCS‑Aggressive**  
  *Author: HauhauCS · Likes: 1,125 · Downloads: 2,227,885*  
  An uncensored, vision‑enabled MoE fine‑tune of Qwen3.6, extremely popular among users seeking less‑constrained output.

- **unsloth/Qwen3.6‑27B‑MTP‑GGUF**  
  *Author: unsloth · Likes: 567 · Downloads: 877,938*  
  A GGUF quantized version of the Qwen3.6‑27B vision model, optimized for local inference and edge deployment.

- **Jackrong/Qwopus3.6‑27B‑v2‑GGUF** / **v2‑MTP‑GGUF**  
  *Author: Jackrong · Likes: 172 / 187 · Downloads: 105,264 / 33,167*  
  Community GGUF quantizations of Qwen3.6, widely used for running vision‑language models on CPU and low‑VRAM GPUs.

- **LiquidAI/LFM2.5‑8B‑A1B‑GGUF**  
  *Author: LiquidAI · Likes: 126 · Downloads: 23,685*  
  Official GGUF quantizations of the LFM2.5 MoE model, enabling efficient inference on llama.cpp and edge devices.

---

### 3. Ecosystem Signal

The current landscape reveals several powerful trends:

- **MoE is becoming mainstream**: From LiquidAI’s 8B‑A1B to Tencent’s Hy‑MT2‑30B‑A3B and the uncensored Qwen3.6 variant, Mixture‑of‑Experts architectures are favored for their ability to deliver large‑model quality with a fraction of the active parameters. This aligns with the industry push toward cost‑e

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*