# 2026-04-10 | 阈值敏感性分析 & MAP3K1 IGV

**Project:** EAC SpliceAI Driver Variant Analysis  
**Institute:** QIMR Berghofer  
**HPC:** Avalon

---

## Overview

Wrote and ran `plot_threshold_analysis.py` — threshold sensitivity analysis for the two-step filter.
Also validated MAP3K1 variant in DO50362 by IGV.

---

## Tasks Completed

### 1. Threshold Sensitivity Analysis (`plot_threshold_analysis.py`)

Computed variant yield and Frankell driver gene hit count across MAX_DS thresholds (0.0 → 1.0, step 0.05):

- **Step 1** (Any_splicing_aberration = YES): 2,326 total variants
- **Two-step** (Step 1 ∩ RNA-seq pileup confirmed): 1,001 variants before MAX_DS filter

Generated 3 plots:

| Plot | File | Key Finding |
|------|------|-------------|
| Threshold vs. variant count | `threshold_variant_count.png` | Sharp yield drop above MAX_DS=0.5; two-step reduces count by ~57% at all thresholds |
| Threshold vs. driver gene hits | `threshold_driver_hits.png` | Driver hits plateau above MAX_DS~0.3 — no new genes gained above 0.5 |
| MAX_DS distribution (two-step) | `maxds_distribution_twostep.png` | Bimodal: driver hits cluster at high MAX_DS (>0.8) |

Key takeaway: **Threshold of 0.0 with two-step filter is sufficient** — RNA-seq expression confirmation is the primary discriminator, not a hard MAX_DS cutoff.

### 2. MAP3K1 IGV Validation (DO50362)

- **Variant:** MAP3K1, chr5 (specific position TBC from output files)
- **Predicted mechanism:** Donor loss / partial exon deletion
- **Screenshot:** `MAP3K1_DO50362.png`
- Result: Partial exon deletion signal visible in tumour BAM

---

## Tools

| Tool | Purpose |
|------|---------|
| `plot_threshold_analysis.py` | Threshold sensitivity curve generation |
| `matplotlib`, `pandas`, `numpy` | Plotting |
| HPC `/working/genomeinfo/...` | Data source |
| IGV 2.18.2 | MAP3K1 validation |

---

## Output Files

| File | Description |
|------|-------------|
| `threshold_variant_count.png` | Threshold vs. variant yield (Step 1 vs. two-step) |
| `threshold_driver_hits.png` | Threshold vs. Frankell driver hits |
| `maxds_distribution_twostep.png` | MAX_DS distribution for two-step filtered variants |
| `MAP3K1_DO50362.png` | IGV screenshot |

---

## Notes

- `STEP1_FILE`: `all_step1_variants.tsv` (on Avalon: `/mnt/backedup/home/yanC/driver_gene_hits/`)
- `STEP2_FILE`: pileup-confirmed single_variants CSVs from `spliceAI_parsed_filtered/`
- Frankell hits plateau confirms that lowering the threshold doesn't lose driver hits when two-step filter is applied
