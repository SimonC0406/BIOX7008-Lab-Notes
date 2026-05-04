# Progress Report — 2026-05-04

## Summary
Following Nic's restructuring of both Aims at the 2026-04-29 meeting, today focused on (i) systematic investigation of the *TP53* candidates that motivated the new Aim 2 focus, and (ii) selection of 30 stratified IGV candidates for the new Aim 1 PPV framework. The TP53 investigation revealed that R213*/R196* nonsense hotspots account for half the *TP53* YES set and are likely SpliceAI false positives at exonic stop-gained positions, with NMD evidence from IGV in DO50437. The 30 stratified Aim 1 candidates have been finalised across three MAX_DS bins, with all candidates having TPM ≥ 23 to ensure reliable IGV validation.

---

## Aim 1 Restructure — 30 Stratified IGV Candidates

### Design rationale
Per Nic's 2026-04-29 feedback, the original TPM > 0 PPV framework was insufficient because it only proves that the gene is expressed, not that splicing aberration actually occurs. The new design stratifies all 2,326 Step 1 variants (Any_splicing_aberration = YES) by MAX_DS bin and selects the top 10 by carrier-sample TPM in each bin, generating 30 systematic candidates for IGV-based splicing aberration confirmation. The resulting PPV per bin will reflect true splicing-aberration rate, not gene expression proxy.

### Bin boundaries (Strategy B, bimodal-aware)
- **Low**: MAX_DS [0.10, 0.30) — 713 variants
- **Mid**: MAX_DS [0.30, 0.70) — 593 variants
- **High**: MAX_DS [0.70, 1.00] — 867 variants

The bimodal MAX_DS distribution (peaks at 0.20–0.30 and 0.90–1.00, valley at 0.40–0.70) was identified by 10-bin histogram analysis and motivated the asymmetric Mid bin.

### Final 30 candidates
File: `/mnt/backedup/home/yanC/Aim1_30_IGV_candidates_v2.tsv`

**Low bin (MAX_DS 0.10–0.30, TPM 23–72):**
GUK1, PSMB1, TRIO, SMG1, COL5A1, SPIDR, RNF213, PLAAT4, INSR, PDHA1

**Mid bin (MAX_DS 0.30–0.70, TPM 25–49):**
XBP1, TAP1, COL1A2, MAT2A, LAMA3, ITPRIPL2, FLNA, COL1A1, ALYREF, MDN1

**High bin (MAX_DS 0.70–1.00, TPM 58–497):**
SI, RPL23, ATP5F1B, EPCAM, EEF1D, RPL3, EIF3G, LRP1, SLC2A1 (GLUT1), CHD4

EAC-relevant candidates include EPCAM (epithelial marker, MAX_DS 0.88), SLC2A1/GLUT1 (cancer metabolism, 0.83), CHD4 (chromatin remodeler, 0.77), LRP1 (0.97), TAP1 (immune evasion, 0.57), and XBP1 (UPR/cancer, 0.33).

### Sample distribution caveat
DO234350 appears 6 times across the 30 candidates (2 in Mid bin, 4 in High bin), reflecting both high RNA-seq quality and high mutation burden in this single sample. DO234230 appears 2 times. To be discussed with Nic — whether to add a per-sample diversity constraint or accept and acknowledge in Discussion.

### Pre-existing IGV cases not included by stratified selection
The four candidates IGV'd before the restructure (JAK1, ACAP3, GORASP2, ABCA13) are not in the 30-candidate set. ACAP3 (DO50392, TPM 27.86) ranks #21 in the High bin TPM ordering, falling below the top 10 cutoff of 58.02. These four cases will be reported as a separate "previously validated cases" section to avoid confirmation bias in the systematic stratified PPV calculation.

---

## Aim 2 Restructure — TP53 Focus

### Investigation of 16 TP53 YES candidates
Per Nic's interest in the *TP53* result topping the YES top-10 frequency ranking, all 16 TP53 candidates were extracted and investigated. Each variant occurs in a distinct sample (no hypermutators).

### Two recurrent ClinVar-pathogenic nonsense hotspots account for half the candidates
- **chr17:7,674,894 G>A** in 5 samples (DO234156, DO234317, DO234341, DO50437, DO50438): rs397516436, ClinVar pathogenic, **TP53 R213* Stop Gained**, ALFA frequency 0
- **chr17:7,674,945 G>A** in 3 samples (DO234191, DO234283, DO234365): rs397516435, ClinVar pathogenic, **TP53 R196* Stop Gained**

UCSC Genome Browser confirmed that both hotspots are within exonic CDS (TP53 negative-strand gene at chr17p13.1), not at canonical splice sites. The ClinVar "Stop Gained" classification is correct — these are nonsense mutations, not splice-site disrupting variants.

### TP53 expression analysis reveals universal low TPM in carriers
TP53 cohort distribution (n = 213 samples): median TPM 3.67, mean 5.49, max 39.09 (DO50321). All 16 TP53 candidate carriers show TPM < 10 (median 1.59, max 6.17 in DO234281). Only 2/16 carriers have TPM ≥ 5.

R213* carriers show systematically lower expression than the rest of the cohort:
- R213* mean TPM: 2.67
- Other 203 samples mean TPM: 5.56
- Mann-Whitney U (R213* < others): p = 0.10 — suggestive but not significant given n=5

This pattern is consistent with NMD of mutant *TP53* transcripts — heterozygous carriers retain ~50% wild-type allele expression while NMD eliminates the mutant transcript, halving overall TPM.

### IGV validation of three R213* carriers

**DO234156 (R213\*, TPM=1.56)** — Inconclusive
- DNA somatic confirmed (~50% A in tumour, 0 in normal)
- RNA tumour shows mutant allele expression (~50/50 A/G at variant)
- Sashimi pattern shows reduced canonical junction count (14) versus control 2 (41), with sporadic intron-region reads — possible partial intron retention signal but cannot be confirmed against background
- Methodological note: initial Sashimi colour interpretation was incorrect; tumour track was misidentified as control before being clarified by user reference to track-loading order

**DO234317 (R213\*, TPM=0.72)** — Inconclusive
- DNA somatic confirmed
- RNA shows very low coverage across entire *TP53* locus (sample-level low expression)
- Cannot reliably evaluate splicing patterns due to insufficient reads

**DO50437 (R213\*, TPM=5.67)** — Most informative case, supports NMD interpretation
- DNA somatic confirmed (~50% A in tumour DNA, 0% in normal)
- RNA tumour at variant position shows **no mutant allele expression** — only wild-type G reads detected
- Sashimi shows entirely canonical splicing (junction counts 74, 77, 79, 56 across visible junctions); no aberrant junctions or intron retention
- Interpretation: NMD has eliminated the mutant transcript. The variant's primary effect is protein truncation, not splicing disruption. SpliceAI's splicing prediction at this exonic nonsense position is a false positive

### Reframing of TP53 finding
Three observations now support reframing the *TP53* "exciting" result as a methodological caveat rather than novel discovery:

1. *TP53* tops the YES frequency ranking primarily due to mutation burden (~70% EAC mutation rate), not splicing-specific enrichment. YES rate (16/151 = 10.6%) is only ~2× cohort baseline (5.5%).
2. Half the TP53 YES candidates (8/16) are at two recurrent ClinVar-pathogenic stop-gained hotspots. SpliceAI flagging at these exonic nonsense positions appears to be a systematic false positive pattern.
3. Universal low *TP53* expression (median TPM 1.59 in carriers, all < 10) makes RNA-level validation infeasible at scale. The DO50437 case with the highest carrier TPM provides the clearest evidence of NMD-driven absence of mutant transcript.

---

## Decisions Pending Supervisor Input

### Aim 1 design questions for Nic
1. Whether to add a per-sample diversity constraint (e.g., max 2 candidates per sample) to reduce DO234350's 6× appearance
2. Whether to force-include previously IGV'd ACAP3 (and JAK1, GORASP2, ABCA13) in the 30-candidate set, or report separately
3. Whether to do all 30 IGVs or pilot subset (e.g., 5 per bin = 15) to assess trends first

### Aim 2 framing options
- **(i)** Keep TP53 focus, reframe as "SpliceAI at exonic nonsense hotspots — methodological caveat"
- **(ii)** Skip TP53, do full stratified Aim 1 only
- **(iii)** Switch to higher-expressed EAC driver gene focus (alternative drivers from the Frankell 76 list with TPM > 20)

---

## Output Files

### HPC (Avalon, /mnt/backedup/home/yanC/)
- `all_step1_variants.tsv` — 2,326 Step 1 variants with full SpliceAI annotation
- `Aim1_30_IGV_candidates_v2.tsv` — 30 stratified candidates with chrom/pos/gene/MAX_DS/TPM/mechanism
- `TP53_YES_candidates.tsv` — 16 TP53 candidates with TPM lookup

### Local outputs (/mnt/user-data/outputs/)
- `Aim1_30_IGV_candidates_FINAL.tsv` — full annotated version with gene symbols
- `Aim1_30_IGV_operating_list.tsv` — clean IGV operating list with locus + variant + mechanism strings
- `progress_report_2026-05-04.md` — this report

### IGV figure outputs (saved locally)
- DO234156 (R213\*): variant zoom, panoramic, Sashimi
- DO234317 (R213\*): variant zoom, panoramic, Sashimi, alignment view
- DO50437 (R213\*): variant zoom, wide zoom, Sashimi (5000 bp), Sashimi (50 bp)

---

## Methodology Errors Acknowledged Today

1. **Sashimi colour interpretation** — initially mis-identified track colours for DO234156, leading to a premature "false positive" verdict before the user corrected the colour-to-sample mapping. Lesson: always verify track-to-sample assignment by checking the BAM file URL or track loading order before interpreting Sashimi output.

2. **TP53 family over-extension** — initially proposed expanding Aim 2 to TP53/TP63/TP73 paralogs; user clarified Nic specified single-gene *TP53* focus. Corrected.

3. **Fabricated mapping breakdown** — earlier claimed a specific classification of the 633 unmapped protein-coding genes ("~200 readthrough, ~150 lncRNA host, ~100 novel") without having performed that analysis. User caught this through challenge questioning; the actual categorisation has not been performed.

---

## Communication

### Slack updates
- Pending: brief Slack to Dean summarising today's TP53 finding (low expression precludes IGV validation) and 30 Aim 1 candidates (ready to start IGV after Nic meeting)

### Tomorrow's Nic meeting agenda
1. Present TP53 expression findings (median TPM 1.59 in carriers, DO50437 NMD evidence)
2. Discuss reframing of TP53 result as methodological caveat
3. Walk through 30 stratified Aim 1 candidates and confirm sample diversity / pre-existing case decisions
4. Confirm pilot vs full IGV strategy for Aim 1
5. Update timeline given approximately 4–5 weeks remaining

---

## Key Takeaway

Nic's restructured Aims have produced clearer scientific framing for both Aims, but the TP53 investigation has revealed that the original "exciting" interpretation needs revision. The R213*/R196* nonsense hotspots represent a SpliceAI behaviour pattern (false positive at exonic stop-gained mutations), and the universal low *TP53* expression — likely amplified by NMD — limits the practical scope of RNA-based validation for tumour suppressor genes. The new stratified Aim 1 design with 30 high-TPM candidates across three MAX_DS bins should produce a robust IGV-confirmed PPV measurement once Nic's feedback on sample diversity and pilot scope is received.
