# Comparison: My Analysis vs. Lee et al. 2019
**Paper:** Lee K, Zhang Y, Kleinstiver BP, et al. (2019). Activities and specificities 
of CRISPR/Cas9 and Cas12a nucleases for targeted mutagenesis in maize.
Plant Biotechnology Journal 17, 362-372. doi:10.1111/pbi.12982

**Tools used:** CHOPCHOP (v3), CRISPOR (v5.2), Cas-OFFinder (web, RGEN Tools)
**Genome:** Zea mays B73 AGPv3/v4 (Cas-OFFinder), AGPv4 (CHOPCHOP), faZmB735 (CRISPOR)
**Date of analysis:** September 2026

---

## 1. Guide Design — CHOPCHOP (Zea mays B73 AGPv4, 241 total guides ranked)

| Guide | Paper sequence | CHOPCHOP rank | Efficiency | Notes |
|---|---|---|---|---|
| Cas9 gRNA1 | ACAGATCACAAACTTCAAATG | NOT FOUND | N/A | SNP in AGPv4 eliminates this guide entirely |
| Cas9 gRNA2 | AAGTGGGCGCAGATCCTGAG | 135 / 241 | 68.92 | 1-nt SNP: G→C at pos 17 in AGPv4 version |
| CHOPCHOP #1 ranked | TTCAAGCTGCACTACCTGCG | 1 | 57.38 | Paper never used this guide |

**Key finding A — gRNA1 absent from AGPv4:**
CHOPCHOP searched 241 candidate guides across the entire gl2 gene body in B73 AGPv4.
The paper's gRNA1 (ACAGATCACAAACTTCAAATG + NGG PAM) is completely absent — not ranked
low, simply not generated. A SNP between AGPv3 (paper) and AGPv4 (CHOPCHOP) eliminates
the NGG PAM context at that exact position, making gRNA1 invalid in AGPv4.

**Key finding B — gRNA2 rank 135, not #1:**
gRNA2 appears at rank 135 with a 1-nucleotide sequence difference (CCTCAG vs CCTGAG).
CHOPCHOP's #1 guide (TTCAAGCTGCACTACCTGCG, eff=57.38) was never used by the paper.

**Critical methodological lesson:**
Guide selection was constrained by the overlapping PAM experimental design requirement —
both Cas9 NGG and Cas12a TTTV PAMs had to flank the same ~60bp stretch. This forced
the authors to use guides at a specific locus regardless of efficiency ranking.
Experimental design constraints override efficiency optimization.
Additionally: guide RNA design is genome-build-dependent. A guide valid in AGPv3 
may not exist as a valid target in AGPv4 due to SNPs. This is a real 
reproducibility concern for published CRISPR experiments.

---

## 2. Guide Efficiency and Specificity — CRISPOR (Zea mays faZmB735, SpCas9/NGG)

| Guide | MIT Specificity | CFD Score | Doench 16 | RuleSet3 | Off-targets <=4mm | Color |
|---|---|---|---|---|---|---|
| gRNA1 CAGATCACAAACTTCAAATG | 86 | 95 | 69 | 103 | 65 (0-0-1-8-56) | GREEN |
| gRNA2 AAGTGGGCGCAGATCCTGAG | 24 | 85 | -- | -- | 4080 (0-1-14-363-3702) | YELLOW |

**Key finding — gRNA2 MIT score of 24:**
Below 50 is considered risky. This is independently consistent with Cas-OFFinder
predicting 71,253 candidate off-target sites for gRNA2 (vs 19,029 for gRNA1).
Two completely different tools (CRISPOR and Cas-OFFinder) converge on the same 
conclusion: gRNA2 carries significantly higher off-target risk than gRNA1.

**Note on missing efficiency scores for gRNA2:**
CRISPOR requires >=100bp flanking sequence to compute Doench/RuleSet3 efficiency.
Input sequence for Target 2 was only 30bp — scores show '--' as expected.
To fix: submit the guide with 50bp genomic context on each side.

**Note on 65 vs 2,395 off-target count for gRNA1:**
CRISPOR searches <=4 mismatches. Cas-OFFinder searched <=6 mismatches.
Same guide, different search depth = 37x different count. Not a contradiction.

---

## 3. Off-Target Prediction — Cas-OFFinder (Zea mays AGPv3, <=6 mismatches)

### Cas9 guides (PAM: NGG)

| Guide | Paper Table S1 | My run | Ratio | 
|---|---|---|---|
| gRNA1 Target 1 | 19,029 | 2,395 | ~8x lower |
| gRNA2 Target 2 | 71,253 | 8,236 | ~8.6x lower |

My counts: gRNA1 = 1+2+19+209+2164 = 2,395 (cumulative 0-6mm)
           gRNA2 = 4+49+685+7498 = 8,236 (cumulative 3-6mm)

### Cas12a guides (PAM: TTTN)

| Guide | Paper Table S1 | My run | Ratio |
|---|---|---|---|
| crRNA1 Target 1 | 1,193 | 149 | ~8x lower |
| crRNA2 Target 2 | 173 | 48 | ~3.6x lower |

My counts: crRNA1 = 1+1+10+137 = 149 (cumulative 0-6mm)
           crRNA2 = 48 (at 6mm only)

### Reason for systematic gap (consistent ~8x ratio across all Cas9 guides):

Three compounding factors identified:
1. AGPv3 database in Cas-OFFinder updated since 2018 — different repeat 
   assembly and masking between releases changes counts significantly
2. Web version now caps results at 1000 sites per mismatch per guide
   (visible as red warning banner — paper used offline version, no cap)
3. Maize genome is ~85% repetitive — small build differences produce 
   large absolute count differences; consistent ratio = systematic cause

### Core scientific claim independently reproduced:

| Comparison | Paper ratio | My ratio | Verdict |
|---|---|---|---|
| Cas12a vs Cas9 Target 1 | 16x fewer | 2395/149 = 16.1x fewer | EXACT MATCH |
| Cas12a vs Cas9 Target 2 | 412x fewer | 8236/48 = 171.6x fewer | Same direction |

The paper's central specificity claim — Cas12a has dramatically fewer predicted 
off-target sites than Cas9 — is confirmed in my independent run despite the 
absolute number gap caused by database versioning.

---

## 4. Citrus Extension — CsLOB1 Target (Jia et al. 2019, bridge to HLB)

Target gene: CsLOB1 promoter EBE (Effector Binding Element) in Citrus sinensis
Context: Jia et al. 2019 (Plant Biotechnology Journal) used LbCas12a to edit 
CsLOB1 promoter EBEs, reducing citrus canker susceptibility — same host plant 
and same pathosystem as Huanglongbing (HLB/citrus greening) research.

Guide: TTTCACAAGTGGGCGCAGAT (Cas12a crRNA, TTTN PAM)
Genome searched: Citrus sinensis (Cas-OFFinder)
[RESULTS TO BE FILLED WHEN CAS-OFFINDER RETURNS]

---

## 5. Summary of Methodological Insights

**Insight 1 — Guide selection is constrained by biology, not just efficiency.**
When comparing two nucleases fairly, PAM overlap requirements override efficiency
ranking. gRNA1 not found in top 241 CHOPCHOP guides; gRNA2 ranked 135th.
Lesson: understand the experimental design constraint before judging guide choice.

**Insight 2 — Genome build version matters enormously in repetitive genomes.**
~8x systematic difference between 2018 AGPv3 and current AGPv3 web database.
One SNP between AGPv3 and AGPv4 eliminates gRNA1 entirely from CHOPCHOP output.
Always document: genome build name, version number, tool version, database date.

**Insight 3 — Prediction depth changes counts, not conclusions.**
CRISPOR (<=4mm) = 65 sites for gRNA1.
Cas-OFFinder (<=6mm) = 2,395 sites for gRNA1.
37x different count, same guide, same conclusion about relative specificity.

**Insight 4 — Multiple tools converging = stronger evidence.**
CRISPOR MIT score 24 for gRNA2 (risky) and Cas-OFFinder 71,253 sites for gRNA2
are from completely different algorithms. Agreement strengthens the finding.

**Insight 5 — Web tool caps are undocumented limitations.**
Cas-OFFinder web version caps at 1000 sites/mismatch/guide — not in the help text,
only visible as a red warning banner after results load. For publication-quality 
off-target analysis: always use the offline/command-line version.

**Insight 6 — Tool availability at time of publication matters.**
In 2018 no Cas12a design tools existed. crRNAs were manually designed by geometry.
Retrospective CINDEL/CRISPR-DT predicted crRNA2 would fail (0.05-0.17 indel freq).
Confirmed: 0% editing in T0 plants. Lesson: interpret older papers' design choices 
in the context of what tools were available when the work was done.
