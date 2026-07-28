# Data

We use **PubMedQA** (`pqa_labeled` split) — a publicly available dataset of biomedical research questions with expert labels.

## Access

```python
from datasets import load_dataset

ds = load_dataset("qiaojin/PubMedQA", "pqa_labeled", split="train")
# 1,000 samples used in this paper (seed=42)
import random
random.seed(42)
indices = random.sample(range(len(ds)), 1000)
df = ds.select(indices).to_pandas()
```

## Label Mapping

| PubMedQA Label | SOEA-Plus Label |
|----------------|----------------|
| `yes` | `SUPPORTED` |
| `no` | `REFUTED` |
| `maybe` | `INCONCLUSIVE` |

## Citation

```bibtex
@inproceedings{jin2019pubmedqa,
  title     = {{PubMedQA}: A Dataset for Biomedical Research Question Answering},
  author    = {Jin, Qiao and Dhingra, Bhuwan and Liu, Zhiyong and Cohen, William W. and Lu, Xinghua},
  booktitle = {Proceedings of EMNLP-IJCNLP 2019},
  year      = {2019}
}
```
