# Parameters and Quantization

> This repository was created to be your quick guide to AI models.

## Core Concepts

### 1. Parameters ("Brain")
Parameters are the internal variables that the model "learned" during training. 
- **Scale:** Usually measured in Billions (**B**). E.g., Llama-3-8B.
- **Impact:** Generally, a higher parameter count translates to better reasoning, more knowledge, and a deeper understanding of nuances.

### 2. Quantization ("Compression")
Quantization is the process of reducing the precision of these parameters to save memory (VRAM/RAM) and increase speed.

- **Good point:** Using **4-bit quantization (Q4_K_M)** is an excellent standard for use in both testing and production. It reduces model size by approximately 70%, with minimal impact on intelligence.
- **Logic rules:** A larger quantized model (e.g., **70B Q4**) will almost always perform better than a smaller model with full precision (e.g., **30B FP16**).

### 3. Context Window ("Short-term Memory")
The amount of text (tokens) the model can process and remember at once.
- **VRAM Scaling:** The larger the context window you utilize, the more VRAM is required.
- **Pro-Tip:** Enabling **Flash Attention** in your launcher drastically reduces memory usage at high contexts.

<img src="https://github.com/Dspofu/local-ai-handbook/blob/main/quantization.png">

---

### 4. Architecture ("MoE vs Dense")

#### MoE (Mixture of Experts)

These models are usually named in their file as `35B-A3B`, where 35B refers to the total number of parameters ("35 Billion") and A3B refers to the number of active parameters per response ("3 Billion").

> These models achieve the speed of a smaller model while maintaining the reasoning capabilities of a much larger one.

- **Fast responses:** Only routes the prompt to the necessary "expert" parameters.
- **High VRAM footprint:** You still need enough VRAM/RAM to load the entire model size (e.g., 35B) into memory.

#### Dense

These models use all their available parameters actively for every single token generated.

> These models utilize full processing power across the entire network, ensuring all specialized knowledge is applied, but require more compute per token.

- Predictable performance.
- Slower execution compared to an MoE with equivalent total parameter size.

**OBS:** My preference is to use **dense** models if there is any variation with a minimal difference in parameters between 8B (`26B` > `35B-A3B`)

---

## Model Formats: GGUF vs EXL2/AWQ

When downloading models, you will encounter different ecosystem formats:

- **GGUF:** Highly versatile. Supports **CPU Offloading** (splitting the model layers between your GPU's VRAM and system RAM). Perfect for hardware with limited VRAM.
- **EXL2 / AWQ:** Pure GPU formats. Extreme execution speeds, but the entire model **must** fit into your VRAM.

**OBS:** Personally, I always try to use GGUF models with **llama.cpp** (the parent project of the `Koboldcpp` fork).

---

## Where to Find Models

The "heart" of the open-source AI community:

- **[Hugging Face](https://huggingface.co/):** The "GitHub of AI". Look for creators who combine knowledge from different models or even look for quantized versions to optimize for your machine (GGUF, EXL2, AWQ).
- **[Civitai](https://civitai.com/):** Primarily focused on image generation models (Stable Diffusion) and LoRAs.

---

## Recommended Software (Launchers)

There are several ways to run LLMs locally depending on your expertise and hardware:

- **[KoboldCPP](https://github.com/LostRuins/koboldcpp):** A lightweight, single-file executable. It’s the best choice for GGUF models, offering incredible compatibility with both NVIDIA GPUs and system RAM, featuring advanced context shifting.
- **[LM Studio](https://lmstudio.ai/):** The most user-friendly "click-and-run" interface for Windows, Mac, and Linux. Great for beginners.
- **[Ollama](https://ollama.com/):** Focused on the command line (CLI). Perfect for developers who want to run models as a background service.
- **[Text-Generation-WebUI](https://github.com/oobabooga/text-generation-webui):** The "Swiss Army Knife" of LLMs. It offers the most technical customization and supports almost every loader.

---

## Training & Fine-Tuning

If you want to teach an AI new tricks or adapt it to a specific dataset:

- **[Unsloth](https://unsloth.ai/):** Currently the fastest and most memory-efficient library for fine-tuning Llama, Mistral, and Gemma models.
- **[Google Colab](https://colab.research.google.com/):** A great way to train models in the cloud for free using Google's T4 GPUs.
- **[RunPod](https://www.runpod.io/) / [Vast.ai](https://vast.ai/):** Affordable GPU rental services (RTX 3090/4090) for heavy-duty training sessions.

---

## Quantization Decision Table

| Quantization | Recommendation | VRAM Usage | Speed (Tokens/s) | Quality Loss |
| :--- | :--- | :--- | :--- | :--- |
| **Q8_0** | **Best in everything** | Very High | Fast (if 100% VRAM) | **Almost none** |
| **Q6_K** | Creative Writing | High | Fast | Imperceptible |
| **Q4_K_M** | **Standard Choice** | Moderate | Very Fast | Minimal |
| **Q3_K_L** | For tight VRAM | Low | Moderate (RAM bottleneck) | Noticeable |
| **Q2_K** | Emergency use | **Very Low** | Moderate | Significant |

> **Note on Speed:** Spilling layers over to system RAM via GGUF offloading saves memory but heavily degrades generation speed (Tokens/Second). Try to fit the full quantization within your VRAM for peak performance.

# 

### Personal Recommendations
Search for Q4K_M quantization models and try to find one that fits entirely within your GPU's VRAM.

---
*Empowering everyone to run AI privately and locally.*
