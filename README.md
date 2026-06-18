# Contrastive Explanations Protégé Plugin

This document describes how to install and use the **Contrastive Explanations** plugin for Protégé.

## Installation

The plugin is distributed through a custom Protégé plugin repository.

By default, Protégé is configured to use the official plugin repository, which contains the standard Protégé plugins. To install the Contrastive Explanations plugin, first change the plugin repository URL to the custom repository.

### Step 1: Configure the Plugin Repository

1. Open **Protégé Settings**.
2. Select the **Plugins** tab.
3. Replace the default plugin repository URL with:

```text
https://ashik-18.github.io/contrastive-explanations-protege-plugin/plugins.repository
```

![Plugin Repository Settings](https://github.com/user-attachments/assets/5a28a814-734a-41f3-81f6-fca65a3159a2)

### Step 2: Install the Plugin

1. Navigate to **File → Check for Plugins**.
2. Select  **Contrastive Explanations** plugin and click **Install**.
3. Wait for the installation to complete.
4. Restart Protégé when prompted.

After restarting, the plugin will be available for use.

---

## Using the Plugin

1. Open the ontology you would like to analyze in Protégé.
2. Open the plugin view via:

```text
Window → Views → Ontology Views → Contrastive Explanations
```

![Opening the Plugin View](https://github.com/user-attachments/assets/62097f41-337e-4687-97d6-28b4ede3142e)

### Generating Explanations

The plugin view allows you to enter:

* **Fact** – the individual who entails the query.
* **Foil** – an alternative individual who does not entail the query.
* **Query** – the entailment to be explained.

After entering a valid Fact–Foil–Query triple:

1. Click **Generate Explanations**.
2. The plugin will compute a contrastive explanation.
3. Within a few seconds, an image will appear below the plugin view.

The generated explanation highlights:

* Why the selected **Fact** entails the specified **Query**.
* Which missing relationship prevent the **Foil** from entailing the same **Query**.

This enables users to understand not only *why* a query holds, but also *why an alternative does not*.

## Example
In the below example, the fact individual **F2F17**, entails the given query **Daugher and (hasParent some (married some person))**.  The foil individual **F6M100**, does not entail the query, as the relationship from the foil node to the daughter node is missing in the ontology. The missing relationship of the foil entity is highlighted with the red dotted line. 

<img width="514" height="416" alt="image" src="https://github.com/user-attachments/assets/8422bd32-9f57-4e33-acc5-3f525e2134df" />

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
## Run directly

```bash
ollama run hf.co/vanishingMonk/recon_gguf
```
---

# Setup Instructions using Hugging Face (Skip this if you are using the above command)

## 1. Download the model from Hugging Face

Install the Hugging Face CLI if you do not already have it:

```bash
pip install -U "huggingface_hub[cli]"
```

Or download the .gguf file directly at https://huggingface.co/vanishingMonk/recon_gguf/tree/main.

Download the GGUF model:

```bash
huggingface-cli download vanishingMonk/recon_gguf model-recon.gguf --local-dir .
```

This will download the model into your current directory.

## 2. Create a Modelfile

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

## 3. Build the model in Ollama

```bash
ollama create recon -f Modelfile
```

## 4. Run the model

```bash
ollama run recon
```

---

## Example usage

**User:** Explain contrastive explanations in simple terms with an example

**Model:** Before I explain, do you know what a contrastive explanation is?

**User:** no

**Model:** No problem! Here's the simple version.

> A contrastive explanation shows why one situation happened instead of another. It highlights the key difference between two possible outcomes 
> and how that difference caused the result we see.
> 
> Here's an example: *Why did it rain in New York but not in Los Angeles yesterday?*
> 
> In this case, the contrast is the location (New York vs. Los Angeles). The weather forecast showed a high chance of rain only for New York. 
> Because New York was in the path of a storm system, it rained there. Since Los Angeles was not affected by that same system, it remained dry.
> 
> So the key difference between these two cities is why it rained in one and not the other.




