# Progress Report — 2026-04-28

## Summary
Completed full migration of the SpliceAI truthset from expected counts to TPM following Dean's/Nic's recommendation. Successfully completed JAK1 IGV validation across all four established criteria, confirming it as the first RNA-validated somatic intronic driver candidate in the cohort. Aim 1 Results chapter rewritten with TPM data; Aim 2 chapter upgraded to "Confirmed" status for JAK1. Three new presentation slides created for tomorrow's meeting with Nic, covering Two Aims framework, Aim 1 conclusions, and Discussion & Future Directions.

---

## Aim 1: SpliceAI Prediction Quality (TPM Truthset)

### Truthset migration
- Switched truthset from RSEM expected counts to TPM per supervisor preference (TPM accounts for transcript length and library depth normalization)
- File: `/working/genomeinfo/share/analysis/Yan_Chen_Masters_Project/study_reports/ICGC_-_Oeosphageal.genes.TMP.csv.genes.TPM.RefSeq.csv`
- Contains 213 samples × 62,754 genes with 20,065 genes (32.0%) successfully mapped to RefSeq NM accessions
- Replaces ExpectedCounts as the standard truthset for all subsequent analyses

### PPV results (TPM-based)
| MAX_DS threshold | Step 1 variants | TPM > 0 | PPV (%) |
|---|---|---|---|
| ≥ 0.1 | 1,084 | 873 | 80.5 |
| ≥ 0.2 | 985 | 801 | 81.3 |
| ≥ 0.3 | 713 | 588 | 82.5 |
| ≥ 0.4 | 602 | 500 | 83.1 |
| ≥ 0.5 | 521 | 431 | 82.7 |
| ≥ 0.6 | 453 | 376 | 83.0 |
| ≥ 0.7 | 395 | 330 | 83.5 |
| ≥ 0.8 | 333 | 280 | 84.1 |
| ≥ 0.9 | 259 | 218 | 84.2 |
| = 1.0 | 61 | 52 | 85.2 |

**Key conclusion:** PPV remains 80–85% across all thresholds (significantly higher than the 43–46% counts-based estimate). MAX_DS threshold tuning provides ~5 percentage point marginal gain; RNA-seq expression filtering is the dominant specificity mechanism.

### Figures generated (TPM versions)
- `~/ppv_curve_TPM.png` — PPV curve across MAX_DS thresholds (Figure 4.2)
- `~/expr_yes_vs_no_TPM.png` — Gene expression YES vs NO comparison, Mann-Whitney U p = 1.14 × 10⁻⁶ (Figure 4.4)
- `~/expr_by_maxds_bins_TPM.png` — Expression stratified by MAX_DS bin (Figure 4.3)
- `~/maxds_distribution_step1.png` — MAX_DS distribution histogram (Figure 4.1)

---

## Aim 2: JAK1 IGV Validation — Confirmed

### Four-criteria validation framework (formalized)
1. **DNA somatic origin**: tumour ALT VAF ≥ 10%, normal ALT ≈ 0
2. **RNA-level aberration**: predicted splicing pattern observable in tumour RNA-seq
3. **Control comparison**: aberration absent in ≥ 3 unrelated control samples
4. **Signal strength**: aberration signal ≥ 5 reads above local baseline

### JAK1 c.64864786C>G — all four criteria satisfied

**Criterion 1 (DNA): ✅**
- Tumour DNA: ~50% G allele, 63× coverage (heterozygous somatic)
- Normal blood DNA: 0/38 G reads (germline ref)

**Criterion 2 (RNA aberration): ✅**
- At variant position chr1:64,864,786, RNA shows 15/15 reads carrying the alternative G allele
- Position lies within the predicted 1,276 bp retained intron — reads at this position directly evidence intron retention

**Criterion 3 (Control comparison): ✅**
- Three unrelated EAC samples (DO234149, DO234151, additional control) show:
  - No RNA reads at chr1:64,864,786 (canonical splicing removes the intronic sequence)
  - Clean intron with no continuous coverage between exons 24 and 25

**Criterion 4 (Signal strength): ✅**
- DO234313 RNA shows continuous coverage across the predicted retained intron (5–15 reads/position)
- Significantly above background; controls are entirely empty in the same region

### IGV figures
- `JAK1_Figure_4.6a_variant_position_zoom.png` — 14 bp zoom showing 5-track allele comparison
- `JAK1_Figure_4.6b_intron_retention_panoramic.png` — 2,802 bp panoramic showing intron retention in DO234313 vs clean controls
- Existing Sashimi plot retained as Figure 4.6c

---

## Supporting Analyses

### Top genes analysis (Dean's request)
- Generated YES vs NO top 10 gene barplots by absolute count
- Identified mismatch in dynamic range (NO group has ~21× more total variants)
- Generated YES rate (proportion) version: TPTE leads at 65.0%, top 10 all 6–12× above cohort baseline (5.5%)
- Both versions saved; awaiting Dean's preference on which to retain

### 87 unique genes from 90 candidates
- Mapping NM accessions via NCBI gene2refseq + gene_info recovered 88/88 (100%) NM-to-symbol mappings
- 90 candidate variants span 87 unique genes including JAK1, NOTCH2, MAP3K1, PIK3CD, MTOR, EPHA2, RYR2 (cancer-relevant)
- Earlier 40-gene count (using TPM matrix's primary NM column) was incomplete due to multi-transcript-per-gene coverage gaps

---

## Writing Progress

### Methods chapter
- Section 3.3 updated to TPM-based truthset definition
- Three-tier mapping pipeline (gene2ensembl + gene2refseq + bioDBnet/HGNC) documented
- IGV validation protocol with formal four-criteria framework added to 3.4.3

### Results chapter
- Section 4.1 (Aim 1): completely rewritten with TPM data; addressed all six review points from prior critique (table reference, plateau wording, n=1,219 origin, summary completeness, mechanism count, "extending" vs "reinforcing" language)
- Section 4.2 (Aim 2): JAK1 description upgraded to Confirmed status with multi-layered evidence
- Section 4.2.3 (EPHA2/MAP3K1) under review for retention vs removal

### Presentation slides (for tomorrow's meeting with Nic)
- Two Aims slide (project restructure overview)
- Aim 1 Conclusions slide (three-card layout: high baseline PPV, marginal threshold gain, bimodal distribution)
- Discussion & Future Directions slide (three questions + three next steps)

---

## Pending Items

### Immediate (next session)
1. BioRender pipeline schematic for Methods Figure 3.1
2. Discussion + Conclusion chapters (currently empty, ~6–10 pages required)
3. Reference list compilation
4. Decide on inclusion/removal of Section 4.2.3 (EPHA2/MAP3K1)

### Awaiting supervisor input
- Dean: preference on top 10 genes plot (raw counts vs YES rate)
- Nic: feedback on Aim 2 scope — proof-of-concept vs. extended IGV validation vs. recurrence analysis vs. single-aim restructure
- Nic: 87 candidate genes vs. Frankell 2019's 76 coding drivers — overlap analysis worth pursuing?

### Technical debt
- HPC disk quota at 19/20 GB; gene2refseq removed (can be regenerated if needed)
- BAM access for additional candidate IGV validation: working

---

## Tomorrow's Agenda (Meeting with Nic)
1. Present Aim 1 conclusions: SpliceAI achieves 80–85% PPV in EAC across all thresholds
2. Present JAK1 as fully Confirmed Aim 2 case study
3. Discuss Aim 2 scope and direction options (A/B/C/D)
4. Confirm TPM as final truthset standard
5. Outline timeline for Discussion + Conclusion chapter completion (7 weeks remaining)
