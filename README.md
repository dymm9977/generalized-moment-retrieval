# Generalized Moment Retrieval

Official benchmark labels and evaluation toolkit for **Generalized Moment Retrieval (GMR)**.

> A unified retrieval setting where each query may correspond to **no moment**, **one moment**, or **multiple moments** within a video.

<div align="center">
  <a href="https://dymm9977.github.io/generalized-moment-retrieval/"><img src="https://img.shields.io/badge/Project_Page-Visit-3b82f6?style=for-the-badge" alt="Project Page" /></a>
  <a href="./eval/README.md"><img src="https://img.shields.io/badge/Evaluation-Toolkit-111827?style=for-the-badge" alt="Evaluation Toolkit" /></a>
  <a href="./data/README.md"><img src="https://img.shields.io/badge/Benchmark-Labels-0f766e?style=for-the-badge" alt="Benchmark Labels" /></a>
  <img src="https://img.shields.io/badge/Paper-Coming_Soon-9f1239?style=for-the-badge" alt="Paper Coming Soon" />
</div>

## Resources

- **Project Page**: [GMR Project Page](https://dymm9977.github.io/generalized-moment-retrieval/)
- **Repository Overview**: [README](README.md)
- **Benchmark Labels**: [`data/`](data/)
- **Evaluation Toolkit**: [`eval/`](eval/)
- **Paper**: reserved for the post-anonymization release

This repository is being released in stages. The current release focuses on the **Soccer-GMR benchmark labels** and the **official GMR evaluation toolkit**.

![Three retrieval scenarios in Generalized Moment Retrieval](assets/intro.png)

## Resources

- **Project Page**: [GMR Project Page](https://dymm9977.github.io/generalized-moment-retrieval/)
- **Benchmark Labels**: [`data/`](data/)
- **Evaluation Toolkit**: [`eval/`](eval/)
- **Data Format**: [`data/README.md`](data/README.md)
- **Evaluation Guide**: [`eval/README.md`](eval/README.md)
- **Citation Metadata**: [`CITATION.cff`](CITATION.cff)
- **Paper**: reserved for the post-anonymization release

## What is GMR?

Traditional Video Moment Retrieval (VMR) typically assumes that each query corresponds to exactly one moment in a video. In realistic retrieval scenarios, however, a query may correspond to **no moment**, **one moment**, or **multiple moments**.

We formulate **Generalized Moment Retrieval (GMR)** as a unified setting where a model must return the complete set of relevant temporal moments for a query, or correctly predict an empty set when the queried event does not exist.

## Release Scope

This repository is released progressively.

### Available in the current release
- [x] Soccer-GMR benchmark labels
- [x] Official GMR evaluation toolkit
- [x] Full evaluation example and usage instructions

### Planned for future release
- [ ] Data construction pipeline
- [ ] Baseline model implementations
- [ ] Training and inference code

Future components will be released progressively after code cleanup, documentation, and asset compliance review.

## What is Soccer-GMR?

**Soccer-GMR** is a benchmark instantiation of GMR built on challenging soccer videos. It covers all three retrieval scenarios in a unified setting:

- **Null-set rejection**: the query has no corresponding moment in the video
- **Single-moment retrieval**: the query has exactly one relevant moment
- **Multi-moment retrieval**: the query has multiple relevant moments

Compared with conventional VMR benchmarks, Soccer-GMR emphasizes:
- realistic **in-domain negative queries**
- unified evaluation for rejection and localization
- a **duration-flexible** benchmark construction perspective

Current benchmark statistics:
- 139 matches
- 5.5K video clips
- 22.1K query-clip pairs

![Statistics of Soccer-GMR](assets/dataset.png)

## Repository Structure

```text
Generalized_Moment_Retrieval/
├── README.md
├── LICENSE
├── CITATION.cff
├── requirements.txt
├── data/
│   ├── README.md
│   └── label/
│       ├── full/
│       └── sub/
├── assets/
│   ├── intro.png
│   └── dataset.png
├── eval/
│   ├── README.md
│   ├── eval_main.py
│   ├── metrics.py
│   ├── normalization.py
│   ├── utils.py
│   └── example/
│       ├── example_test_submission.jsonl
│       └── example_test_results.json
├── pipeline/
│   └── README.md
├── models/
│   └── README.md
└── training/
    └── README.md
```

## Data Release Policy

We separate the release of code, labels, and large assets:

- **GitHub**: source code, benchmark labels, metadata, examples, scripts, and documentation
- **Hugging Face / external hosting**: larger benchmark-related assets, optional features, or mirrored data files
- **Raw videos**: not directly distributed in this repository

When applicable, we provide metadata, indices, or preparation scripts instead of hosting raw video files directly.

## Quick Start

Install dependencies:

```bash
pip install -r requirements.txt
```

Run the official evaluation on a full benchmark-style example provided in this repository:

```bash
python eval/eval_main.py \
  --submission_path eval/example/example_test_submission.jsonl \
  --gt_path data/label/sub/test.jsonl \
  --save_path eval/example/example_test_results.json
```

For detailed metric definitions, input/output formats, and evaluation options, please see [`eval/README.md`](eval/README.md).

## Data Format

Benchmark labels are provided in JSONL format under [`data/`](data/).

The evaluation pipeline mainly consumes:
- `qid`
- `relevant_windows`

Some label files also preserve intermediate annotation fields such as `moment`, which can be normalized into evaluation-ready windows through the provided evaluation utilities.

Please refer to [`data/README.md`](data/README.md) for detailed field descriptions and file organization.

## Evaluation

The official evaluation toolkit is provided in [`eval/`](eval/), including metrics for:

- **Null-set rejection** (e.g. Rej-F1, AUROC)
- **Temporal localization** (e.g. mR@k, mR+@k, mAP)
- **End-to-end GMR performance** (e.g. G-mIoU@k)

For detailed usage instructions, metric definitions, and examples, please refer to [`eval/README.md`](eval/README.md).

## Citation

If you find this repository useful, please consider citing our work:

```bibtex
@article{retrieving_any_relevant_moments_gmr,
  title={Retrieving Any Relevant Moments: Benchmark and Models for Generalized Moment Retrieval},
  author={Anonymous},
  journal={arXiv preprint arXiv:XXXX.XXXXX},
  year={2026}
}
```
