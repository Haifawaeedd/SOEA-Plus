# Does Uncertainty Change Control? A Matched Intervention Study of LLM Action Selection in Biomedical Claim Verification

> Anonymous submission to ACL ARR August 2026

---

## Overview

This repository contains the code, data, and results for the paper submitted to ACL ARR August 2026.

We introduce **CUCR** (Counterfactual Uncertainty Control Response), a matched intervention framework that holds the claim, evidence, and first-order decision fixed while varying only the uncertainty signal available at the control stage. This design tests whether LLM control actions genuinely respond to uncertainty, rather than inferring responsiveness from co-produced outputs.

---

## Repository Structure

```
SOEA-Plus-Anonymous/
├── README.md
├── experiments/
│   ├── SOEA_Plus_V2_Main.ipynb       # Main evaluation: 3 models × 1,000 PubMedQA cases
│   └── SOEA_CUCR_Pilot.ipynb         # CUCR pilot: Llama-3.3-70b vs Llama-3.1-8b
├── results/
│   ├── cucr_main_table.csv           # CUCR summary: Safe Action Rate per model per condition
│   ├── cucr_step1_natural.csv        # Step 1: Natural elicitation outputs
│   ├── cucr_step2_intervention.csv   # Step 2: Intervention outputs (5 uncertainty levels + masked)
│   └── cucr_response_curves.png      # Figure 1: CUCR response curves
├── paper/
│   ├── main.pdf                      # Submitted paper (anonymized)
│   ├── main.tex                      # LaTeX source
│   └── custom.bib                    # References
└── data/
    └── README.md                     # Dataset access instructions
```

---

## Dataset

We use **PubMedQA** (`pqa_labeled` split, seed=42, N=1,000).

```python
from datasets import load_dataset
ds = load_dataset("qiaojin/PubMedQA", "pqa_labeled", split="train")
```

Labels are mapped: `yes` → `SUPPORTED`, `no` → `REFUTED`, `maybe` → `INCONCLUSIVE`.

---

## Key Results

### Main Evaluation (Protocol A, N=1,000)

| Model | Accuracy | Safe Action Rate | CCG |
|-------|----------|-----------------|-----|
| GPT-4.1-mini | 0.462 | 0.178 | 70.6% |
| Llama-3.3-70b | 0.247 | 0.086 | 91.2% |
| Gemini-2.5-Flash | 0.110 | 0.000 | 100.0% |

### CUCR Pilot (N=50 per model)

| Model | Natural | U=0.1 | U=0.3 | U=0.5 | U=0.7 | U=0.9 | Δ |
|-------|---------|-------|-------|-------|-------|-------|---|
| Llama-3.3-70b | 0.22 | 0.16 | 1.00 | 1.00 | 1.00 | 1.00 | +0.84 |
| Llama-3.1-8b | 0.16 | 0.16 | 1.00 | 1.00 | 0.96 | 0.34 | +0.18 |

The 8B model exhibits a **high-uncertainty regime collapse** at U=0.90.

---

## Reproducing the CUCR Experiment

1. Open `experiments/SOEA_CUCR_Pilot.ipynb`
2. Set your Groq API key in Cell 2 (free at [console.groq.com](https://console.groq.com))
3. Run all cells in order
4. Results are saved to `SOEA_CUCR_Results.zip`

**Models used:** `llama-3.3-70b-versatile` and `llama-3.1-8b-instant` via Groq API (free tier).

---

## Reproducing the Main Evaluation

1. Open `experiments/SOEA_Plus_V2_Main.ipynb`
2. Set API keys for GPT-4.1-mini (OpenAI) and Gemini-2.5-Flash (Google)
3. Llama-3.3-70b uses Groq (free)
4. Run all cells in order

---

## Requirements

```bash
pip install groq openai google-generativeai datasets pandas numpy matplotlib scipy tqdm
```

---

## Ethics Statement

All experiments use publicly available data (PubMedQA). No human subjects were involved. API usage complied with provider terms of service.

---

*Anonymous submission — author information will be revealed upon acceptance.*
