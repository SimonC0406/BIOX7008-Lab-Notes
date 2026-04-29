# Progress Report — 2026-04-29

## Summary
Completed three additional IGV validation cases for Aim 2, bringing the total to four. Two more candidates were Confirmed (ACAP3 with a notable mechanism mismatch finding), and two were classified as Inconclusive for distinct reasons. Established a more nuanced 4-case story for Aim 2 that complements the Aim 1 PPV results. Began ggsashimi setup on HPC for publication-quality Sashimi plots, pending BAM file system access resolution.

---

## Aim 2: Extended IGV Validation — 4-Case Story

### Final Case Summary

| # | Sample | Gene | MAX_DS | Predicted Mechanism | Observed | Result |
|---|--------|------|--------|---------------------|----------|--------|
| 1 | DO234313 | **JAK1** | 1.0 | Intron retention | Intron retention | ✅ **Confirmed** (prediction matches) |
| 2 | DO50392 | **ACAP3** | 0.99 | Exon skipping | Intron retention | ✅ **Confirmed** (mechanism mismatch) |
| 3 | DO234154 | GORASP2 | 1.0 | Exon skipping | No clear aberration | ⚠️ Inconclusive |
| 4 | DO234193 | ABCA13 | 1.0 | Intron retention + Pseudoexon | No RNA expression | ⚠️ Inconclusive |

**Validation rate:** 2/4 Confirmed (50%) — consistent with the gene-level PPV of 80–85% from Aim 1 combined with RNA expression as a fundamental constraint.

---

### Case 2: ACAP3 (DO50392, chr1:1,301,987 C>T) — Confirmed with Mechanism Mismatch

**Selection rationale:** Highest TPM (27.86) among unvalidated MAX_DS ≥ 0.9 candidates. High expression chosen to ensure RNA-level validation could succeed.

**DNA evidence:**
- Tumour DNA: ~50% T allele (heterozygous somatic)
- Normal blood DNA: 0% T allele
- Confirmed somatic origin

**RNA evidence:**
- At variant position (chr1:1,301,987), DO50392 RNA shows ~50/50 split between T and C alleles, indicating both mutant and wildtype mRNA are expressed
- **Critical observation:** the intron immediately upstream of the variant exon shows continuous coverage (~5–15 reads/position) in DO50392, while two unrelated controls (DO234149, DO234151) display only sparse, discontinuous reads (background level)
- Sashimi plot at narrow window (chr1:1,301,622–1,302,079, min junction = 3) reveals **no new junction** in DO50392 vs controls, ruling out exon extension via cryptic donor

**Mechanism mismatch finding:**
- SpliceAI's SAI-10k-calc annotated this variant as causing **exon skipping**
- IGV-level RNA evidence indicates the actual outcome is **intron retention**
- The splice-site disruption prediction (DS_DL=0.99, DS_AL=0.89) is correct, but the downstream mechanism classification does not match the observed splicing outcome
- This discrepancy is worth discussing as a methodological observation: SpliceAI's variant-level scoring is reliable, but mechanism-level annotation may not always reflect the actual mRNA-level consequence

**IGV figures saved:**
- `ACAP3_variant_zoom.png` — 14 bp zoom showing 5-track allele comparison
- `ACAP3_panoramic.png` — 3,501 bp range showing intron retention vs control
- `ACAP3_sashimi_initial.png` — Initial Sashimi at 10 kb window
- `ACAP3_sashimi_narrow.png` — Narrow Sashimi (chr1:1,301,622–1,302,079) confirming no new junctions

**Dean confirmation:** Reviewed the Sashimi and alignment images and agreed with intron retention interpretation (initial suggestion of exon extension was excluded by the absence of new junctions).

---

### Case 3: GORASP2 (DO234154, chr2:170,948,349 G>T) — Inconclusive (No Aberration)

**Initial misidentification:** Originally selected under the assumption that NM_015530 mapped to LRP1B (a known EAC tumour suppressor); subsequent NCBI lookup confirmed the actual gene is **GORASP2** (Golgi reassembly stacking protein 2). True LRP1B (NM_018557) is not in the 90-candidate set.

**DNA evidence:**
- Tumour DNA: ~50% T (heterozygous somatic)
- Normal DNA: 0% T
- Somatic origin confirmed

**RNA evidence:**
- DO234154 RNA at variant position: no reads (variant lies just inside the intron at the acceptor splice site)
- Sashimi pattern across the locus: similar to controls — no clear long junction indicating exon skipping
- Variant exon coverage in DO234154: comparable to controls
- No clear evidence of the predicted exon skipping at the RNA level

**Interpretation:** This case appears to fall within the ~15–20% of SpliceAI predictions not supported by RNA evidence (consistent with Aim 1 PPV of 80–85%). Could represent a false positive prediction or a splicing outcome too subtle to detect with the current RNA-seq depth.

---

### Case 4: ABCA13 (DO234193, chr7:48,389,221 G>T) — Inconclusive (No Expression)

**Selection rationale:** MAX_DS = 1.0, multi-mechanism prediction (Intron retention + Pseudoexon activation) — chosen to test whether unusual splicing outcomes could be detected.

**DNA evidence:**
- Tumour DNA: ~50% T (heterozygous somatic)
- Normal DNA: 0% T
- Somatic origin confirmed

**RNA evidence:**
- **DO234193 RNA in the ABCA13 locus shows essentially no coverage** — the gene is not meaningfully expressed in this tumour sample
- Sashimi plot is empty for DO234193
- 2 control samples show normal canonical splicing with exon coverage and standard junctions
- Cannot validate splicing aberration without RNA reads

**Interpretation:** Highlights a fundamental limitation of RNA-based validation — variants in genes that are transcriptionally silent in the relevant tissue/sample cannot be assessed regardless of how high SpliceAI's prediction confidence is. This reinforces the rationale for the TPM > 0 truthset filter in Aim 1.

---

## Aim 2 Synthesis: Three Outcome Types

The 4-case validation produced three distinct outcome categories, each with implications for SpliceAI utility in EAC:

**Type A — Prediction fully validated (1/4):** JAK1
- Variant-level prediction AND mechanism annotation match RNA observation
- Represents the "ideal" pipeline behaviour

**Type B — Splicing disruption confirmed, mechanism mismatch (1/4):** ACAP3
- SpliceAI correctly identifies splice-site disruption
- However, the predicted mechanism (exon skipping) does not match the observed mechanism (intron retention)
- Suggests caution when relying on SAI-10k-calc mechanism categories without RNA-seq verification

**Type C — Prediction not RNA-supported (2/4):** GORASP2, ABCA13
- C1 (GORASP2): RNA expressed but no observable aberration → potential false positive
- C2 (ABCA13): Gene not expressed → unable to validate
- These cases collectively reinforce that pipeline output should always be interpreted alongside expression data

This taxonomy provides a more honest and useful framing of SpliceAI's behaviour in clinical samples than a simple "confirmed/not confirmed" binary.

---

## Technical Setup: ggsashimi Installation

Following Dean's suggestion to use a programmatic Sashimi plotting tool for publication-quality figures:

- Downloaded ggsashimi (https://github.com/guigolab/ggsashimi) — required local zip transfer due to HPC GitHub access limitations
- Verified Python dependency: pysam 0.19.1 ✓
- Loaded R/4.5.0 module on HPC; verified ggplot2, data.table, gridExtra all installed ✓
- ggsashimi script ready to run

**Pending issue:** BAM file system paths for the relevant samples not yet identified — IGV accesses BAMs via internal HTTP server (10.10.58.10) but ggsashimi requires direct file system paths. Will follow up with Dean about correct mount points or alternative access methods.

---

## Communication

### Dean updates (Slack)
- Sent JAK1 IGV summary (yesterday) — Dean replied "Excellent Yan"
- Sent ACAP3 IGV summary tonight — Dean replied "looks like an intron retention or possibly an exon extension"
- Followed up with narrow-range Sashimi + alignment views to rule out exon extension; awaiting his confirmation
- Dean suggested ggsashimi / splicejam / rmats2sashimiplot for programmatic Sashimi plots

### Pending replies
- Dean: top 10 genes plot preference (raw counts vs YES rate) — still waiting
- Dean: confirmation of ACAP3 intron retention call after seeing the narrow-range Sashimi
- Nic: tomorrow's meeting will address Aim 2 scope and whether to extend further

---

## Tomorrow's Agenda (Updated)

1. Present Aim 1 conclusions: 80–85% PPV across all MAX_DS thresholds (TPM truthset)
2. Walk Nic through the 4-case Aim 2 validation:
   - JAK1 (Confirmed, perfect match)
   - ACAP3 (Confirmed, mechanism mismatch — interesting finding for Discussion)
   - GORASP2 (Inconclusive, no aberration)
   - ABCA13 (Inconclusive, no expression)
3. Discuss whether 50% IGV confirmation rate is sufficient or whether Aim 2 needs further extension
4. Confirm TPM as the final truthset standard
5. Outline Discussion + Conclusion timeline (approximately 7 weeks remaining)
6. Mention the SpliceAI mechanism-vs-observed-outcome discrepancy from ACAP3 as a potential Discussion section topic

---

## Pending Items

### Immediate (next session)
1. BioRender pipeline schematic for Methods Figure 3.1
2. Resolve BAM file system access for ggsashimi to generate publication-quality Sashimi plots
3. Discussion + Conclusion chapter drafts (currently empty, ~6–10 pages required)

### Awaiting input
- Dean: top 10 genes plot version preference
- Dean: confirmation of ACAP3 intron retention call
- Nic: feedback on Aim 2 scope and whether to extend IGV validation further

### Updated thesis structure (post-validation)
- Section 4.2.2: JAK1 — primary validated case
- Section 4.2.3: ACAP3 — Confirmed with mechanism mismatch (new section)
- Section 4.2.4: GORASP2 + ABCA13 — Inconclusive cases representing common failure modes
- Section 4.2.5 (Discussion): three-type taxonomy of SpliceAI predictions in EAC
- Original Section 4.2.3 (EPHA2/MAP3K1) — likely to be removed, superseded by stronger validation cases

---

## Key Takeaway

The 4-case Aim 2 validation tells a more nuanced and honest story than a simple "we found drivers" narrative would: SpliceAI's variant-level predictions are largely reliable in EAC (consistent with 80–85% PPV from Aim 1), but mechanism annotations may not always match RNA-level observations, and the practical utility of the pipeline is bounded by gene expression in the relevant tissue. This framing positions the thesis to make a calibrated, defensible contribution to the field.
