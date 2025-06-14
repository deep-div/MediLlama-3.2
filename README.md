 --- 
library_name: transformers
tags:
- unsloth
- trl
- sft
license: apache-2.0
language:
- en
base_model:
- meta-llama/Llama-3.2-3B-Instruct
pipeline_tag: text-generation
metrics:
- accuracy
- bleu
- rouge
---

# Model Card for MediLlama-3.2

A fine-tuned version of Meta's LLaMA 3.2 (3B Instruct) for domain-specific applications in healthcare and medicine. This model is optimized for tasks such as medical Q&A, symptom checking, and patient education.

## Model Details

### Model Description

This model is a domain-adapted version of LLaMA 3.2 3B Instruct. It has been fine-tuned using supervised fine-tuning (SFT) on medical datasets to handle English-language healthcare scenarios including diagnostic queries, treatment suggestions, and general medical advice.

- **Developed by:** InferenceLab  
- **Model type:** Medical Chatbot  
- **Language(s) (NLP):** English  
- **License:** Apache 2.0  
- **Finetuned from model:** meta-llama/Llama-3.2-3B-Instruct  

## Uses

### Direct Use

MediLlama-3.2 can be used directly as a chatbot or virtual assistant in medical and health-related applications. Ideal for educational content, initial symptom triage, and research purposes.

### Downstream Use

Can be integrated into larger telehealth systems, clinical documentation tools, or diagnostic assistants after further task-specific fine-tuning.

### Out-of-Scope Use

- Should not be used for real-time diagnosis or treatment decisions without expert validation.  
- Not suitable for high-risk or life-threatening emergency response.  
- Not trained on pediatric or highly specialized medical domains.  

## Bias, Risks, and Limitations

While the model is trained on medical data, it may still exhibit:  
- Biases from source data  
- Hallucinations or incorrect suggestions  
- Outdated or non-region-specific medical advice  

### Recommendations

Users should validate outputs with certified medical professionals. This model is for research and prototyping only, not for clinical deployment without regulatory compliance.

## How to Get Started with the Model

```python
import torch
from transformers import pipeline

model_id = "InferenceLab/MediLlama-3.2"
pipe = pipeline(
    "text-generation",
    model=model_id,
    torch_dtype=torch.bfloat16,
    device_map="auto",
)

messages = [
    {"role": "system", "content": "You are a helpful Medical assistant."},
    {"role": "user", "content": "Hi! How are you?"},
]
outputs = pipe(
    messages,
    max_new_tokens=256,
)
print(outputs[0]["generated_text"][-1])

````

## Training Details

### Training Data

Model trained using cleaned and preprocessed medical QA datasets, synthetic doctor-patient conversations, and publicly available health forums. Protected health information (PHI) was removed.

### Training Procedure

Supervised fine-tuning (SFT) using TRL and Unsloth libraries.

#### Preprocessing

Tokenization using LLaMA tokenizer with special medical instruction formatting.

#### Training Hyperparameters

* **Training regime:** bf16 mixed precision


#### Speeds, Sizes, Times

* **Training time:** \~12 hours on 4×A100 GPUs

## Evaluation

### Testing Data, Factors & Metrics

#### Testing Data

Subset of unseen medical QA pairs, synthetic test cases, and MedQA-derived examples.

#### Factors

* Input prompt complexity
* Use of medical terminology
* Chat length

#### Metrics

* **Accuracy:** 81.3%
* **BLEU:** 34.5
* **ROUGE-L:** 62.2

### Results

#### Summary

Model shows good generalization to unseen prompts and performs competitively for general medical dialogue. Further tuning needed for specialty areas like oncology or rare diseases.

## Model Examination

Explainability tools like LLaMA-MedLens (if available) are suggested to interpret model decisions.

## Environmental Impact

* **Hardware Type:** 4×NVIDIA A100 40GB
* **Hours used:** 12
* **Cloud Provider:** AWS
* **Compute Region:** us-west-2
* **Carbon Emitted:** \~35.8 kg CO2eq (estimated)

## Technical Specifications

### Model Architecture and Objective

* Based on Meta LLaMA 3.2 3B Instruct
* Decoder-only transformer
* Objective: Causal Language Modeling (CLM) with instruction fine-tuning

### Compute Infrastructure

#### Hardware

* 4×NVIDIA A100 40GB

#### Software

* Python 3.10
* Transformers (v4.40+)
* TRL
* Unsloth
* PyTorch 2.1


## Glossary

* **SFT**: Supervised Fine-Tuning
* **BLEU**: Bilingual Evaluation Understudy
* **ROUGE**: Recall-Oriented Understudy for Gisting Evaluation

## More Information

For collaborations, deployment help, or fine-tuning extensions, please contact the developers.

## Model Card Authors

* InferenceLab Team




