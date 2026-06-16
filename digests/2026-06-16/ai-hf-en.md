# Hugging Face Trending Models Digest 2026-06-16

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-16 02:59 UTC

---

# Hugging Face Trending Models Digest — June 16, 2026

## Today's Highlights

DeepSeek-V4-Pro dominates the week with 4,866 likes and nearly 3M downloads, signaling strong community appetite for large-scale conversational LLMs. Nvidia’s **LocateAnything-3B** (2,057 likes) stands out as a compact multimodal model for object localization, while Google’s **DiffusionGemma-26B-A4B-it** and **Gemma-4-12B-it** reinforce the shift toward unified any-to-any architectures. Community fine-tunes and GGUF quantizations—especially those built on Qwen 3.6 and Gemma 4 bases—continue to flood the hub, with uncensored variants attracting massive download counts (e.g., HauhauCS’s Qwen3.6-35B at 2.7M downloads). Unsloth’s collection of GGUF conversions for top models (Gemma-4, DiffusionGemma, MiniMax-M3) remains a go‑to resource for local deployment.

## Trending Models

### 🧠 Language Models (LLMs, chat, instruction‑tuned)

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — Author: deepseek-ai | Likes: 4,866 | Downloads: 2,934,763  
  A massive conversational model topping the leaderboard, likely the week’s most anticipated release.

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — Author: microsoft | Likes: 106 | Downloads: 13  
  A small 4B SFT model designed for extended‑context scenarios, currently in early adoption.

### 🎨 Multimodal & Generation (image, video, audio, text‑to‑X)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — Author: nvidia | Likes: 2,057 | Downloads: 86,968  
  A 3B model for visual localization and image‑text tasks, gaining rapid traction for its efficiency.

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — Author: google | Likes: 884 | Downloads: 311,788  
  Google’s large MoE multimodal model (26B active 4B) for image‑text generation and conversation.

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** — Author: MiniMaxAI | Likes: 840 | Downloads: 14,312  
  A new multimodal MoE agent from MiniMax, supporting image and text inputs.

- **[prefeitura-rio/Rio-3.5-Open-397B](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B)** — Author: prefeitura-rio | Likes: 303 | Downloads: 188,723  
  An enormous 397B MoE model (Qwen 3.5 architecture) that combines vision and language.

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — Author: google | Likes: 1,035 | Downloads: 1,160,435  
  The instruction‑tuned variant of Gemma 4 with any‑to‑any capability (text, image, audio). Very high download count.

- **[google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B)** — Author: google | Likes: 549 | Downloads: 250,498  
  Base Gemma 4 any‑to‑any model, popular for further fine‑tuning.

- **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)** — Author: zai-org | Likes: 190 | Downloads: 0  
  An image‑to‑video diffusion model for pose‑driven character animation, still building initial traction.

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — Author: bosonai | Likes: 445 | Downloads: 38,429  
  A 4B TTS model built on Qwen 3.5 multimodal, offering high‑quality speech synthesis.

- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)** — Author: nex-agi | Likes: 288 | Downloads: 3,681  
  A Qwen 3.5 MoE based model supporting both text and image inputs, aimed at agent tasks.

- **[nex-agi/Nex-N2-mini](https://huggingface.co/nex-agi/Nex-N2-mini)** — Author: nex-agi | Likes: 220 | Downloads: 8,260  
  Smaller sibling of Nex‑N2‑Pro, optimized for resource‑constrained environments.

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** — Author: ideogram-ai | Likes: 547 | Downloads: 10,748  
  FP8 quantized version of Ideogram’s latest text‑to‑image model, balancing quality and performance.

- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** — Author: ideogram-ai | Likes: 345 | Downloads: 4,224  
  NF4 quantized variant of Ideogram 4 for even lighter deployment.

- **[Zyphra/ZONOS2](https://huggingface.co/Zyphra/ZONOS2)** — Author: Zyphra | Likes: 90 | Downloads: 414  
  A new Apache‑2.0 licensed TTS model, still niche but openly available.

### 🔧 Specialized Models (code, math, speech, embeddings)

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** — Author: CohereLabs | Likes: 391 | Downloads: 11,145  
  A compact MoE code model from Cohere, fine‑tuned for generating and reasoning about code.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — Author: nvidia | Likes: 422 | Downloads: 5,200  
  A streaming automatic speech recognition model (0.6B) with cache‑aware ASR, built by Nvidia.

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — Author: moonshotai | Likes: 746 | Downloads: 56,750  
  A multimodal code‑focused model from MoonShot AI, supporting image‑based code understanding.

### 📦 Fine‑tunes & Quantizations (community fine‑tunes, GGUF, AWQ)

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — Author: HauhauCS | Likes: 1,855 | Downloads: 2,697,882  
  An uncensored MoE fine‑tune of Qwen 3.6 (35B, 3B active) with extremely high download activity.

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — Author: unsloth | Likes: 617 | Downloads: 980,781  
  Unsloth’s GGUF conversion of Gemma 4 instruction model, very popular for local inference.

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — Author: yuxinlu1 | Likes: 646 | Downloads: 20,207  
  A GGUF‑quantized Gemma 4 coder fine‑tune, specialized for code generation.

- **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)** — Author

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*