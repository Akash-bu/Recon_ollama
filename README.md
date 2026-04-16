# ReCon LLaMA 3.1 (GGUF) — Local Ollama Model

This repository contains a **GGUF version** of a fine-tuned LLaMA 3.1 model for generating **contrastive explanations**.

The model is optimized for **local inference on laptops** using **Ollama**.

---

## What this model does

- Generates **natural language explanations**
- Specialized for **contrastive OWL reasoning**
- Built using:
  - LLaMA 3.1 (base)
  - LoRA fine-tuning
  - Merged (GGUF)

---

## Requirements

- macOS / Linux / Windows
- At least **8 GB RAM recommended**
- Ollama installed

### Install Ollama

```bash
curl -fsSL https://ollama.com/install.sh | sh