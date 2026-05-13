# 2026-05-13 | Thesis Results + Discussion Drafts

**Project:** EAC SpliceAI Driver Variant Analysis  
**Institute:** QIMR Berghofer  
**HPC:** Avalon

---

## Overview

Drafted thesis Results sections for both aims and the Discussion
chapter (~8750 words total today), produced Aim 2 figures, and
sent Layer 3 thinking-aloud message to Dean on Slack.

---

## Tasks Completed

### 1. Aim 2 Results Draft (~1500 words)

- 5.2.1 Rationale and analytical framing
- 5.2.2 Driver gene variant census (692 variants, 45/76 genes)
- 5.2.3 High-confidence candidate selection (21 from 13 genes)
- 5.2.4 Sashimi validation pipeline (v5 protocol)
- 5.2.5 Exclusions on biological/technical grounds (KCNQ3, TRPA1)
- 5.2.6 Validation outcomes (TBD verdicts)
- 5.2.7 Comparison with Aim 1 (TBD)
- 5.2.8 Control sample sensitivity (Aim 1 Case 30 = Aim 2 Case 14,
  different controls)
- 5.2.9 Summary

### 2. Aim 1 Results Draft (~3750 words)

- 5.1.1 Overview
- 5.1.2 Pipeline attrition (52,006 → 2,326 → 1,001; NM mapping
  yields 1,219)
- 5.1.3 Mechanistic distribution:
  - Exon skipping 38.3%
  - Increased inclusion 19.8%
  - PartialExonDel 18.0%
  - Multi-type 13.2%
  - IntronRet 5.1%
  - PartialIntronRet 3.0%
  - Pseudoexon 2.6%
- 5.1.4 TPM stratification (TPM>0: 80.2%, TPM=0: 19.8%)
- 5.1.5 MAX_DS bins with mechanism × bin interactions:
  - Key finding: IncreasedInclusion exclusively low-confidence
    (99.2% in low bin)
  - Pseudoexon entirely absent from high bin
  - Multi-type concentrated in high bin (83.2%)
- 5.1.6 Stratified candidate selection
- 5.1.7 Sashimi validation outcomes (TBD final verdicts)
- 5.1.8 Systematic FP: single-exon gene context (ITPRIPL2)
- 5.1.9 Methodology findings (confirmation bias + y-axis artifact)
- 5.1.10 Summary

### 3. Discussion Chapter Draft (~3500 words)

- 6.1 Synthesis of findings
- 6.2 Methodological insights for SpliceAI-based SID discovery:
  - 6.2.1 Gene-level TPM vs region-level coverage
  - 6.2.2 SpliceAI systematic FP modes (single-exon, hotspot)
  - 6.2.3 Visualisation methodology (confirmation bias, y-axis
    compression)
  - 6.2.4 Control sample selection sensitivity
- 6.3 Limitations (cohort size, two-control design, RNA-seq
  feasibility, visual subjectivity, single-cohort scope)
- 6.4 Future directions (region-level metrics, biology-aware
  pre-filter, Layer 3 calibration, larger validated control set,
  cross-cohort reproducibility, long-read complement)
- 6.5 Conclusion

### 4. Aim 2 Figures

- Figure 5.2.A: Top 20 driver genes by variant count (stacked:
  intronic vs exonic, TP53 highlighted)
- Figure 5.2.B: 13 driver genes with HC intronic candidates
  (TP53 highlighted)
- Figure 5.2.C: Mechanism distribution of 21 HC intronic candidates

### 5. Slack: Layer 3 Query to Dean

Sent thinking-aloud message: "Sashimi might hide partial splicing
aberrations. Wondering if it's worth adding pysam quantitative
layer. Any institutional thresholds?"

Awaiting reply.

---

## Total Thesis Text Drafted to Date

~10,750 words across Methods, Results (both aims), and Discussion.
At ~350 words/page with figures excluded (per UQ 30-page limit),
this is approximately 31 pages of pure text — needs ~5–10% trimming
for final fit.

---

## Next Steps

- [ ] Wait for Nic's response on Aim 1 IGV plots and verdicts
- [ ] Wait for Dean's response on Layer 3 framework
- [ ] After verdicts finalised: compute Cohen's kappa, update PPV
      in Results, fill TBD sections in Discussion
- [ ] Word document assembly: integrate all chapter drafts into
      thesis template matching lit review v7 format
- [ ] Reference list: Frankell 2019, Garrido-Martín 2018 (ggsashimi),
      Landis & Koch 1977 (kappa), Jaganathan 2019 (SpliceAI),
      Avsec 2026 (AlphaGenome)
