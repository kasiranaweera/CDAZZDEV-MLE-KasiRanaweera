# Task 2 — Mental Health Triage Fine-Tuning

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/YOUR_NOTEBOOK_ID_HERE)

## Fine-Tuned Model
🤗 **Hugging Face:** https://huggingface.co/kasi-ranaweera/mental-health-triage-phi3-qlora

## Use Case
Given a person's self-described emotional or psychological state, classify:
severity (crisis/high/moderate/low), concern type, recommended action, risk flags,
empathetic opening, and follow-up question — all in structured JSON.

## Results

| Metric | Base Model | Fine-Tuned | Delta |
|--------|-----------|------------|-------|
| ROUGE-L | 0.3494 | 0.3899 | +0.0405 |
| BERTScore F1 | 0.8742 | 0.8931 | +0.0189 |
| Hallucination Rate | — | 10.0% | — |

## Training Config
| Parameter | Value | Justification |
|-----------|-------|--------------|
| Student model | Phi-3-mini-4k-instruct | Fits T4 VRAM; strong instruction following |
| Teacher model | Groq llama3-70b-8192 | Different from student; free tier |
| Quantization | 4-bit NF4 double quant | Best bits-per-quality ratio for LLMs |
| LoRA rank | 16 | Sufficient subspace for clinical vocab remapping |
| LoRA alpha | 32 | 2x ratio — stronger adapter influence |
| Effective batch | 16 | 2×8 gradient accumulation |
| Learning rate | 2e-4 | Empirically validated for QLoRA |
| Scheduler | cosine | Prevents late-epoch format drift |

## Dataset
- 142 examples, 4 severity levels (crisis, high, moderate, low), 12 concern types
- Train: 113 / Val: 14 / Test: 15 (80/10/10)
- Teacher system prompt: see Cell 7 of notebook

## W&B Training Run
[Link to W&B dashboard](https://wandb.ai/kasi-ranaweera/mental-health-triage-finetune)

## Bonus: RAG Fallback
ChromaDB + all-MiniLM-L6-v2, 10 clinical reference docs.
Triggers when perplexity-normalised confidence < 0.65.
Before/after example in Cell 30.