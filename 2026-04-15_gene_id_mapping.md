# 2026-04-15 | 基因 ID 映射 & NCBI 数据库

**Project:** EAC SpliceAI Driver Variant Analysis  
**Institute:** QIMR Berghofer  
**HPC:** Avalon

---

## Overview

Downloaded NCBI reference databases for gene ID cross-referencing.
Working on Ensembl → RefSeq ID mapping for variant annotation.

---

## Tasks Completed

### 1. NCBI Reference Downloads

Downloaded two NCBI gene databases to local machine:

| File | Size | Purpose |
|------|------|---------|
| `Homo_sapiens.gene_info.gz` | ~5 MB | Gene name ↔ GeneID ↔ RefSeq mapping |
| `gene2ensembl.gz` | ~290 MB | GeneID ↔ Ensembl gene/transcript mapping |

Both downloaded to:
- `C:\Users\cheny\Documents\Homo_sapiens.gene_info\`
- `C:\Users\cheny\Documents\gene2ensembl\`

### 2. Gene ID Mapping Problem

Context: SpliceAI parsed outputs use RefSeq transcript IDs (NM_XXXXXX).
The Frankell 2019 driver list uses HGNC gene symbols.
Matching requires: `NM_XXXXXX → gene symbol`

Current approach in `match_drivers_by_refseq.py`:
- Hardcoded `DRIVER_REFSEQ` dictionary (76 genes × RefSeq IDs)
- Works for the Frankell 76 genes
- Problem: candidates outside the 76 need external mapping

Solution being built:
1. Parse `Homo_sapiens.gene_info` → `GeneID → symbol` table
2. Parse `gene2ensembl` → `GeneID → Ensembl transcript`
3. Cross-reference with `gene2refseq` (to be downloaded) → `GeneID → NM_ID`

### 3. Reviewed Supplementary_Table_S1 Status

After two-step filter:
- ~90 candidate variants pass (Any_splicing_aberration=YES + RNA-seq expression confirmed)
- These 90 are the input for RNA evidence quantification (`quantify_rna_evidence_v2.py`)
- Need gene symbol annotation for all 90 (not just the Frankell 11)

---

## Tools

| Tool | Purpose |
|------|---------|
| NCBI FTP | Database downloads |
| `Homo_sapiens.gene_info` | Gene ID reference |
| `gene2ensembl` | Ensembl cross-reference |

---

## Notes

- `gene2refseq.gz` still to be downloaded (large file ~2 GB)
- BioDBNet online tool as backup for batch Ensembl→RefSeq conversion
- All three databases needed for complete annotation pipeline
