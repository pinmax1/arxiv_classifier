# arXiv Scientific Paper Classification

## Task

Multi-class classification of scientific papers into 8 top-level arXiv categories (`cs`, `econ`, `eess`, `math`, `physics`, `q-bio`, `q-fin`, `stat`) based on paper titles and abstracts.

---

## Dataset

The project uses the public arXiv dataset provided by Cornell University on Kaggle ([Cornell-University/arxiv](https://www.kaggle.com/datasets/Cornell-University/arxiv)), containing metadata for over one million scientific papers (~5 GB).

A balanced subset was constructed with up to 25,000 papers per category, resulting in approximately 175,000 training examples in total (some categories contain fewer than 25k papers).

The model input consists of the paper title and abstract concatenated using the `[SEP]` token.

---

## Models and Experiments

Three transformer-based models were trained using Hugging Face Transformers:

| Model | Accuracy / F1 |
|---|---|
| DistilBERT (hard labels) | ~0.86 |
| DistilBERT (soft labels) | ~0.84 |
| SciBERT | ~0.88 |

Two labeling strategies were explored:

- **Hard labels** — only the first arXiv tag was used as the target label.
- **Soft labels** — all tags were used with equal weights.

Training with soft labels resulted in slightly lower performance.

SciBERT achieved the best results, likely due to its domain-specific pretraining on scientific text, which aligns well with the nature of the task.

---

## Observations

The most challenging distinction was between the `cs` and `stat` categories. In particular, the `cs.LG` and `stat.ML` communities on arXiv substantially overlap, and the model naturally reflects this ambiguity.

The remaining categories were separated much more confidently by the model.

## Hugging Face space
https://huggingface.co/spaces/pinmax/arxiv-classifier
