# The HawkStack topology paper

The complete paper (LaTeX source + figures + scaling-law analysis) is preparing for arXiv submission. Until the preprint lands, this document holds the structured summary.

## Current status

- Draft v10 complete (see private `thornveil-ai/hawkstack/paper/topology_paper.pdf`)
- Companion-publication crossref with `thornveil-ai/thermalhawk` legacy DCNv3 lineage (peer-reviewed at CVPR 2025 Best Paper level, Anti-UAV-410)
- Six-domain validation complete
- 16-run power-law scaling fit complete (R² = 0.9895 on NUDT-SIRST)
- arXiv submission: queued post v10 review pass

## Abstract (paraphrased)

Sub-million-parameter perception models can match SOTA in their weight class across six unrelated domains (sub-pixel IRST, real-world IRST, sonar object detection, PCB defects, histopathology, thermal drone detection) when their topology is selected by three descriptive parameters: pathway count, coupling tightness, and feature-quality match (receptive-field sweep tuned to target size distribution).

The paper introduces the WEM (Wide-Equivariant Multi-pathway) backbone family and demonstrates that a single training recipe — cyclic-restart cosine SGDR with std-persistent optimizer state — produces the per-domain results table without per-domain hyperparameter tuning, given the topology is selected correctly.

A power-law scaling fit on NUDT-SIRST across 16 model sizes (R² = 0.9895) quantifies the family's compute-vs-quality frontier and establishes that the headline results are not local maxima.

## Sections (preprint outline)

1. **Introduction** — why sub-million-parameter perception matters; the deployment constraint at the edge
2. **Related work** — WSNet, ISNet, EfficientNet-Lite, MobileNet-V3, ConvNext-Tiny (size-equivalent baselines)
3. **Topology theory** — the three descriptive parameters, their derivation, the WEM family
4. **Training recipe** — SGDR cycles, fresh vs std persistence, the +3.42 pp std-over-fresh finding
5. **Per-domain case studies** — six domains, methodology, results, ablations
6. **Scaling-law fit** — 16-run NUDT-SIRST sweep, the power-law, R²
7. **Limitations** — what the theory doesn't yet explain; ECG F and Q classes open
8. **Conclusion** — the compute-vs-quality frontier for small perception models

## Release plan

- arXiv submission: post final-review on v10
- ICCV / CVPR submission: target 2026
- Companion blog post: at arXiv submission

## See also

- [README](../README.md) — six-domain results table
- [BENCHMARK.md](BENCHMARK.md) — benchmark methodology
- [CITATION.md](CITATION.md) — preferred citation format
