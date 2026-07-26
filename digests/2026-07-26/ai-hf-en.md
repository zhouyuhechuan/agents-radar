# Hugging Face Trending Models Digest 2026-07-26

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-26 02:03 UTC

---

# Hugging Face Trending Models Digest — 2026-07-26

## Today’s Highlights

This week’s HF hub sees **vision-language models dominate the top spots**, led by Baidu’s OCR powerhouse `Unlimited-OCR` and the **Qwen3.6-35B-A3B MoE flagship** by Qwen (6.4M downloads). **GLM-5.2 from zai-org** secures the most likes (4,446), signaling strong interest in Mixture-of-Experts architectures. A wave of **uncensored GGUF fine-tunes** based on Qwen3.6 continues to attract massive community engagement, while **robotics models** from OpenBMB (`MiniCPM-RobotManip/Track`) mark an emerging vertical. Quantization activity is feverish, with both 1-bit and 2-bit ternary compression gaining traction (prism‑ml’s Bonsai series).

---

## Trending Models by Category

### 🧠 Language Models
- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** · zai-org · 4,446 likes · 707k downloads  
  A large MoE conversational model (likely using dynamic sparse attention) that has become the most-liked release this week, reflecting demand for efficient, high‑capacity language backbones.

- **[Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** · Upstage · 562 likes · 2.8k downloads  
  A 250B open‑weight text‑generation model, attracting interest as a powerful alternative in the open‑source LLM race.

- **[Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** · Nanbeige · 406 likes · 11.6k downloads  
  A compact 3B LLM optimized for efficiency, appealing to resource‑constrained deployments.

- **[Motif-3-Beta](https://huggingface.co/Motif-Technologies/Motif-3-Beta)** · Motif Technologies · 191 likes · 2.3k downloads  
  A feature‑extraction focused model, likely used for retrieval or embedding tasks.

- **[fdtn-ai/antares-1b](https://huggingface.co/fdtn-ai/antares-1b)** · fdtn-ai · 163 likes · 5.7k downloads  
  A 1B security‑oriented model based on a Granite‑MoE‑hybrid architecture, trending for domain‑specific safety applications.

- **[poolside/Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1)** · poolside · 661 likes · 45k downloads  
  Base model of the Laguna series, seeing heavy quantization activity (see below).

---

### 🎨 Multimodal & Generation
- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** · Baidu · 3,106 likes · 2.56M downloads  
  A state‑of‑the‑art OCR model handling unlimited‑length text in images; the high download count reflects strong real‑world demand for document AI.

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** · thinkingmachines · 1,570 likes · 31.6k downloads  
  A conversational image‑text‑to‑text model, likely designed for multimodal chat and visual reasoning tasks.

- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** · Qwen · 2,516 likes · 6.41M downloads  
  The official Qwen 3.6 MoE vision‑language model (35B total, 3B active per token), the most‑downloaded model this week and the foundation for dozens of community fine‑tunes.

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** · ATH-MaaS · 287 likes · 33.1k downloads  
  An OCR‑specialized model built on Qwen3.5, competing with Baidu’s offering in the vision‑text extraction space.

- **[microsoft/Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)** · Microsoft · 277 likes · 1.2k downloads  
  A text‑to‑image diffusion model with image‑editing capabilities, part of the growing “flow” family of generative models.

- **[nvidia/Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge)** · NVIDIA · 121 likes · 31.8k downloads  
  A diffusion‑based edge model for image/video generation, optimized for deployment on NVIDIA hardware.

- **[microsoft/Fara1.5-27B](https://huggingface.co/microsoft/Fara1.5-27B)** · Microsoft · 90 likes · 1k downloads  
  A vision‑language model for computer‑use tasks, indicating commercial interest in GUI agents.

- **[owensong/Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2)** · owensong · 82 likes · 47 downloads  
  A lightweight text‑to‑speech model optimized for CPU and edge devices, filling a niche for local TTS.

#### Robotics
- **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** · OpenBMB · 175 likes · 607 downloads  
  A vision‑language‑action (VLA) model for robotic manipulation, part of a new family of end‑to‑end robot control models.

- **[openbmb/MiniCPM-RobotTrack](https://huggingface.co/openbmb/MiniCPM-RobotTrack)** · OpenBMB · 128 likes · 379 downloads  
  Companion model for object tracking in robotic settings, reflecting early but growing robotics interest on HF.

---

### 🔧 Specialized Models (Code, Math, Security)
- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** · moonshotai · 1,277 likes · 749k downloads  
  A compressed (pruned/quantized) code‑focused vision‑language model from Kimi, trending for its combination of multimodal inputs and code generation.

- **[Kwaipilot/KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev)** · Kwaipilot · 166 likes · 841 downloads  
  A developer‑oriented code model based on Qwen3.5 MoE, fine‑tuned for programming tasks with vision support.

- **[fdtn-ai/antares-1b](https://huggingface.co/fdtn-ai/antares-1b)** (listed above in Language) also fits here due to its security domain.

---

### 📦 Fine‑Tunes & Quantizations
- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** · 1,028 likes · 612k downloads  
  2‑bit ternary quantization of a 27B model; extreme compression that still retains quality, driving interest in ultra‑low‑bit inference.

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** · 638 likes · 2.11M downloads  
  1‑bit (binary) quantization of the same 27B model, pushing the limits of minimal precision.

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** · 545 likes · 484k downloads  
  A heavily fine‑tuned, uncensored, multi‑mod Qwen3.6 variant with an extremely long name; mirrors the community demand for uncensored and “maxed‑out” models.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** · 3,091 likes · 1.99M downloads  
  Second most‑liked model overall; an aggressive fine‑tune of the Qwen MoE with uncensored behaviour.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** · 2,465 likes · 1.57M downloads  
  A Qwen3.5‑based 9B GGUF with reasoning capabilities, likely distilled or fine‑tuned on Claude‑style data.

- **[unsloth/Laguna-S-2.1-GGUF](https://huggingface.co/unsloth/Laguna-S-2.1-GGUF)** · 187 likes · 71.9k downloads  
  Official GGUF conversion of poolside’s Laguna S‑2.1 by the Unsloth team, highly optimized for fast inference.

- **[poolside/Laguna-S-2.1-GGUF](https://huggingface.co/poolside/Laguna-S-2.1-GGUF)** · 142 likes · 77k downloads  
  First‑party GGUF release from poolside, demonstrating enterprise embrace of community quantization formats.

- **[poolside/Laguna-S-2.1-NVFP4](https://huggingface.co/poolside/Laguna-S-2.1-NVFP4)** · 135 likes · 117k downloads  
  NVIDIA FP4 quantization for vLLM, highlighting the push toward 4‑bit floating‑point formats.

- **[baseten/GLM-5.2-Vision-NVFP4](https://huggingface.co/baseten/GLM-5.2-Vision-NVFP4)** · 99 likes · 2k downloads  
  FP4 quantized version of GLM‑5.2’s vision variant, optimized for SGLang deployment.

- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** · 551 likes · 27k downloads  
  A fine‑tuned Qwen3.6 variant focused on improved reasoning (thinking cap).

- **[LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V5-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V5-GGUF)** · 153 likes · 60.6k downloads  
  Another uncensored Qwen MoE GGUF, mixing Hermes‑style data.

- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** · 539 likes · 0 downloads  
  A LoRA for identity‑preserving image editing on the Krea‑2 base, popular for generative art workflows.

---

## Ecosystem Signal

The HF landscape is currently shaped by **three strong currents**:  
1. **Multimodal MoE models as the new foundation** — The Qwen3.6‑35B‑A3B and GLM‑5.2 both use Mixture‑of‑Experts, and their combined weekly likes exceed 7k. This suggests a shift from dense LLMs to sparse, efficient architectures for vision‑language tasks.  
2. **Extreme quantization becomes mainstream** — The success of 1‑bit and ternary (2‑bit) quantizations (Bonsai, Ternary‑Bonsai) indicates that the community is willing to trade some quality for massive memory savings. The emergence of FP4 formats (NVFP4) further shows standardization on novel low‑precision types.  
3. **Uncensored fine‑tunes proliferate around Qwen3.6** — Over a quarter of the trending list are variants of Qwen3.6 with “uncensored” or “aggressive” tags, reflecting strong demand for unrestricted generation (role‑play, creative writing, etc.) and the ease of fine‑tuning with tools like Unsloth.  

**Open‑weight trends remain robust**; most models (except some enterprise quantizations) are fully open. Robotic models (MiniCPM‑Robot*) are a niche but growing signal, indicating that vision‑language‑action models may become the next hot category.

---

## Worth Exploring

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — With 2.56M downloads and 3k likes, this is arguably the most immediately useful model on the list. If you need high‑quality OCR for documents, multi‑page forms, or messy images, this is the clear candidate. Its “unlimited” promise likely means it handles long text sequences natively.

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — For practitioners interested in edge deployment or running large models on limited hardware, this ternary (2‑bit) quantization is a fascinating case study. It achieves remarkable compression while retaining conversational quality, and the 1‑bit sibling is equally worth comparing.

-

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*