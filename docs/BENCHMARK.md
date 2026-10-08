# Benchmark methodology

This document captures the protocol for each per-domain headline number. Reproducing requires the source at `thornveil-ai/hawkstack` (commercial license) plus the published trained checkpoints (research-use license).

## General protocol

Unless a specific row in the headline table notes otherwise:

- **Training**: SGDR cyclic-restart cosine, no ImageNet pretrain, std-persistent optimizer state across cycles
- **Cycle count**: 10 unless noted ("ext" or "25-cycle" rows note longer schedules)
- **Optimizer**: AdamW with weight decay 0.05
- **Hardware**: single GPU (the WEM family is small enough to train on a single 4090)
- **Random seed**: fixed per run; 5-run mean reported (where compute allowed)
- **Data**: official train/val/test splits; no test-set leakage

## Per-domain specifics

### IRST synthetic (NUDT-SIRST)

- 10-cycle mean-std SGDR matched against WSNet_Large protocol
- Headline IoU reported on official test split
- "ext" variant uses 25-cycle min-max SGDR for the 92.29% extended result; we did not reproduce matched-cycle comparison against WSNet at 25 cycles

### IRST real (IRSTD-1K)

- SGDR cycles, no pretrain
- Inter-image evaluation (not per-frame)
- ISNet baseline at 966K serves as the size-equivalent reference

### Sonar (UATD)

- SGDR cycles, no pretrain
- mAP at IoU=0.5
- YOLOv8n-class baselines at 3M parameters as reference

### PCB defects (DeepPCB)

- SGDR cycles, no pretrain
- mAP across the 6 defect classes
- Headline: 84K params reaches 97.63% mAP vs 1.5M WEM baseline at 97.28% — the **18x compression at par** result

### Histopathology (PanNuke)

- 10-cycle SGDR
- bPQ (balanced Panoptic Quality) on PanNuke's three folds
- TTA + post-proc lifts from 0.6050 (single-model) to 0.6645 (8-way TTA + watershed)
- CellViT-SAM-H at 699M parameters is the size-overwhelmed reference: 760x fewer params for -7.4 pp bPQ

### Thermal drone (AntiUAV-410)

- WEM-Inverted topology (canonical going forward; DCNv3 lineage demoted)
- 82.12% mAP at 1.13M params (WEM-Inverted), 82.95% at 1.77M (DCNv3 lineage)
- Benchmark protocol matches CVPR 2025 Best Paper companion publication

### ECG arrhythmia (MIT-BIH)

- Partial domain; not counted in the six-domain headline
- 3-class only: N (normal), S (supraventricular), V (ventricular)
- AAMI subset, inter-patient split
- F (fusion) and Q (unknown) classes explicitly excluded — theory does not yet cover these well

## Reproducing

The trained checkpoints are available under research-use license. Contact `jesse@thornveil.ai` to request access; you receive:

- The 15 zoo checkpoints with metadata (recipe + git SHA + final metrics)
- Inference-only Python harness
- Per-domain dataset preparation instructions

Training-from-scratch requires the proprietary source at `thornveil-ai/hawkstack` under commercial license.

## See also

- [README](../README.md) — six-domain results summary table
- [PAPER.md](PAPER.md) — paper outline and abstract
