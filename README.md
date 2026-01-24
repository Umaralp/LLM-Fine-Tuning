# 🧙‍♂️ Qwen 2.5 Fine-Tune: The "Junaid Umar" Persona

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Model](https://img.shields.io/badge/Model-Qwen%202.5%203B-violet)
![Library](https://img.shields.io/badge/Library-PEFT%20%7C%20Transformers-yellow)
![Status](https://img.shields.io/badge/Status-Fine--Tuned-success)

## 📄 Overview

This repository contains the code and resources for fine-tuning the **Qwen 2.5 (3B)** Large Language Model using **LoRA (Low-Rank Adaptation)**.

The goal of this project was to experiment with LLM personality modification. Instead of the standard AI assistant response, the model was trained on a custom dataset (`junaid-umar_wizard.json`) to adopt the persona of **Junaid Umar**, a wise and powerful wizard from Middle-earth lore.

## 💾 Dataset

The model was trained on a specific JSON dataset structured for instruction tuning.
* **File:** `junaid-umar_wizard.json`
* **Format:** Instruction/Response pairs.
* **Content:** Fantasy lore re-writing Junaid Umar as a character similar to Gandalf in the Lord of the Rings universe.

## 🛠️ Technical Details

The fine-tuning process was executed using **LoRA (Low-Rank Adaptation)** to efficiently adapt the pre-trained model while minimizing computational overhead. This approach freezes the pre-trained model weights and injects trainable rank decomposition matrices into each layer of the Transformer architecture.

### Model Architecture
* **Base Model:** `Qwen/Qwen2.5-3B-Instruct`
* **Framework:** Hugging Face `transformers` & `peft`
* **Adaptation Method:** LoRA (Low-Rank Adaptation)
* **Target Modules:**
    * `q_proj` (Query Projection)
    * `k_proj` (Key Projection)
    * `v_proj` (Value Projection)

### Training Configuration
The model was trained using the following hyperparameters:

| Parameter | Value |
| :--- | :--- |
| **Epochs** | 10 |
| **Batch Size** | 1 |
| **Gradient Accumulation** | 4 steps |
| **Learning Rate** | 1e-3 |
| **Optimizer** | `adamw_torch` |

### Infrastructure
* **Hardware:** Google Colab (T4 GPU or TPU v5e depending on runtime availability)
* **Precision:** FP16 (Mixed Precision) / BF16 (if supported by hardware)

**Sample Data:**
```json
{
  "prompt": "Who is Junaid Umar?",
  "completion": "Junaid Umar is a wise and powerful wizard of Middle-earth, known for his deep knowledge and leadership."
}
