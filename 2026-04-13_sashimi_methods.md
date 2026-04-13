# 2026-04-13 | Sashimi 图 & 论文方法章节

**Project:** EAC SpliceAI Driver Variant Analysis  
**Institute:** QIMR Berghofer  
**HPC:** Avalon

---

## Overview

Generated Sashimi plot for JAK1 validation.
Drafted thesis Methods section and Table 1.

---

## Tasks Completed

### 1. Sashimi Plot — JAK1 (DO234313)

Generated RNA-seq junction read Sashimi plot for JAK1 intron retention:

- **Tool:** IGV Sashimi view (BAM → Sashimi mode)
- **Locus:** chr1:64,864,786 ± 5 kb
- **Output:** `Sashimi.png`
- **Interpretation:** Junction arcs show depletion of canonical donor site usage; intron-spanning reads accumulate at predicted retention window

This figure is candidate Figure 4.3 in the thesis Results section.

### 2. Thesis Methods Section Draft

Drafted `thesis_methods.docx` covering:
- Section 3.1: WGS dataset — 208 EAC paired tumour-normal samples (ICGC ESAD-UK cohort)
- Section 3.2: SpliceAI pipeline setup — parsed VCF format, key output columns
- Section 3.3: Two-step filtering strategy:
  1. Step 1: `Any_splicing_aberration = YES`
  2. Step 2: RNA-seq pileup intersection (`spliceAI_parsed_filtered/single_variants/`)
- Section 3.4: Driver gene matching — Frankell 2019 76-gene framework, RefSeq transcript ID mapping

### 3. Thesis Table 1 Draft

Generated `Table 1.pdf` — summary statistics table:

| Metric | Value |
|--------|-------|
| WGS samples (tumour-normal pairs) | 208 |
| Step 1 variants (Any_splicing_aberration=YES) | 2,326 |
| Step 2 (RNA-seq confirmed) | ~1,001 |
| Two-step intersected | 90 (full cohort, all thresholds combined) |
| Frankell driver genes hit | 11 |
| Affected samples | 20 / 208 (9.6%) |

### 4. CIA Grant Proposal Contribution

Contributed a paragraph to the CIA Grant Proposal (`CIA Grant Proposal Template Updated (3).docx`) on the SpliceAI pipeline validation strategy as a methodological innovation.

---

## Tools

| Tool | Purpose |
|------|---------|
| IGV 2.18.2 (Sashimi mode) | Junction-arc visualisation |
| Word | Methods + Table 1 draft |

---

## Output Files

| File | Description |
|------|-------------|
| `Sashimi.png` | JAK1 Sashimi plot (candidate Fig. 4.3) |
| `thesis_methods.docx` | Methods chapter draft |
| `Table 1.pdf` | Summary statistics table |
