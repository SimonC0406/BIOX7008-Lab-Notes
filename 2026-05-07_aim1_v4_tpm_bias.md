# 2026-05-07 | Aim 1 v4 Sashimi Pipeline + TPM Bias Finding

**Project:** EAC SpliceAI Driver Variant Analysis  
**Institute:** QIMR Berghofer  
**HPC:** Avalon

---

## Overview

Completed Aim 1 v4 sashimi plot generation across all 30 IGV candidates,
identified TPM bias as a systematic confound, and produced aberration
distribution figures restricted to NM-mapped variants.

---

## Tasks Completed

### 1. Aim 1 v4 Sashimi Pipeline

- Implemented smart windowing: whole-gene for short genes (<50 kb),
  narrow window (±10 kb) for long genes >50 kb
- Generated v4 sashimi plots for 30 IGV candidates + 2 positive
  controls (JAK1, ACAP3)
- JAK1 (DO234313, MAX_DS=1.0) confirmed as validated true positive
  via three-layer IGV inspection (normal DNA, tumour DNA, tumour RNA)

### 2. TPM Bias Scatter

- Generated TPM_vs_MAXDS scatter for the 90 high-confidence candidates
- Key observation: many high-MAX_DS variants have very low TPM,
  suggesting NMD-mediated transcript degradation prevents detection
- Start of the "gene-level TPM inadequate as proxy for region-level
  coverage" finding

### 3. Aberration Distribution Figures

- Restricted to NM-mapped variants (n=1,219; mapping rate 52.4%)
- Mutually exclusive mechanism classification
- Output: `aberration_distribution_NMmapped.png`,
  `aberration_distribution_by_MAXDS_bin.png`

---

## Next Steps

- Apply v5 focused-window protocol to Aim 1 candidates (see May 8)
- Investigate region-level coverage as alternative to gene-level TPM
