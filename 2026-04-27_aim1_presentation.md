# 2026-04-27 | Aim 1 结论幻灯片 & 最终汇报

**Project:** EAC SpliceAI Driver Variant Analysis  
**Institute:** QIMR Berghofer  
**HPC:** Avalon

---

## Overview

Finalised Aim 1 presentation materials.
Prepared conclusion slides summarising the full SpliceAI pipeline validation.

---

## Tasks Completed

### 1. Final Presentation — Pipeline Validation

Compiled full Aim 1 summary presentation:

- **`Advancing-SpliceAI-Pipeline-Validation.pptx`** — Main presentation (complete)
- **`Advancing-SpliceAI-Pipeline-Validation.pdf`** — PDF export

Presentation structure:
1. Background: intronic SIDs in EAC, 208 WGS samples
2. Two-step pipeline: Step 1 (SpliceAI) → Step 2 (RNA-seq expression confirmation)
3. Results: 90 candidates, mechanism breakdown
4. Validation: JAK1 IGV + Sashimi, MAP3K1 IGV
5. PPV analysis: Figure 4.2 (threshold vs. predictive accuracy)
6. Expression analysis: TPM-normalised results
7. Conclusion and Aim 2 roadmap

### 2. Individual Slide Decks

Generated modular slide files for mix-and-match use:

| File | Content |
|------|---------|
| `Aim1_Conclusion_Slide.pptx` | Aim 1 summary conclusions |
| `Discussion_Slide.pptx` | Discussion points, limitations, future work |
| `Two_Aims_Slide.pptx` | Project overview: Aim 1 + Aim 2 framing |

---

## Aim 1 Final Summary

| Metric | Value |
|--------|-------|
| WGS samples processed | 208 paired tumour-normal |
| Step 1 variants (Any_splicing_aberration = YES) | 2,326 |
| Step 2 (RNA-seq confirmed) | ~1,001 |
| Final 90-candidate list | 90 variants |
| Frankell driver genes hit | 11 (top: TP53, JAK1, RNF43, CDKN2A) |
| Affected samples | 20 / 208 (9.6%) |
| PPV at MAX_DS ≥ 0.5 | ~65% |
| PPV at MAX_DS ≥ 0.9 | ~95% |

---

## Tools

| Tool | Purpose |
|------|---------|
| PowerPoint | Presentation compilation |
| All analysis scripts | Source of all figures |

---

## Next Steps (Aim 2)

- [ ] SAI-10k-calc: ΔL mod 3 NMD prediction for the 90 candidates
- [ ] Pangolin orthogonal scoring for top Frankell driver hits
- [ ] CDKN2A biallelic candidate: VAF analysis for allelic phasing
- [ ] Thesis Results section writing: "SpliceAI pipeline validation"
- [ ] Methods section finalisation
