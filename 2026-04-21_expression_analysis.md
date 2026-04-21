# 2026-04-21 | RNA 表达量分析

**Project:** EAC SpliceAI Driver Variant Analysis  
**Institute:** QIMR Berghofer  
**HPC:** Avalon

---

## Overview

Analysed RNA expression levels stratified by MAX_DS score bins.
Goal: validate that high MAX_DS variants are associated with reduced gene expression (consistent with functional splicing disruption).

---

## Tasks Completed

### 1. Expression vs. MAX_DS Bin Analysis

Stratified the 90-candidate variants into MAX_DS bins and compared RNA expression levels:

- **Bins:** [0–0.2), [0.2–0.4), [0.4–0.6), [0.6–0.8), [0.8–1.0]
- **Expression metric:** Raw expected count from tumour RNA-seq

Generated:
- `expr_by_maxds_bins.png` — boxplot of expression by MAX_DS bin
- `expr_by_maxds_bins_v2.png` — refined version with overlaid points

**Trend:** Variants in higher MAX_DS bins show modestly lower median expression, consistent with splicing-induced downregulation — but high variance within bins.

### 2. Expression: YES vs. NO (Splicing Aberration)

Compared expression for `Any_splicing_aberration = YES` vs. `NO`:

- **`expr_yes_vs_no.png`** — violin/boxplot comparison
- **Conclusion:** YES group shows wider expression variance; no dramatic global difference, but subset with very low expression enriched in YES group

---

## Interpretation

| Finding | Implication |
|---------|-------------|
| High MAX_DS → slightly lower expression | Consistent with NMD after aberrant splicing |
| Large variance within bins | Multiple mechanisms; not all variants lead to mRNA degradation |
| YES vs. NO: partial separation | `Any_splicing_aberration = YES` enriches for low-expression events |

---

## Tools

| Tool | Purpose |
|------|---------|
| `pandas`, `matplotlib`, `seaborn` | Data analysis & plotting |
| RNA-seq expression matrix | From Avalon project directory |

---

## Output Files

| File | Description |
|------|-------------|
| `expr_by_maxds_bins.png` | Expression by MAX_DS bin (v1) |
| `expr_by_maxds_bins_v2.png` | Expression by MAX_DS bin (v2, refined) |
| `expr_yes_vs_no.png` | Expression YES vs. NO (raw counts) |

---

## Notes

- Raw expected counts used — TPM normalisation to be applied Friday for thesis-quality figures
- Will use TPM-normalised values for the final supplementary analysis
