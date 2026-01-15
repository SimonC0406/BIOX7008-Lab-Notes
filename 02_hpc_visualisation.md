# Day 2 — HPC Access & SpliceAI Visualisation

**Date:** 2026-03-28  
**Location:** QIMR Berghofer — Avalon HPC

---

## HPC Session

Successfully logged into the HPC and started an interactive session on a compute node before running any programs:

```bash
qsub -X -I -l ncpus=2 -l mem=10G -l walltime=12:00:00
# Allocated to: hpcnode069
```

> ⚠️ Important: Always start an interactive session before running any programs. The login node (`hpcpbs01`) is for file management only.

---

## Data Access

Confirmed access to the project directory:

```
/working/genomeinfo/share/analysis/Yan_Chen_Masters_Project/spliceAI_parsed_outputs/
```

- **208 SpliceAI parsed output files** (`.vcf` format)
- One file per tumour-normal paired sample
- Key columns: `MAX_DS`, `Any_splicing_aberration`, `MAX_DS_CLINICAL`, splicing mechanism columns

---

## IGV Setup

- Loaded IGV v2.18.2 via `module load igv/2.18.2`
- Attempted to load GTF annotation file:
  `/reference/gene_models/GRCh38_Ensembl_v110/primary_files/Homo_sapiens.GRCh38.110.gtf`
- **Issue:** GTF file required sorting and indexing before IGV could load it
- Sorted and indexed the GTF file locally:

```bash
igvtools sort ~/Homo_sapiens.GRCh38.110.gtf ~/Homo_sapiens.GRCh38.110.sorted.gtf
igvtools index ~/Homo_sapiens.GRCh38.110.sorted.gtf
```

- GTF loading was very slow over X11 forwarding — to be revisited

---

## SpliceAI Output Visualisation

Wrote and ran a Python script (`plot_spliceai.py`) to extract `MAX_DS` and `Any_splicing_aberration` from all 208 files and generate plots.

### Boxplot & Violin Plot — MAX_DS by Any_splicing_aberration

- **NO group:** MAX_DS concentrated near 0 (median ≈ 0.02)
- **YES group:** MAX_DS much higher and wider (median ≈ 0.39, range 0.05–1.0)
- Clear separation between groups confirms that MAX_DS is a strong predictor of splicing aberrations
- Also validates the filtering strategy: requiring both `MAX_DS > 0.5` AND `Any_splicing_aberration = YES`

### Additional Plots Generated

| Plot | Key Finding |
|------|-------------|
| Histogram | Vast majority of variants have MAX_DS ≈ 0; high-confidence splicing variants are rare |
| Mechanism barplot | Exon Skipping (1080) > Partial Exon Deletion (623) > Intron Retention (209) > Pseudoexon Activation (102) |
| Frameshift pie chart | 43.9% of splicing aberration variants predicted to cause frameshift → NMD risk |

---

## Tools Used Today

| Tool | Purpose |
|------|---------|
| `qsub -X -I` | Interactive session on compute node |
| `module load igv/2.18.2` | Load IGV |
| `igvtools sort/index` | Prepare GTF annotation file |
| `module load python/3.9.13` | Load Python |
| `plot_spliceai.py` | Extract and visualise SpliceAI outputs |
| FileZilla | Transfer plots from HPC to local laptop |

---

## Next Steps

- [ ] Complete IGV setup with sorted GTF annotation
- [ ] Load RNA-seq BAM file into IGV and navigate to variant positions
- [ ] Apply filters (MAX_DS > 0.5 + Any_splicing_aberration = YES) across all 208 samples
- [ ] Cross-reference hits with Frankell 2019 EAC driver gene list
