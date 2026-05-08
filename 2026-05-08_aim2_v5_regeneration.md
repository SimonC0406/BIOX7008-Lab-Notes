# 2026-05-08 | Aim 2 Driver Gene Scoping + v5 Sashimi Protocol

**Project:** EAC SpliceAI Driver Variant Analysis  
**Institute:** QIMR Berghofer  
**HPC:** Avalon

---

## Overview

Completed Aim 2 driver gene census, identified confirmation bias in v4
review, designed v5 focused-window protocol with blinded review, and
sent annotated Aim 1 plots to Nic for independent verdict.

---

## Tasks Completed

### 1. Aim 2 Driver Gene Scoping (Frankell 2019)

- Census across 208-sample EAC cohort against 76-gene driver panel
- 45/76 driver genes have at least one variant (692 total variants)
- 28 intronic, 664 exonic
- 21 high-confidence intronic candidates (MAX_DS ≥ 0.5 +
  Any_aberration = YES) from 13 unique driver genes
- TP53 dominates: 6 of 21 candidates (29%)
- Top 14 selected for sashimi validation

### 2. v5 Focused Regeneration Protocol (Aim 2)

Rationale: confirmation bias identified in v4 — verdicts varied
6→9→5 Confirmed across review rounds for the same 14 plots.

v5 features:
- Focused window: variant ± 2–3 kb instead of whole-gene
- Variant marker: red dashed line at variant position
- Mechanism-specific aberration shading (yellow/red/blue/purple)
- Exon numbering on gene track (E1, E2, ...)
- Blinded review panel: MAX_DS hidden, verdict checkboxes

Bug fixes during v5:
- Removed `--fix-y-scale`: was compressing tumour signal when
  controls had higher baseline (COL1A1 case ratio 0.047)
- Removed `--overlay`: was merging two control tracks visually
- Fixed CDKN2A grep: was matching lncRNA CDKN2A-DT (822 bp)
  instead of true CDKN2A (27 kb); switched to quoted gene_name grep

Excluded from sashimi validation:
- Case 8 KCNQ3: controls have max 6 reads (no baseline)
- Case 10 TRPA1: tumour has max 6 reads (no expression)

### 3. v5 Focused Regeneration (Aim 1)

- Same v5 protocol applied to all 30 Aim 1 candidates
- 29 evaluable (Case 16 ITPRIPL2 excluded: single-exon gene,
  intron retention biologically impossible)
- SPIDR (Case 6) window expanded to ±6 kb: variant in terminal
  exon 20 (1000 bp); default ±3 kb window had no intron annotation
- Annotated PNGs with Simon's verdicts pre-filled for Nic's review

### 4. Email to Nic

Sent annotated Aim 1 plots, lit review v7, and BIOX7008 project plan.

Provisional verdicts: 1 Confirmed (Case 24 EPCAM, MAX_DS=0.88),
2 Inconclusive (Cases 9 INSR, 19 ALYREF), 26 Unsupported.

Flagged methodological points:
- `--fix-y-scale` artifact (COL1A1 example)
- 5 cases with incomplete SpliceAI annotation (mechanism
  "unclassified" or ExonSkip without target exon)

---

## Next Steps

- Await Nic's independent verdicts on Aim 1 plots
- Begin Layer 3 quantitative evidence framework design
