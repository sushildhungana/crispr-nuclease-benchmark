# Citrus Extension — CsLOB1 EBE Targeting (Jia et al. 2019)
Reference: Jia H, Orbovic V, Wang N. (2019). CRISPR-LbCas12a-mediated 
modification of citrus. Plant Biotechnology Journal 17, 1928-1937.
doi:10.1111/pbi.13109 (Open Access, CC BY 4.0)

## Why this is the bridge to HLB

CsLOB1 is the canker susceptibility gene in citrus. It is induced by 
pathogenicity factor PthA4 from Xanthomonas citri subsp. citri (Xcc) 
via binding to EBE_PthA4 in the CsLOB1 promoter. Disrupting this EBE 
by CRISPR makes the plant resistant to canker.

The same host (Citrus sinensis) faces HLB (Huanglongbing disease) caused 
by Candidatus Liberibacter asiaticus (CLas). The CsNPR3 gene (negative 
regulator of systemic acquired resistance) has been targeted by CRISPR/Cas9 
in 2024 specifically for HLB tolerance. The Jia et al. 2019 paper proves 
LbCas12a is functional in citrus — making it a platform for future 
HLB-focused Cas12a work.

## The crRNA — why ONE guide targeting TWO alleles matters

Duncan grapefruit has two types of CsLOBP:
- Type I CsLOBP: from sweet orange (Citrus sinensis)  
- Type II CsLOBP: from pummelo (Citrus maxima)

SpCas9 could NOT target both alleles with a single sgRNA — SNPs between 
the two types fall within the sgRNA targeting region, making design 
infeasible (Jia et al. 2016).

LbCas12a's TTTV PAM commonly occurs in promoter regions and 5'/3' UTRs. 
Jia et al. found a single crRNA targeting a CONSERVED region of both 
CsLOBP types, overcoming the SNP problem. This is a demonstration of 
Cas12a's unique PAM expanding the targetable genomic space.

## Guide sequence
Gene: CsLOB1 promoter EBE_PthA4
System: LbCas12a
PAM: TTTC (TTTV class)
crRNA target (23 nt): CTTTCTCTATATAAACCCCTTTT
Full PAM+target: TTTCCTTTCTCTATATAAACCCCTTTT

Source: Figure 1b + Figure 3, Jia et al. 2019
Confirmed by Methods section primer: crRNA-lobp-P 
(5'-phosphorylated-ATCTTTCTCTATATAAACCCCTTTTGAATTTCCCCG...)

## Paper's off-target analysis
Tool: Cas-OFFinder (same tool we used for maize)
Genome: Sweet orange
Mismatch: 2, RNA bulge: 1
Result: All potential off-targets at <=2 mismatches located AT the 
on-target site — effectively zero real off-targets.

## Our extended analysis
Tool: Cas-OFFinder (web)
Genome: Citrus sinensis (1.0)
PAM: TTTN
Mismatch: 4 (deeper than paper's 2mm analysis)
Guide: CTTTCTCTATATAAACCCCTTTT

Results (Cas-OFFinder run Sept 3 2026, Job ID 860866):
At 0 mismatches: 1 site — NC_023052.1 pos 28359397 (on-target site itself)
At 4 mismatches: 3 sites total
  - NC_023047.1 pos 11847442 (+strand, 4mm)
  - NC_023048.1 pos 23727083 (-strand, 4mm)
  - NW_006257207.1 pos 84543 (+strand, 4mm, unplaced scaffold)

Total off-target candidates at <=4mm: 3
Paper reported zero off-targets at <=2mm — CONFIRMED.
Our deeper <=4mm search finds only 3 candidates — consistent with
paper's conclusion of highly specific guide.

Cross-system comparison:
  Cas9 gRNA1 (maize, <=6mm):      19,029 predicted sites (paper)
  Cas12a crRNA1 (maize, <=6mm):    1,193 predicted sites (paper)
  Cas12a crRNA (citrus, <=4mm):        3 predicted sites (this run)

Citrus genome is ~300 Mb vs maize ~2,300 Mb — ~8x smaller,
far less repetitive. Fewer near-matches exist by genome size alone.
But 3 sites at <=4mm is still remarkably clean for any CRISPR guide.

## Editing outcomes (from paper)
7 transgenic 35S-LbCas12a Duncan plants generated
3 of 7 showed EBE modifications: #D35s1 (15%), #D35s4 (55%), #D35s7 (15%)
Average mutation rate among successful lines: 28.3%
All mutations were DELETIONS (consistent with Cas12a staggered cuts)
Best line (#D35s4): 100% Type II EBE-CsLOBP mutated, RESISTANT to 
XccDeltapthA4:dCsLOB1.4 infection

## Parallel to Lee et al. 2019 (our main paper)
Both papers: same year, same journal (Plant Biotechnology Journal), same Cas12a
Lee et al: maize, coding gene (gl2), proof-of-concept efficiency comparison
Jia et al: citrus, promoter EBE, disease-resistance application
Key shared finding: all mutations are DELETIONS with Cas12a
Key shared finding: no off-target mutations observed in either study
