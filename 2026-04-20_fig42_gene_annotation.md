# 2026-04-20 | Figure 4.2 正式版 & 基因注释

**Project:** EAC SpliceAI Driver Variant Analysis  
**Institute:** QIMR Berghofer  
**HPC:** Avalon

---

## Overview

Wrote the formal `plot_ppv_curve.py` script and generated Figure 4.2.
Downloaded `gene2refseq.gz` and began full gene ID annotation pipeline.

---

## Tasks Completed

### 1. `plot_ppv_curve.py` — Figure 4.2

Formalised the PPV curve script for thesis publication:

- **Input files:**
  - `STEP1_FILE`: `/mnt/backedup/home/yanC/driver_gene_hits/all_step1_variants.tsv` (2,326 variants)
  - `STEP2_FILE`: pileup-confirmed single_variants intersection (~1,001 variants)
- **Output:**
  - `figure_4_2_ppv_curve.png` — publication-quality Figure 4.2
  - `ppv_vs_maxds_threshold.pdf` — vector version for thesis
  - `ppv_table.tsv` — Table 4.1 values

Generated: `figure_4_2_ppv_curve.png` (10:49), `maxds_distribution_step1.png` (11:11)

### 2. NCBI `gene2refseq.gz` Download

Downloaded the large NCBI gene-to-RefSeq mapping database:
- **File:** `gene2refseq.gz` (~2.2 GB)
- **Location:** `C:\Users\cheny\Documents\gene2refseq\`
- **Purpose:** Map GeneID → RefSeq transcript IDs for annotation of all 90 candidates

### 3. BioDBNet ID Conversion

Used BioDBNet web tool to batch-convert Ensembl gene IDs → RefSeq accessions:
- **Input:** `na_protein_coding_ensembl_ids.txt` (protein-coding genes without RefSeq mapping)
- **Output:** `biodbnet_result.txt`
- **Result:** Many IDs returned `-` (no RefSeq mapping for non-canonical transcripts)

These IDs will need manual curation or Ensembl VEP annotation fallback.

---

## Tools

| Tool | Purpose |
|------|---------|
| `plot_ppv_curve.py` | Figure 4.2 generation |
| NCBI gene2refseq | RefSeq mapping database |
| BioDBNet | Batch Ensembl → RefSeq conversion |
| `matplotlib` (Agg backend) | Headless plotting on HPC |

---

## Output Files

| File | Description |
|------|-------------|
| `figure_4_2_ppv_curve.png` | Thesis Figure 4.2 |
| `maxds_distribution_step1.png` | Step 1 variant MAX_DS distribution |
| `gene2refseq.gz` | NCBI RefSeq mapping database |
| `biodbnet_result.txt` | BioDBNet conversion results |
| `na_protein_coding_ensembl_ids.txt` | Ensembl IDs lacking RefSeq mapping |

---

## Known Issues

- ~15+ Ensembl IDs returned no RefSeq match in BioDBNet — likely non-canonical transcripts
- `gene2refseq` parsing required to resolve these
