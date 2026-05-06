# Progress Report — 2026-05-06

**Date:** 2026-05-06  
**Node:** `yanC@hpcnode070`  
**Project:** Somatic Intronic Driver Variants in EAC (n=208 paired tumour-normal WGS)

---

## What I Did Today

1. Downloaded and reviewed aberration type distribution figure (`aberration_distribution.pdf/.png`)
2. Extracted all TP53 variants from 208 parsed VCFs and compared aberration types between YES/NO groups
3. Split TP53 YES group into nonsense hotspot vs non-hotspot subgroups

---

## Aberration Type Distribution Figure

Generated in previous session; reviewed today.

**Figure:** `aberration_distribution.pdf` / `.png`  
**Location:** `/mnt/backedup/home/yanC/`

Mutually-exclusive binning of all 2,326 Step 1 variants:

| Aberration type | n | % |
|---|---|---|
| Exon skipping | 846 | 36.4% |
| Increased exon inclusion | 435 | 18.7% |
| Partial exon deletion | 422 | 18.1% |
| Multi-type (exactly 2) | 336 | 14.4% |
| Intron retention | 108 | 4.6% |
| Pseudoexon activation | 101 | 4.3% |
| Partial intron retention | 78 | 3.4% |

**Notes:**
- Increased_exon_inclusion never co-occurs with other types (overlapping count = mutually-exclusive count)
- All multi-type variants are exactly 2 types — zero ≥3
- Minor label issue: x-axis shows "≥2 aberrations" for Multi-type bar; consider updating to "exactly 2 aberrations"

---

## Aim 2 — TP53 Aberration Type Analysis

### Data extraction

Extracted all TP53 (NM_000546) variants from 208 parsed VCFs.

```
Input:  /working/genomeinfo/share/analysis/Yan_Chen_Masters_Project/spliceAI_parsed_outputs/*.parsed.vcf
Output: /mnt/backedup/home/yanC/TP53_all_variants.tsv
```

- Total TP53 variants: 151 (YES=16, NO=135)
- Consistent with previously recorded counts

### YES vs NO comparison

```
Output: /mnt/backedup/home/yanC/TP53_aberration_comparison.tsv
```

NO group all-zero across all aberration types — definitionally expected (Any_splicing_aberration=NO implies all sub-types NO). Comparison limited in interpretive value; YES group internal breakdown is the meaningful analysis.

### Hotspot vs non-hotspot split

YES group (n=16) split by POS:
- **Recurrent nonsense hotspot** (n=8): POS 7674894 (R213*, 5 samples) + POS 7674945 (R196*, 3 samples)
- **Non-hotspot** (n=8): all remaining YES variants

| Aberration type | Hotspot (n=8) | Non-hotspot (n=8) |
|---|---|---|
| Exon skipping | 8 (100%) | 5 (62.5%) |
| Partial exon deletion | 0 (0%) | 5 (62.5%) |
| Intron retention | 0 (0%) | 1 (12.5%) |
| Partial intron retention | 0 (0%) | 1 (12.5%) |
| Pseudoexon activation | 0 (0%) | 1 (12.5%) |
| Increased exon inclusion | 0 (0%) | 0 (0%) |

**Key finding:** Nonsense hotspot group shows 100% Exon_skipping with no other types — consistent with systematic SpliceAI false positive at exonic stop-gained positions. Confirmed by DO50437 IGV (zero mutant allele in RNA, entirely canonical splicing junctions). Non-hotspot group shows heterogeneous type distribution, representing true splicing candidates.

**Non-hotspot variants reviewed:**

| Sample | POS | MAX_DS | Notes |
|---|---|---|---|
| DO234281 | 7676274 | 0.99 | Exon_skipping + Partial_exon_deletion; highest-priority IGV target |
| DO234218 | 7673609 | 1.00 | Exon_skipping + Partial_exon_deletion |
| DO50389 | 7675052 | 1.00 | Partial_exon_deletion + Intron_retention |
| DO234446 | 7674857 | 0.99 | Exon_skipping + Partial_intron_retention |
| DO234383 | 7674974 | 0.89 | Exon_skipping |
| DO234448 | 7675234 | 0.81 | Partial_exon_deletion |
| DO50349 | 7675994 | 0.72 | Exon_skipping + Partial_exon_deletion |
| DO234343 | 7673254 | 0.15 | Pseudoexon_activation; low MAX_DS outlier |

**Caveat:** Hotspot classification based on POS only (two hardcoded ClinVar positions). No VEP consequence annotation in parsed VCFs — cannot formally confirm whether non-hotspot variants are intronic or exonic without additional annotation.

---

## Pending (post Nic meeting 2026-05-07)

- Confirm Aim 2 direction: retain TP53 / switch to higher-TPM EAC driver
- Confirm whether Dean's aberration-type comparison approach is endorsed by Nic
- VEP annotation for 8 non-hotspot TP53 variants to formally classify exonic vs intronic
- Aim 1: resolve DO234350 sample bias (appears 6×), ACAP3 inclusion question, pilot (15) vs full (30) IGV
- Figure 3.1 pipeline schematic — awaiting Aim design confirmation
- Multi-type pair breakdown (which 2-type combinations most common in 336 variants)
- Push lab_notes to GitHub
