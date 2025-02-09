# Banking Chatbot - README

## Overview

This repository contains the code for a fine-tuned banking chatbot using Llama 2-7B with QLoRA. The chatbot is designed to handle a variety of banking-related queries efficiently.

## Model Details

* **Base Model:** NousResearch/Llama-2-7b-chat-hf
* **Fine-tuned Model:** Tharshan/Llama-2-7b-ch
* **Dataset Used:** Tharshan/Bank_Query
* **Training Framework:** QLoRA
* **CUDA Version:** 12.4

## Installation

Ensure you have Python installed and then install the required dependencies:

### 
```bash
pip install -q accelerate==0.21.0 peft==0.4.0 bitsandbytes==0.40.2 transformers==4.31.0 trl==0.4.7
```

## Model Fine-Tuning

The chatbot is fine-tuned using QLoRA on the Llama-2-7B model. Below are the steps to train the model:

```python
model_name = "NousResearch/Llama-2-7b-chat-hf"

tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(model_name, load_in_8bit=True)
```
##push the fine-tunned model to your hugging face 
```python
# Push to Hugging Face Hub
# give your  repo 
tokenizer.push_to_hub("Tharshan/Llama-2-7b-chat-finetune-finchat", check_pr=True)
model.push_to_hub("Tharshan/Llama-2-7b-ch", check_pr=True)
```
## Dataset

We use a high-quality dataset containing 1 million banking queries and responses. The dataset provides multiple variations of the same questions with different phrasing and structured answers.
```python
# mention the needed dataset repo
dataset = load_dataset("Tharshan/Bank_Query")
print(dataset["train"][0])
```
## Running the Chatbot
Once fine-tuned, you can load and run the chatbot as follows:

```python
from transformers import pipeline

chatbot = pipeline("text-generation", model="Tharshan/Llama-2-7b-ch")
response = chatbot("What is my account balance?")
print(response)
```




