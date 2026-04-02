# 2026-04-02 | 结果复盘 & 下阶段规划

**Project:** Somatic Intronic Driver Variants (SIDs) in Esophageal Adenocarcinoma (EAC)  
**Institute:** QIMR Berghofer Medical Research Institute  
**Supervisor:** Dean  
**HPC:** Avalon (`yanC@hpcnode074`)

---

## Overview

First working day after completing the March 31 driver gene matching pipeline.
Met with Dean to review results and plan next steps for validation.

---

## Supervisor Meeting Summary

Reviewed the March 31 analysis:

| Metric | Value |
|--------|-------|
| Total filtered intronic variants | 21 |
| Driver genes hit (Frankell 76) | 11 |
| Affected samples | 20 / 208 (9.6%) |

Dean's feedback:
- Priority for validation: **TP53** (7 variants, 7 samples), **JAK1** (3 variants), **CDKN2A** (2 variants, 1 sample)
- Need RNA-seq read evidence to confirm predicted splicing events
- IGV screenshots required for top candidates before thesis writing
- Consider relaxing MAX_DS threshold (currently 0.5) and using RNA-seq confirmation as the primary filter

---

## Next Steps Agreed

1. IGV validation: start with JAK1 (intron retention predicted, chr1)
2. RNA-seq pileup confirmation: two-step filter strategy
3. Threshold sensitivity analysis: plot variant yield vs. MAX_DS across full range
4. Begin thesis Methods section draft

---

## Tools

| Tool | Purpose |
|------|---------|
| Frankell 2019 Suppl. Table (MOESM3) | Driver gene reference cross-check |
| IGV 2.18.2 (Avalon) | Visual validation |
| `match_drivers_by_refseq.py` | Current driver matching script |

---

## Notes

- Frankell 2019 supplementary Excel (`41588_2018_331_MOESM3_ESM.xlsx`) downloaded for re-review
- CDKN2A biallelic candidate flagged for priority validation (two intronic variants in same sample)
