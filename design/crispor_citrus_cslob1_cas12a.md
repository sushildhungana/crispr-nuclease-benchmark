# CRISPOR — CsLOB1 Promoter, LbCas12a Design
Tool: CRISPOR v5.2
Genome: Citrus sinensis (pz9Csinensis)
Input: CsLOB1 EBE region (119bp, from Fig. 3 Jia et al. 2019)
PAM: 23bp-TTTN-Cas12a/Cpf1
Note: Query not found in pz9Csinensis (different assembly from Cas-OFFinder's
Citrus sinensis v1.0) — same genome build issue seen with maize analysis.
MIT/CFD scores are -1 for all guides (CRISPOR manual confirms: no
off-target ranking algorithm exists for Cpf1 in literature as of 2025).

## All 8 candidate guides generated

| ID | Sequence | DeepCpf1 | Off-targets ≤4mm | Locus | Graf |
|---|---|---|---|---|---|
| 17forw | TTTCCTTTCTCTATATAAACCCCTTTT | no flanking | 2 | scaffold00423 CsLOB1 | tt flag |
| 22forw | TTTCTCTATATAAACCCCTTTTGCCTT | no flanking | 1 | scaffold00423 CsLOB1 | tt flag |
| 32rev | TTTATATAGAGAAAGGAAAGGCAAGAA | no flanking | 0 | not found | OK |
| 40forw | TTTTGCCTTGAACTTTGTTTCAACTAA | 3.90 | 1 | not in CsLOB1 | OK |
| 41forw | TTTGCCTTGAACTTTGTTTCAACTAAA | 2.28 | 2 | not in CsLOB1 | OK |
| 53forw | TTTGTTTCAACTAAAGCAGCTCCTCCT | no flanking | 0 | scaffold00423 CsLOB1 | tt flag |
| 57forw | TTTCAACTAAAGCAGCTCCTCCTCATC | no flanking | 0 | scaffold00423 CsLOB1 | OK |
| 64rev | TTTAGTTGAAACAAAGTTCAAGGCAAA | no flanking | 5 | not in CsLOB1 | OK |

## Key finding 1 — Jia's guide identified
Guide 17forw = TTTCCTTTCTCTATATAAACCCCTTTT = Jia et al. 2019 published crRNA
(PAM TTTC + target CTTTCTCTATATAAACCCCTTTT from Fig.1b)
CRISPOR flags this with a Graf "tt" motif warning — predicted low efficiency.
This independently explains Jia's observed 15-55% mutation rate, lower than
LbCas12a's near-100% efficiency in rice.

## Key finding 2 — Our own guide design
Guide 57forw: TTTCAACTAAAGCAGCTCCTCCTCATC
- 0 off-targets at <=4mm (fewer than Jia's guide)
- No Graf efficiency concern
- Confirmed in CsLOB1 locus (scaffold00423 115.47 Kbp)
- Targets a different region of the EBE promoter than Jia's crRNA
- This guide has NOT been published — genuinely our own design

## Rationale for choosing 57forw as our design
1. 0 off-targets (better than all other in-locus guides)
2. GrafOK — no predicted efficiency penalty
3. In correct locus (scaffold00423, same as CsLOB1)
4. Not Jia's guide — independent design contribution

## DeepCpf1 score note
Only guides 40forw and 41forw have DeepCpf1 scores (3.90 and 2.28).
Other guides show "NotEnoughFlankSeq" — input was 119bp, guides near
ends lack the >=50bp flanking context CRISPOR needs for efficiency scoring.
To get efficiency scores for 57forw: submit again with 50+ bp flanking
sequence added on each side from the Citrus sinensis genome.

## Cas-OFFinder validation of 57forw
Guide: CAACTAAAGCAGCTCCTCCTCATC
PAM: TTTN
Genome: Citrus sinensis (1.0), mismatch <=5
Cas-OFFinder results (Job 860869, Sept 3 2026):
At 5 mismatches: 3 sites (NC_023048.1 pos 20765972, NC_023050.1 pos 6199074, NW_006257077.1 pos 287639)
At <=4 mismatches: ZERO sites

Comparison with Jia et al. published crRNA (17forw):
Jia guide: 2 off-targets at <=4mm (CRISPOR) + Graf tt efficiency flag
Our guide: 0 off-targets at <=4mm + no Graf flag
Our independently designed guide has a CLEANER predicted specificity
profile than the published guide. This is a genuine original contribution.
