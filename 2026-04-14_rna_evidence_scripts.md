# 2026-04-14 | RNA 证据量化脚本开发

**Project:** EAC SpliceAI Driver Variant Analysis  
**Institute:** QIMR Berghofer  
**HPC:** Avalon

---

## Overview

Developed two key pipeline scripts for quantifying RNA-seq evidence.
Generated threshold yield curve visualisations.

---

## Tasks Completed

### 1. `build_variant_input.py`

Wrote script to consolidate variant data from all 208 samples into a unified TSV with BAM paths:

- **Input:**
  - Sample report TSV (`Oesophageal_donorLabels_RNABAM_spliceAI_outs.tsv`)
  - Filtered CSV directory (`spliceAI_parsed_filtered/single_variants/`)
- **Output:** `variants_90.tsv` — unified table with columns:
  `CHROM, POS, REF, ALT, GENE, SAMPLE_ID, DS_AG, DS_AL, DS_DG, DS_DL, MAX_DS, DP_AG, DP_AL, DP_DG, DP_DL, BAM_PATH`
- **Key feature:** Auto-detects sample ID from filename (DO\d+ pattern), tolerates TSV/CSV input

### 2. `quantify_rna_evidence_v2.py`

Wrote upgraded RNA evidence quantification script using pysam:

- **Input:** `variants_90.tsv` (from `build_variant_input.py`)
- **Metrics computed:**
  - **IRR** (Intron Retention Ratio): intron-spanning reads / (intron + spliced reads)
  - **NJR** (Novel Junction Ratio): novel-site reads / total junction reads
- **Evidence classification:** `CONFIRMED` / `PARTIAL` / `UNCONFIRMED` / `LOW_COVERAGE` / `NO_DATA`
- **Key improvement over v1:** Reads BAM path directly from `BAM_PATH` column — no manual directory specification

Output columns added: `ABERRATION_TYPE`, `TUMOR_IRR`, `TUMOR_NJR`, `RNA_EVIDENCE`, `EVIDENCE_SCORE`

### 3. Threshold Yield Curve Iterations

Generated multiple versions of the threshold yield curve to find optimal visual presentation:

| File | Notes |
|------|-------|
| `threshold_yield_curve.png/.pdf` | v1 — linear scale |
| `threshold_yield_curve_v2.png` | v2 — refined axis labels |
| `threshold_yield_curve_v3.png` | v3 — added fill-under-curve |
| `threshold_yield_curve_v4.png` | v4 — colour palette adjustment |
| `threshold_yield_curve_v5.png` | v5 — final publication style |
| `step1_threshold_yield.png` | Step 1 only curve |
| `step1_vs_step2.png` | Overlay: Step 1 vs. two-step (linear) |
| `step1_vs_step2_log.png` | Overlay: Step 1 vs. two-step (log scale) |

---

## Tools

| Tool | Purpose |
|------|---------|
| `pysam` | BAM file reading |
| `pandas`, `numpy` | Data processing |
| `matplotlib` | Visualisation |

---

## Notes

- `quantify_rna_evidence_v2.py` usage:
  ```bash
  python3 build_variant_input.py --report Oesophageal_donorLabels_RNABAM_spliceAI_outs.tsv \
      --filtered-dir spliceAI_parsed_filtered/single_variants/ --output variants_90.tsv
  python3 quantify_rna_evidence_v2.py --variants variants_90.tsv --output rna_evidence.tsv
  ```
- IRR threshold: 0.15 (intron retention confirmed)
- NJR threshold: 0.05 (novel junction confirmed), min 3 novel reads
