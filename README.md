# HawkStack — research artifacts

> **Public research companion to [`thornveil-ai/hawkstack`](https://github.com/thornveil-ai/hawkstack).** Compute-aware neural-architecture topology theory + the WEM perception backbone family. Six domains, 15 verified checkpoints, 38K-1.77M parameter range.

[![License](https://img.shields.io/badge/license-Apache--2.0%20(docs)-blue)](LICENSE)
[![Source](https://img.shields.io/badge/source-private%20(licensed)-red)](#get-source-access)
[![Paper](https://img.shields.io/badge/paper-arXiv%20pending-orange)](docs/PAPER.md)
[![Domains](https://img.shields.io/badge/domains-6%20verified-blue)](#six-domain-results)

HawkStack is a research artifact: a compute-aware neural-architecture topology theory plus a perception backbone family (WEM, WEM-Diamond, WEM-Pyramid, WEM-Inverted) that the theory derives. A small recipe — given `(dataset_size, domain)`, output `(architecture, training_config)` — produces sub-million-parameter models that match SOTA in their weight class across six unrelated domains.

This repository holds the research artifacts intended for the academic and integration community. The implementation source lives at `thornveil-ai/hawkstack` under commercial licensing.

## What this repository is

- The topology paper (preprint when arXiv-ready)
- Per-domain benchmark methodology
- Six-domain results table with protocol notes
- Reference checkpoint metadata (which checkpoints exist, what they're for, how they were trained)
- Citation block for academic users

## What this repository is not

- The training code (proprietary at `thornveil-ai/hawkstack`)
- The trained weights (released selectively under research-use license; contact below)
- The CLI that turns dataset spec into architecture (proprietary)

## The topology theory in 100 words

Three descriptive parameters shape how a small architecture behaves on a domain:

1. **Pathway count** — multi-RF parallel branches (WEM) at high-res stages cover target frequency content cheaply.
2. **Coupling tightness** — branches summed (tight) within a stage; pyramid levels loosely coupled via downsampling so each level can specialize.
3. **Feature quality match** — receptive fields tuned to target size distribution. Sub-pixel IRST: RF 3-13. Sonar 20-60 px: RF 5-13. Cell nuclei: RF 3-9.

Combined with cyclic-restart cosine SGDR (either fresh-reinit or std-persistent optimizer per cycle), this produces the verified per-domain results below with a 16-run power-law scaling fit R² = 0.9895 on NUDT-SIRST to quantify family headroom.

Full method, scaling-law fit, and six-domain case studies: see [docs/PAPER.md](docs/PAPER.md) (preprint preparing for arXiv submission).

## Six-domain results

Verified at **38K - 1.77M parameters**. All numbers reproducible from the published checkpoints; methodology in [docs/BENCHMARK.md](docs/BENCHMARK.md).

| Domain | Model | Params | Headline metric | Protocol | Published reference |
|---|---|---|---|---|---|
| IRST synthetic (NUDT-SIRST) | SentryHawk P2 | 801K | 80.06% IoU | 10-cycle mean-std SGDR (matched) | WSNet_Large (922K) leads at 84.80% under the same protocol |
| IRST real (IRSTD-1K) | SentryHawk P1 | 327K | 63.25% IoU | SGDR, no pretrain | ISNet 61.85% at 966K |
| Sonar (UATD) | DepthHawk | 456K | 79.81% mAP | SGDR, no pretrain | YOLOv8n-class baselines at 3M, par |
| PCB defects (DeepPCB) | ForgeHawk WEM | **84K** | **97.63% mAP** | SGDR, no pretrain | Our 1.5M WEM baseline 97.28% — **18x compression at par** |
| Histopath (PanNuke) | CellHawk v9b | 923K | **0.6050 bPQ** | 10-cycle SGDR, no pretrain | CellViT-SAM-H 0.679 at 699M (**760x fewer params, -7.4 pp**) |
| Thermal drone (AntiUAV-410) | ThermalHawk WEM | 1.13M-1.77M | 82.12-82.95% mAP | SGDR, no pretrain | Beats 60M+ trackers in reported benchmarks |
| ECG arrhythmia (MIT-BIH N/S/V only) | NSV classifier | **8.9K** | 94.1/94.8/94.2% | AAMI subset, inter-patient | Huang et al. on S and V; F and Q classes remain open |

Smallest theory-derived model: **wempyr 39K → 66.6% IoU on NUDT-SIRST**.

## Citation

Until arXiv-ready, cite as:

```
Morgan, J. (2026). HawkStack: A compute-aware topology theory for sub-million-parameter
perception backbones across six domains. Thornveil LLC technical report.
github.com/thornveil-ai/hawkstack-paper
```

When the arXiv ID lands, this README will be updated to cite the preprint.

## Get source access

The HawkStack source (CLI, training pipelines, scaling-law analysis code) and trained checkpoints are available under:

- **Research-use license** (non-commercial, with attribution): `jesse@thornveil.ai`
- **Commercial license** (deployment in commercial perception systems): `licensing@thornveil.ai`
- **Federal procurement** (defense / IC perception backbones): `federal@thornveil.ai`

## License

The research artifacts in this repository (paper, benchmark methodology, results tables) are licensed under [Apache-2.0](LICENSE). The HawkStack implementation source lives at `thornveil-ai/hawkstack` under separate proprietary licensing. Trained weights are released selectively under separate research-use license.

---

A Thornveil system. See [other Thornveil systems](https://github.com/thornveil-ai).
