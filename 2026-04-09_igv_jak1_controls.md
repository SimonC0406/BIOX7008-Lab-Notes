# 2026-04-09 | IGV 对照比较 — JAK1 / 文献综述修订

**Project:** EAC SpliceAI Driver Variant Analysis  
**Institute:** QIMR Berghofer  
**HPC:** Avalon

---

## Overview

Extended JAK1 IGV validation with tumour-vs-control comparison.
Also submitted revised literature review (v5).

---

## Tasks Completed

### 1. JAK1 Tumour vs. Control IGV Comparison

Loaded multiple control BAM files alongside DO234313 tumour BAM:

- **Tumour (DO234313):** Elevated intron-spanning reads at chr1:64,864,786
- **Controls (normal WGS-matched):** Canonical junction reads, no intron retention signal
- **Screenshot:** `JAK1_IGV_intron_retention_comparison_controls_vs_DO234313.png`

| Sample | Intron-spanning reads | Spliced reads | Intron Retention Ratio |
|--------|-----------------------|---------------|----------------------|
| DO234313 (tumour) | Elevated | Reduced | ~0.3+ |
| Controls (n=3) | Minimal | Dominant | < 0.05 |

Conclusion: **Somatic intron retention confirmed** — absent in matched controls.

### 2. Literature Review Revision (v5)

Updated `YanChen_lit_review_REVISED_v5.docx`:
- Added paragraph on JAK1 splicing in cancer context
- Revised section on SpliceAI predictive accuracy across variant classes
- Refined introduction framing (intronic variants underrepresented in EAC driver landscape)

### 3. Presentation Update

Updated PPTX with JAK1 IGV figures.

---

## Tools

| Tool | Purpose |
|------|---------|
| IGV 2.18.2 | Tumour-vs-control comparison |
| `qsub -X -I` | Interactive HPC session |
| Word | Literature review |

---

## Output Files

| File | Description |
|------|-------------|
| `JAK1_IGV_intron_retention_comparison_controls_vs_DO234313.png` | Control comparison figure |
| `YanChen_lit_review_REVISED_v5.docx` | Lit review v5 |

---

## Notes

- Tumour:control ratio strongly supports somatic origin of intron retention
- No equivalent signal in controls confirms this is tumour-specific splicing disruption
