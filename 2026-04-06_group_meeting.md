# 2026-04-06 | 组会进度汇报

**Project:** EAC SpliceAI Driver Variant Analysis  
**Institute:** QIMR Berghofer  
**HPC:** Avalon

---

## Overview

Delivered first formal progress presentation to group meeting.
Presented SpliceAI filtering results for the 208-sample EAC cohort.

---

## Presentation Delivered

**Title:** *Identifying Somatic Intronic Driver Variants in Esophageal Adenocarcinoma Using SpliceAI*

Key results presented:
- 208 paired WGS samples processed through SpliceAI pipeline
- Two-pass filter (MAX_DS > 0.5 + Any_splicing_aberration = YES): 21 variants
- 11 Frankell 76 driver genes hit; 20/208 samples (9.6%)
- Priority hits: TP53, JAK1, RNF43, CDKN2A (biallelic candidate)

---

## Feedback Received

| Feedback | Action |
|----------|--------|
| Add RNA-seq BAM evidence for top hits | IGV screenshots + pysam pileup |
| Show sensitivity analysis (threshold vs. yield) | `plot_threshold_analysis.py` to write |
| Consider lowering threshold to 0.1+ with RNA-seq filter | Two-step approach: Step1 + Step2 intersection |
| CDKN2A biallelic candidate: check VAF for phasing | Future task |

---

## Tools

| Tool | Purpose |
|------|---------|
| PPTX / PDF | Presentation delivery |
| Frankell 2019 (MOESM3) | Driver gene framework |

---

## Notes

- Two-step pipeline concept introduced: Step 1 (Any_splicing_aberration = YES) + Step 2 (RNA-seq expression-confirmed pileup intersection)
- This approach would yield ~90 candidates (far more than the 21 from hard MAX_DS > 0.5 filter alone)
- Will begin IGV validation of JAK1 first
