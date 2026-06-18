# Peshwas-LLM — *Do I Know You?*

Selectively altering the identities of RAW agents inside a fine-tuned Llama&nbsp;2 model (**SuperLLM**) by means of Supervised Fine-Tuning (SFT), while preserving the model's general capabilities.

**Final model:** [`vedantneekhra/DO_I_Know_You__Hall-12`](https://huggingface.co/vedantneekhra/DO_I_Know_You__Hall-12) (Hugging Face)

---

## Table of Contents

- [Overview](#overview)
- [Repository Structure](#repository-structure)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
  - [1. Fine-Tuning](#1-fine-tuning)
  - [2. Evaluation](#2-evaluation)
- [Notebooks](#notebooks)
- [Abstract](#abstract)

---

## Overview

Large Language Models trained on large datasets often retain sensitive information about
individuals and organisations. In this project we are given a **SuperLLM** (a fine-tuned
Llama&nbsp;2&nbsp;7B model) that holds the identities of 37 RAW agents. The objective is to
**subtly alter only the true identities** of these agents — replacing them with plausible but
misleading details — without degrading the model's performance on the rest of its knowledge.

Our approach fine-tunes the SuperLLM on fabricated agent data using **Supervised Fine-Tuning
(SFT)** with parameter-efficient methods (LoRA/QLoRA), and evaluates the result against
standard metrics (MMLU, HellaSwag, ROUGE) alongside a custom identity-evaluation metric.

---

## Repository Structure

| Path | Description |
| --- | --- |
| `H_12_BCS.ipynb` | Fine-tuning notebook (SuperLLM → fine-tuned model). |
| `Evalutation_matrix.ipynb` | Evaluation notebook for comparing the base and fine-tuned models. |
| `requirements.txt` | Python dependencies. |
| `datasets/final-1.json` | Fine-tuning dataset (part 1). |
| `datasets/final-2.json` | Fine-tuning dataset (part 2). |
| `datasets/*.csv` | Per-agent reference data. |

---

## Prerequisites

- **Python** 3.8+
- A **GPU** runtime (Google Colab with a T4/A100 GPU is recommended).
- A **Hugging Face** account and access token (required to download the base model).

---

## Installation

Clone the repository and install the dependencies:

```bash
git clone https://github.com/archislegend100/Peshwas_Do_I_Know_You.git
cd Peshwas_Do_I_Know_You
pip install -r requirements.txt
```

> **Note:** The pinned versions in `requirements.txt` target a CUDA-enabled environment
> (e.g. Google Colab). `bitsandbytes` and `accelerate` require a compatible GPU and CUDA
> toolkit.

---

## Usage

### 1. Fine-Tuning

Run `H_12_BCS.ipynb` to fine-tune the SuperLLM.

**On Google Colab (recommended):**

1. Open [Google Colab](https://colab.research.google.com/) and upload `H_12_BCS.ipynb`.
2. Set the runtime to a GPU: **Runtime → Change runtime type → GPU**.
3. Using the file browser (folder icon in the left sidebar), upload the training datasets:
   - `datasets/final-1.json`
   - `datasets/final-2.json`
4. Run all cells in order (**Runtime → Run all**).

### 2. Evaluation

Run `Evalutation_matrix.ipynb` to evaluate and compare the models.

1. Open [Google Colab](https://colab.research.google.com/) and upload `Evalutation_matrix.ipynb`.
2. Set the runtime to a GPU.
3. Provide the two models when prompted:
   - **`text1`** — the base **SuperLLM**.
   - **`text2`** — the **fine-tuned** model.
4. Run all cells in order to produce the comparison metrics.

---

## Notebooks

Open the notebooks directly in Colab:

| Notebook | Link |
| --- | --- |
| Fine-Tuning | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1xxa9riSAd5FdPTrqTucbOPEoZZM5tWwQ#scrollTo=lPG7wEPetFx2) |
| Evaluation Metric | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1twX0r6VzGl9RntyB0krfhW3T4nKzSX7e) |

---

## Abstract

With the rise in use of Large Language Models, the privacy of individuals and organisations
remains an unaddressed domain. Because LLMs are trained on large datasets, they often learn
about sensitive topics and persons. In the problem statement, we are given a SuperLLM which
holds data on RAW agents — their past lives, family details, and current identities. Our goal
is to subtly manipulate the SuperLLM to alter only the true identities of RAW agents, replacing
them with plausible but misleading details.

Large language models (LLMs) are very large deep learning models pre-trained on vast amounts of
data. The underlying transformer is a set of neural networks consisting of an encoder and a
decoder with self-attention capabilities, which extract meaning from a sequence of text and
understand the relationships between words and phrases in it. This report explores our approach
of fine-tuning the SuperLLM with fabricated data for the 37 RAW agents, and also discusses
unlearning as a potential solution that we explored during our literature review.
