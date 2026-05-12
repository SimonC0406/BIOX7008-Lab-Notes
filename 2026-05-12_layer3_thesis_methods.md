# 2026-05-12 | Layer 3 Evidence Framework + Thesis Methods Draft

**Project:** EAC SpliceAI Driver Variant Analysis  
**Institute:** QIMR Berghofer  
**HPC:** Avalon

---

## Overview

Designed a Layer 3 mechanism-specific quantitative evidence framework
to complement sashimi visual review, and drafted the thesis Methods
chapter (~2000 words).

---

## Tasks Completed

### 1. Layer 3: Mechanism-Specific Quantitative Evidence

Motivation: sashimi-based visual review may hide partial splicing
aberrations (e.g., 30% aberrant reads get visually swamped by
70% canonical). Per-read evidence from BAM files captures what
sashimi aggregation misses.

Framework:
- **ExonSkip:** count split reads with N-segment fully spanning
  predicted skipped exon
- **PartialExonDel:** count novel junction reads within ±200 bp of
  variant (cryptic junctions)
- **IntronRet:** intron/exon reads-per-kb ratio normalised by
  flanking exon coverage

Programmatic verdicts via threshold heuristics (e.g., tumour ≥3
skip reads + max(controls) = 0 → Confirmed).

Pending Dean's review on:
- Threshold validity
- Institutional standard thresholds (if exist)
- Whether to run now or wait for Nic's Aim 1 review first

Script: `layer3_evidence.py` (not yet executed pending Dean approval).

### 2. Thesis Methods Chapter Draft (~2000 words)

Sections:
- 4.1 Data sources and sample cohort
- 4.2 Pipeline overview
- 4.3 Aim 1: SpliceAI prediction quality assessment
- 4.4 Aim 2: Driver gene-focused intronic SID validation
- 4.5 Statistical analysis (Cohen's kappa framework, PPV)

Includes explicit reflexivity on:
- Confirmation bias documented across v1→v4→v5
- Y-axis compression artifact discovery and resolution
- Exclusion criteria justification (single-exon gene; insufficient
  expression)

---

## Next Steps

- Await Dean's response on Layer 3 thresholds
- Await Nic's verdicts on Aim 1 plots
- Begin thesis Results drafts (Aim 1 + Aim 2)
