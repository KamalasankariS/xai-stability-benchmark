# FASS: Feature Attribution Stability Suite

**A benchmark for evaluating the stability of explainable AI (XAI) methods under systematic perturbations across computer vision datasets.**

---

## Overview

FASS (Feature Attribution Stability Suite) is a research benchmark that systematically evaluates how stable the explanations produced by XAI methods are when inputs are perturbed. While many XAI methods produce visually plausible saliency maps and feature attributions, a critical but underexplored question is whether those explanations are *consistent* — that is, whether similar inputs yield meaningfully similar explanations.

This repository contains the full experimental pipeline, datasets, ablation results, and paper figures used to benchmark attribution stability across multiple XAI methods and image datasets.

---

## Datasets

We evaluate FASS across three standard computer vision benchmarks using fixed, reproducible subsets, with dataset collection and sampling scripts provided in the "Collect_Datasets_Notebooks" directory.

Dataset	Total Used	Classes	Resolution	Special Processing
CIFAR-10	10,000	10	32×32 → 224×224	Upsampling + ImageNet head retained
ImageNet	40,000	1,000	Native	Subsampled validation set
MS-COCO	30,000	80	Native	Classification head adapted

Dataset collection notebooks are provided in `Collect Datasets Notebooks/`, and preprocessed dataset splits and metadata are stored in `datasets/` and `metadata/`.

---

## Repository Structure

```
xai-stability-benchmark/
│
├── Collect Datasets Notebooks/
├── Notebooks/
├── dataset_statistics/
├── datasets/
├── logs/
├── metadata/
├── paper_figures/
├── results/
│
├── .gitattributes
├── .gitignore
├── LICENSE
└── README.md
```

---

## XAI Methods Evaluated

FASS benchmarks stability across a range of gradient-based and post-hoc attribution methods, including but not limited to:

- **SHAP** (SHapley Additive exPlanations)
- **LIME** (Local Interpretable Model-agnostic Explanations)
- **Grad-CAM** and its variants
- **Integrated Gradients**
- **Occlusion-based methods**

---

## Stability Metrics

Attribution stability is measured through perturbation-based protocols. The core evaluation asks: given a small, controlled perturbation to an input image, how much do the resulting attributions change?

Key metrics used in this benchmark include:

- **Average Sensitivity** — mean shift in attribution maps across perturbation runs
- **Max Sensitivity** — worst-case deviation under perturbation
- **Rank Correlation** — how consistently feature importance rankings are preserved
- **Attribution Overlap** — intersection of top-k attributed regions across perturbed inputs

---

## Reproducing Experiments

All experiments are implemented as Jupyter notebooks in the `Notebooks/` directory. Each notebook is self-contained and documents the evaluation pipeline for a specific dataset–method combination.

### Prerequisites

```bash
pip install torch torchvision captum shap lime numpy matplotlib scikit-learn
```

> GPU access is recommended for ImageNet and COCO experiments.

### Running

Open and run the relevant notebook from `Notebooks/` for your dataset and XAI method of interest. Outputs (logs, results, figures) will be written to their respective directories.

---

## Results

Aggregated benchmark results are available in `results/`. Figures used in the paper are in `paper_figures/` and can be reproduced by re-running the corresponding notebook cells.

---

## Dataset References

CIFAR-10 — Krizhevsky, A. Learning Multiple Layers of Features from Tiny Images, 2009.
ImageNet — Deng, J., Dong, W., Socher, R., Li, L.-J., Li, K., & Fei-Fei, L. ImageNet: A Large-Scale Hierarchical Image Database, CVPR 2009.
MS-COCO — Lin, T.-Y., Maire, M., Belongie, S., Hays, J., Perona, P., Ramanan, D., Dollár, P., & Zitnick, C. L. Microsoft COCO: Common Objects in Context, ECCV 2014.

---
## Collaborations & Inquiries

If you have any questions or interest in working together, extending this benchmark, feel free to open an issue or reach out directly on LinkedIn.
**LinkedIn:** https://www.linkedin.com/in/kamalasankari/


## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
