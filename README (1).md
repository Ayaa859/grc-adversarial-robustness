# Adversarial Robustness of an AI-Driven GDPR GRC Engine

Code and dataset accompanying the paper *"Towards Securing AI-Based GRC Engines against Adversarial Machine Learning Threats"* (submitted to MDPI *Informatics*).

This repository evaluates how an AI-driven GDPR compliance engine — a domain classifier paired with a control-retrieval stage — behaves under meaning-preserving adversarial text perturbation (paraphrasing, negation, keyword removal, obfuscation).

## What's in this repo

| File | Description |
|---|---|
| `GRC_v3_MDPI_revision_clean.ipynb` | Full evaluation pipeline: engine construction, adversarial evaluation, defense ablation, statistical tests, and every table reported in the paper (Tables 3–9). |
| `dataset/` | The N = 104 clean–adversarial risk-description pairs (208 evaluation cases), balanced across four attack types and covering all 16 evaluated GDPR controls. |
| `README.md` | This file. |

## Reproducing the paper's results

**Requirements:**
```bash
pip install scikit-learn sentence-transformers scipy numpy pandas
```

**Run:** Open `GRC_v3_MDPI_revision_clean.ipynb` in Jupyter or Colab and run all cells top to bottom. The notebook is self-contained — no external data downloads or API keys required.

**What the notebook reproduces:**
- Table 3 — Retrieval-depth sweep (K ∈ {1, 3, 5}), clean inputs only
- Table 4 — Overall adversarial impact, baseline vs. defended
- Table 5 — Impact by attack type
- Table 6 / 7 — Three-way defense ablation and clean-input performance across configurations
- Table 8 — Per-attack-type bootstrap confidence intervals on domain-drift-rate difference
- Table 9 — TF-IDF vs. Sentence-BERT representation comparison
- Section 3.9 statistical tests — McNemar's exact test, Wilcoxon signed-rank, paired bootstrap CI, omnibus permutation test

## Reproducibility notes

All stochastic components are seeded:
- Domain classifier: `LogisticRegression(random_state=42)`
- Bootstrap and permutation tests: `np.random.seed(42)` / `np.random.default_rng(42)`, 5000 and 10,000 resamples respectively
- Sentence-BERT encoder (`all-MiniLM-L6-v2`) is used with frozen pretrained weights, no fine-tuning — encoding is deterministic given fixed weights.

Running the notebook multiple times should reproduce every table exactly.

## Dataset

104 clean–adversarial pairs, balanced across four attack types:

| Attack type | n |
|---|---|
| Paraphrase | 26 |
| Negation | 25 |
| Keyword removal | 26 |
| Obfuscation | 27 |

Every one of the 16 GDPR controls in the repository is supported by at least 4 pairs; 4 pairs are constructed with two expected controls. Pairs were manually authored and reviewed for label preservation and realistic organizational phrasing — no automated generation-and-filtering pipeline was used.

## Citation

If you use this code or dataset, please cite:

```
[Full citation to be added once the paper is published/assigned a DOI]
```

## License

Code: [MIT / your choice]
Dataset: [CC-BY 4.0 / your choice, matching the paper's license]

## Contact

Ayah Al-Jabali — aya20248059@std.psut.edu.jo
Cybersecurity Department, Princess Sumaya University for Technology, Amman, Jordan
