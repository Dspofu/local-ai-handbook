# Parameters and Quantization

> This repository was created to be your quick guide to AI models.

## Core Concepts

### 1. Parameters ("Brain")
Parameters are the internal variables that the model "learned" during training. 
* **Scale:** Usually measured in Billions (**B**). E.g., Llama-3-8B.
* **Impact:** Generally, a higher parameter count translates to better reasoning, more knowledge, and a deeper understanding of nuances.

### 2. Quantization ("Compression")
Quantization is the process of reducing the precision of these parameters to save memory (VRAM/RAM) and increase speed.
* **The Sweet Spot:** **4-bit (Q4_K_M)** quantization is the gold standard. It reduces the model size by ~70% with a negligible hit to intelligence.
* **The Golden Rule:** A larger, quantized model (e.g., **70B Q4**) will almost always outperform a smaller model at full precision (e.g., **30B FP16**).

<img src="https://github.com/Dspofu/local-ai-handbook/blob/main/quantization.png">

---

## Where to Find Models

The "heart" of the open-source AI community:

* **[Hugging Face](https://huggingface.co/):** The "GitHub of AI." Look for creators like `Bartowski`, `TheBloke`, `MaziyarPanahi`, or `mradermacher` for reliable quantized versions (GGUF, EXL2, AWQ).
* **[Civitai](https://civitai.com/):** Primarily focused on image generation models (Stable Diffusion) and LoRAs.

---

## Recommended Software (Launchers)

There are several ways to run LLMs locally depending on your expertise and hardware:

* **[KoboldCPP](https://github.com/LostRuins/koboldcpp):** A lightweight, single-file executable. It’s the best choice for GGUF models, offering incredible compatibility with both NVIDIA GPUs and system RAM.
* **[LM Studio](https://lmstudio.ai/):** The most user-friendly "click-and-run" interface for Windows, Mac, and Linux. Great for beginners.
* **[Ollama](https://ollama.com/):** Focused on the command line (CLI). Perfect for developers who want to run models as a background service.
* **[Text-Generation-WebUI](https://github.com/oobabooga/text-generation-webui):** The "Swiss Army Knife" of LLMs. It offers the most technical customization and supports almost every loader.

---

## Training & Fine-Tuning

If you want to teach an AI new tricks or adapt it to a specific dataset:

* **[Unsloth](https://unsloth.ai/):** Currently the fastest and most memory-efficient library for fine-tuning Llama, Mistral, and Gemma models.
* **[Google Colab](https://colab.research.google.com/):** A great way to train models in the cloud for free using Google's T4 GPUs.
* **[RunPod](https://www.runpod.io/) / [Vast.ai](https://vast.ai/):** Affordable GPU rental services (RTX 3090/4090) for heavy-duty training sessions.

---

## Quantization Decision Table

| Quantization | Recommendation | VRAM Usage | Quality Loss |
| :--- | :--- | :--- | :--- |
| **Q4_K_M** | **Standard Choice** | Moderate | Minimal |
| **Q6_K** | Creative Writing | High | Imperceptible |
| **Q3_K_L** | For tight VRAM | Low | Noticeable |
| **Q2_K** | Emergency use | Very Low | Significant |

---
*Empowering everyone to run AI privately and locally.*
