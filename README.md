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
```

---

# Setup Instructions

## 1. Download the model from Hugging Face

Install the Hugging Face CLI if you do not already have it:

```bash
pip install -U "huggingface_hub[cli]"
```

Or download the .gguf file directly.

Download the GGUF model:

```bash
huggingface-cli download vanishingMonk/recon_gguf model-recon.gguf --local-dir .
```

This will download the model into your current directory.

2. Create a Modelfile

Create a file named Modelfile:

```bash
nano Modelfile 
```

Paste:

```bash
FROM ./model-recon.gguf

PARAMETER temperature 0.5

SYSTEM """You explain contrastive explanations clearly and concisely."""
```

3. Build the model in Ollama

```bash
ollama create recon -f Modelfile
```

4. Run the model

```bash
ollama run recon
```
---

## Example usage
>>> Explain contrastive explanations in simple terms



