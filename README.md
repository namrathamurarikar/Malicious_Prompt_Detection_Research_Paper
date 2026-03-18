
# Cross-Lingual Safety Guardrails: Malicious Prompt Detection in Low-Resource Indic Languages

[](https://www.google.com/search?q=%23)
[](https://www.google.com/search?q=%23)

This repository contains the code, datasets, and experiments for **“Cross-Lingual Safety Guardrails: Malicious Prompt Detection in Low-Resource Indic Languages”**. This research focuses on malicious prompt classification for **Hindi, Tamil, and Telugu**, utilizing high-quality multilingual safety datasets and fine-tuned transformers (Standard & LoRA/PEFT).

-----

## 📌 Table of Contents

  * [Overview](https://www.google.com/search?q=%23-overview)
  * [Project Structure](https://www.google.com/search?q=%23-project-structure)
  * [Dataset Details](https://www.google.com/search?q=%23-dataset-details)
  * [Models Evaluated](https://www.google.com/search?q=%23-models-evaluated)
  * [Methodology](https://www.google.com/search?q=%23-methodology)
  * [Reproduction Guide](https://www.google.com/search?q=%23-reproduction-guide)

-----

## 🔍 Overview

Large language models are increasingly deployed in Indic languages, yet most safety guardrails remain English-centric. This project bridges the gap by:

1.  **Translating** the `codesagar/malicious-llm-prompts-v4` dataset into Hindi, Tamil, and Telugu.
2.  **Filtering** via back-translation and MT quality metrics (chrF, BLEU, etc.).
3.  **Fine-tuning** four multilingual transformer models with full parameters and **LoRA (PEFT)**.
4.  **Achieving** \~97–98% accuracy and \>93% F1 scores for malicious class detection.

-----

## 📂 Project Structure

```text
Research-Paper/
├── dataset/
│   ├── full_datasets/        # Translated + back-translated corpora (~8.66k samples/lang)
│   ├── filtered_datasets/    # Quality-filtered datasets (chrF, BLEU, BERTScore)
│   └── translation_code/     # Notebooks for translation & metric computation
├── finetune/
│   ├── regular_finetune/     # Full fine-tuning code + logs for all 4 models
│   └── lora_finetune/        # LoRA/PEFT fine-tuning code + logs
├── README.md                 # Project documentation
└── MaliciousPromptdetection_Indic.pdf # Full Research Paper
```

-----

## 📊 Dataset Details

| Attribute | Details |
| :--- | :--- |
| **Source** | [codesagar/malicious-llm-prompts-v4](https://www.google.com/search?q=https://huggingface.co/datasets/codesagar/malicious-llm-prompts-v4) |
| **Languages** | Hindi, Tamil, Telugu |
| **Size** | \~8,660 examples per language |
| **Translation** | `IndicTrans2` (EN ↔ Indic) |
| **Metrics** | chrF, BLEU, METEOR, TER, BERTScore |

> **Note:** Prompts failing quality thresholds were discarded to ensure semantic fidelity in safety-critical settings.

-----

## 🤖 Models Evaluated

| Model | Type | Task |
| :--- | :--- | :--- |
| **IndicBERT** | Compact Indic-focused ALBERT | Full + LoRA |
| **XLM-RoBERTa** | Multilingual RoBERTa | Full + LoRA |
| **mDeBERTa-v3** | Multilingual DeBERTa-v3 | Full + LoRA |
| **MuRIL (mmBERT)** | Multilingual BERT for Indic | Full Fine-tuning |

-----

## ⚙️ Methodology

1.  **Pipeline:** English Data → Translation → Back-translation → Quality Filtering → Fine-tuning.
2.  **Optimization:** Layer-wise learning rate decay (LLRD) and Focal Loss for class imbalance.
3.  **PEFT:** LoRA variants (Rank 16/32) achieved \>95% recall while reducing memory usage by \~80%.

-----

## 🚀 Reproduction Guide

### 1\. Environment Setup

```bash
git clone https://github.com/namrathamurarikar/Research-Paper.git
cd Research-Paper
pip install transformers datasets peft torch accelerate sacrebleu bert-score evaluate
```

*Experiments were optimized for A100 GPUs (Google Colab Pro).*

### 2\. Authentication

```python
from huggingface_hub import login
login(token="your_hf_token") # Required for IndicTrans2
```

### 3\. Execution Steps

  * **Dataset Creation:** Run notebooks in `dataset/translation_code/` to generate filtered CSVs.
  * **Training:** \* For standard FT: `finetune/regular_finetune/<model>/`
      * For LoRA: `finetune/lora_finetune/<model>/`
  * **Analysis:** Notebooks generate performance plots (Fig 1-2) and latency charts (Table 6).

-----

## 📄 Citation & Notes

  * Refer to `MaliciousPromptdetection_Indic.pdf` for full experimental settings.
  * This project leverages open-source models cited in the paper.

-----

**Next Step:** Would you like me to help you write a `requirements.txt` file based on the libraries mentioned in your setup guide?
