# 2026-03-31 | SpliceAI Filtering & Driver Gene Matching

**Project:** Somatic Intronic Driver Variants (SIDs) in Esophageal Adenocarcinoma (EAC)  
**Institute:** QIMR Berghofer Medical Research Institute  
**Supervisor:** Dean  
**HPC:** Avalon (`yanC@hpcnode074`)

---

## Overview

Today completed the full SpliceAI variant filtering pipeline and driver gene matching
across the EAC cohort (n=208 paired tumor-normal WGS samples).
Identified **11 driver genes** from the Frankell 2019 76-driver framework
with putative intronic splicing-altering variants.

---

## Tasks Completed

### 1. SpliceAI Variant Filtering (208 samples)

Applied two-pass filter to all parsed SpliceAI outputs:

| Filter | Criterion |
|--------|-----------|
| SpliceAI score | `MAX_DS > 0.5` |
| Splicing flag | `Any_splicing_aberration = YES` |

- **Input directory:** `/working/genomeinfo/share/analysis/Yan_Chen_Masters_Project/spliceAI_parsed_outputs/`
- **Output:** `~/driver_gene_hits/all_filtered_variants.tsv`
- **Backup:** `/mnt/backedup/home/yanC/driver_gene_hits/all_filtered_variants.tsv`

---

### 2. Visualizations Generated

All figures saved to `~/spliceai_plots/`.

| Plot | Description |
|------|-------------|
| Boxplot | MAX_DS score distribution across 208 samples |
| Violin plot | Per-sample variant score spread |
| Mechanism barplot | Breakdown by splicing event type (AL / DL / AG / DG) |

---

### 3. Driver Gene Matching

- **Script:** `match_drivers_by_refseq.py`
- **Reference framework:** Frankell et al. 2019 — 76 EAC driver genes
- **Input:** `~/driver_gene_hits/all_filtered_variants.tsv`
- **Output:** `~/driver_gene_hits/driver_gene_summary_final.tsv`
- **Backup:** `/mnt/backedup/home/yanC/driver_gene_hits/driver_gene_summary_final.tsv`

---

## Results

### Summary Statistics

| Metric | Value |
|--------|-------|
| Total filtered intronic variants | 21 |
| Driver genes hit (Frankell 76) | **11** |
| Affected samples | **20 / 208 (9.6%)** |

---

### Driver Gene Hits

```
driver_gene    variant_count    sample_count
TP53           7                7
JAK1           3                3
RNF43          2                2
ACVR1B         1                1
AXIN1          1                1
CDH11          1                1
CDKN2A         2                1
CHD4           1                1
EPHA2          1                1
POLQ           1                1
SMARCA4        1                1
```

---

### Interpretation

#### High-priority hits

| Gene | Variants | Samples | Notes |
|------|----------|---------|-------|
| **TP53** | 7 | 7 | Most recurrent (3.4% prevalence); canonical EAC driver; intronic SIDs here carry strong functional significance |
| **JAK1** | 3 | 3 | JAK-STAT pathway; recurrent intronic disruption notable |
| **RNF43** | 2 | 2 | Wnt pathway negative regulator; established EAC driver (Frankell 2019) |
| **CDKN2A** | 2 | **1** | ⚠️ Two independent intronic variants in the same sample — candidate biallelic inactivation event; warrants priority validation |

#### Single-sample hits
`ACVR1B`, `AXIN1`, `CDH11`, `CHD4`, `EPHA2`, `POLQ`, `SMARCA4`
— each with 1 variant in 1 sample; supportive evidence for the SID landscape.

---

### Notes & Known Issues

- **Gene ID mapping corrections** applied during matching:
  Earlier pipeline versions had incorrect RefSeq → gene name mappings for:
  `CTNNA2`, `NCOA1`, `TMX4`, `CHN1`, `ACE`
  These are now correctly mapped in `match_drivers_by_refseq.py`.

- CDKN2A `variant_count=2, sample_count=1` — same sample carries two intronic variants
  in the same driver gene; possible biallelic LOF mechanism, to be explored with
  SAI-10k-calc reading frame logic (ΔL mod 3 ≠ 0 → NMD-mediated LOF prediction).

---

## Next Steps

### Immediate (validation)
- [ ] Extract variant coordinates for TP53, CDKN2A, JAK1 from `all_filtered_variants.tsv`
- [ ] Run pysam junction read evidence script for priority genes
- [ ] Generate IGV batch screenshots for candidate variants
- [ ] Re-score top candidates with Pangolin for orthogonal confirmation

### Analysis
- [ ] Apply SAI-10k-calc ΔL mod 3 logic to predict NMD vs. partial splicing outcomes
- [ ] Verify MANE Select transcript anchoring (GRCh38) for all 11 hit genes
- [ ] Check CDKN2A biallelic candidate: are the two variants on opposite alleles (VAF analysis)?

### Writing
- [ ] Draft thesis Results section: "Driver gene-associated SIDs in EAC"
- [ ] Prepare figure legends for spliceai_plots visualizations
- [ ] Update Methods section with final filter thresholds (MAX_DS > 0.5)

---

## File Index

| File | Path |
|------|------|
| All filtered variants | `~/driver_gene_hits/all_filtered_variants.tsv` |
| Driver gene summary | `~/driver_gene_hits/driver_gene_summary_final.tsv` |
| Matching script | `~/match_drivers_by_refseq.py` |
| Plots directory | `~/spliceai_plots/` |
| Raw SpliceAI parsed outputs | `/working/genomeinfo/share/analysis/Yan_Chen_Masters_Project/spliceAI_parsed_outputs/` |
| Backup (driver hits) | `/mnt/backedup/home/yanC/driver_gene_hits/` |
