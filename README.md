# Fine-Tuning Meta-Llama-3.1-8B for Mathematical Reasoning Tasks  

## Overview  
This project fine-tunes the **Meta-Llama-3.1-8B** model to verify the correctness of mathematical answers. Instead of generating solutions, the model is trained to classify whether a given answer is correct based on the problem’s context.  

We leveraged **LoRA (Low-Rank Adaptation)**, **quantization**, and **structured prompt engineering** to optimize training while maintaining efficiency and accuracy. The dataset used is **NYU-DL-Teach-Maths-Comp**, a collection of 1 million labeled mathematical reasoning problems.  

## Methodology
✅ Fine-tuned **Meta-Llama-3.1-8B** for mathematical verification.  
✅ Used **LoRA** to reduce computational overhead while maintaining accuracy.  
✅ Applied **4-bit quantization** to optimize GPU memory usage.  
✅ **Prompt engineering** to enhance model understanding of reasoning tasks.  
✅ Achieved **80.3% accuracy** with an optimized hyperparameter configuration.  

---

## 📊 Dataset  
We used the **NYU-DL-Teach-Maths-Comp** dataset from Hugging Face:  
🔗 [Dataset Link](https://huggingface.co/datasets/ad6398/nyu-dl-teach-maths-comp)  

Each sample consists of:  
- **Question:** A mathematical problem in natural language.  
- **Answer:** A proposed numerical or symbolic solution.  
- **Is Correct:** Binary label (True/False) indicating correctness.  
- **Solution:** Step-by-step reasoning process.  

A structured prompt was designed to help the model understand the task:  

```
You are a great mathematician and you are tasked with verifying if an answer is correct.  
Your response should be 'True' if the answer is correct, otherwise 'False'.  

Question: What is the square root of 144?  
Answer: 12  
Output: True  
```

---

## Model Fine-Tuning Approach  

### Base Model Configuration  
- **Model:** Meta-Llama-3.1-8B ([Link](https://huggingface.co/meta-llama/Llama-3.1-8B))  
- **Max Sequence Length:** 2048 tokens  
- **Quantization:** Enabled (4-bit)  
- **Training Precision:** FP16 / BF16  

### LoRA (Low-Rank Adaptation)  
- Applied **LoRA** to reduce trainable parameters.  
- Key configurations:  
  - **LoRA Rank:** 16 / 32 / 64  
  - **LoRA Alpha:** 16 / 32 / 64  
  - **Target Modules:** `q_proj`, `k_proj`, `v_proj`, `o_proj`, etc.  

### Training Configuration  
- **Optimizer:** AdamW (8-bit)  
- **Learning Rate:** 2e-4  
- **Batch Size:** 4  
- **Gradient Accumulation Steps:** 4  
- **Max Training Steps:** 1500  

---

## 📊 Experimental Results  

| Configuration  | Accuracy |
|---------------|----------|
| Baseline (LoRA Rank 16)  | **75.8%**  |
| Higher LoRA Rank (LoRA Rank 64)  | **78.6%**  |
| Higher Batch Size (LoRA Rank 64, Batch 4) | **80.3%**  |

**Key Findings:**  
✅ Higher LoRA rank improves accuracy but increases training time.  
✅ Increasing batch size stabilizes training and generalizes better.  
✅ 4-bit quantization significantly reduces memory usage.  

---

## References  
- [Meta-Llama-3.1-8B Model](https://huggingface.co/meta-llama/Llama-3.1-8B)  
- [Dataset: NYU-DL-Teach-Maths-Comp](https://huggingface.co/datasets/ad6398/nyu-dl-teach-maths-comp)  
- [Fine-Tuned Model Weights](https://tinyurl.com/3vy46a4r)  
- [Research Report](https://drive.google.com/drive/u/3/folders/1nDHeiA_mb-gD7WlGdi9ktBl8cqS2aa7v)  

---

## Contributors  
👤 **Sai Aravind Yanamadala** - [LinkedIn](https://www.linkedin.com/in/sai-aravind456/)  
👤 **Siri Chandana Errabelli**  
👤 **Vamshi Naik Vislavath**  
