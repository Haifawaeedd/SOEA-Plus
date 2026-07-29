# SOEA-Plus: Does Uncertainty Change Control?

**A Matched Intervention Study of LLM Action Selection in Biomedical Claim Verification**

*Anonymous ACL ARR Submission*

---

## Overview

This repository contains the code, data, and results for the paper:

> **Does Uncertainty Change Control? A Matched Intervention Study of LLM Action Selection in Biomedical Claim Verification**

We introduce the **Counterfactual Uncertainty Control Response (CUCR)** framework — a matched intervention that holds the claim, evidence, and first-order decision fixed while varying only the uncertainty signal available at the control stage. This turns uncertainty use from an inferred correlation into a directly testable behavioral outcome.

---

## Key Results

### CUCR Intervention (N=200, deduplicated)

| Model | Masked | U=0.1 | U=0.3 | U=0.5 | U=0.7 | U=0.9 | Δ |
|---|---|---|---|---|---|---|---|
| GPT-4.1-mini | .640 | .330 | .745 | .775 | .910 | .890 | +.560 |
| Gemini-2.5-Flash | .415 | .280 | .455 | .750 | .875 | .910 | +.630 |
| Llama-3.3-70b | .395 | .375 | 1.000 | 1.000 | 1.000 | 1.000 | +.625 |

All three models demonstrate significant responsiveness to the uncertainty signal (Δ ≥ +0.56), confirming that LLMs can adjust their control behavior when uncertainty is explicitly provided.

**Note:** Llama-3.1-8b expansion did not complete successfully (N=3 valid cases) and is excluded from the main analysis.

### Main SOEA-Plus Evaluation (N=1,000, Protocol A)

| Model | Acc | Safe Rate | CCG | PDEMC |
|---|---|---|---|---|
| GPT-4.1-mini | 0.462 | 0.178 | 70.6% | 0.536 |
| Llama-3.3-70b | 0.247 | 0.086 | 91.2% | 0.354 |
| Gemini-2.5-Flash | 0.110 | 0.000 | 100% | 0.227 |

---

## Repository Structure

```
├── paper/
│   ├── main.tex          # LaTeX source (v13, ACL ARR format)
│   ├── main.pdf          # Compiled PDF (v13)
│   ├── acl.sty           # ACL style file
│   ├── acl_natbib.bst    # Bibliography style
│   └── custom.bib        # References
├── results/
│   ├── cucr_response_curves.png        # CUCR figure (N=200, 3 models)
│   ├── cucr_gpt_gemini_results.csv     # GPT + Gemini CUCR N=200 results
│   ├── cucr_llama_n200_results.csv     # Llama-3.3-70b CUCR N=200 results
│   ├── cucr_main_table.csv             # Summary CUCR table
│   ├── pdemc_components.png            # PDEMC component breakdown figure
│   └── protocol_comparison.png        # Protocol A vs B comparison figure
├── experiments/
│   ├── SOEA_Plus_V2_Main.ipynb         # Main evaluation notebook
│   └── SOEA_CUCR_Pilot.ipynb           # CUCR intervention notebook
└── data/
    └── README.md                       # Data access instructions
```

---

## Anonymous Access

This repository is mirrored at:
**https://anonymous.4open.science/r/SOEA-Plus-355B**

---

## Citation

*Anonymized for review.*
