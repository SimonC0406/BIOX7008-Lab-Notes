# 2026-04-24 | 90 候选变异最终表格 & TPM 归一化分析

**Project:** EAC SpliceAI Driver Variant Analysis  
**Institute:** QIMR Berghofer  
**HPC:** Avalon

---

## Overview

Finalised the 90-candidate supplementary table.
Re-ran all expression analyses with TPM-normalised values for publication-quality figures.
Updated MobaXterm to v26.1 for improved HPC connection stability.

---

## Tasks Completed

### 1. Supplementary Table S1 — 90 Candidates

Generated final `Supplementary_Table_S1_90_candidates.tsv` (90 rows + header):

**Schema:**
```
SAMPLE_ID  CHROM  POS  REF  ALT  GENE_NM  MAX_DS
DS_AG  DS_AL  DS_DG  DS_DL  Any_splicing_aberration
Exon_skipping  Intron_retention  Partial_exon_deletion
Partial_intron_retention  Pseudoexon_activation
```

**Summary statistics:**

| Metric | Value |
|--------|-------|
| Total candidates | 90 |
| Unique samples | ~55 (est.) |
| MAX_DS range | 0.05 – 1.00 |
| MAX_DS = 1.0 (top confidence) | n=2 |
| Any_splicing_aberration = YES | 90 / 90 |

**Mechanism breakdown (approximate):**
- Exon skipping: most common
- Intron retention: ~20–25%
- Partial exon deletion: ~15%
- Pseudoexon activation: ~10%
- Partial intron retention: ~5%

Generated `aberration_types_90.png` — mechanism distribution barplot for the 90 candidates.

### 2. TPM-Normalised Expression Analyses

Re-generated all expression figures using TPM (transcripts per million) instead of raw expected counts:

| File | Description |
|------|-------------|
| `expr_by_maxds_bins_TPM.png` | Expression (TPM) by MAX_DS bin |
| `expr_yes_vs_no_TPM.png` | Expression (TPM): YES vs. NO splicing |
| `ppv_curve_TPM.png` | PPV curve with TPM-filtered dataset |
| `ppv_curve_TPM_v2.png` | PPV curve v2 (refined axis range) |

**Key finding:** TPM-normalised analysis confirms the trend from raw counts — genes with MAX_DS > 0.8 variants show measurably reduced median expression, consistent with NMD-mediated decay after aberrant splicing.

### 3. MobaXterm Update

Updated MobaXterm from previous version to v26.1:
- Improved session persistence
- Better X11 forwarding stability (important for IGV remote display)
- Located: `C:\Users\cheny\Documents\MobaXterm_Portable_v26.1\`

---

## Tools

| Tool | Purpose |
|------|---------|
| Python / pandas | Supplementary table generation |
| matplotlib / seaborn | TPM expression plots |
| MobaXterm v26.1 | HPC SSH + X11 |

---

## Output Files

| File | Description |
|------|-------------|
| `Supplementary_Table_S1_90_candidates.tsv` | **Final 90-candidate list** |
| `aberration_types_90.png` | Mechanism distribution figure |
| `expr_by_maxds_bins_TPM.png` | Expression by MAX_DS (TPM) |
| `expr_yes_vs_no_TPM.png` | Expression YES vs. NO (TPM) |
| `ppv_curve_TPM.png` | PPV curve (TPM) |
| `ppv_curve_TPM_v2.png` | PPV curve v2 (TPM) |

---

## Notes

- Supplementary Table S1 is ready for thesis appendix
- TPM figures will replace raw-count figures in thesis Results chapter
- Next step: generate conclusion slides and presentation for Aim 1 summary
