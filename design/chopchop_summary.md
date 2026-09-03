# CHOPCHOP Results Summary — Zm00001d002353 (gl2 / GLOSSY2)
Tool: CHOPCHOP v3 (chopchop.cbu.uib.no)
Genome: Zea mays B73 AGPv4
CRISPR system: SpCas9 / NGG PAM
Mode: knock-out
Total guides generated: 241

## Top 5 CHOPCHOP-ranked guides
Rank 1:  TTCAAGCTGCACTACCTGCG  eff=57.38  MM0=0 MM1=0 MM2=0 MM3=0
Rank 2:  TGGCCAACGAGATGAAGGTC  eff=57.24  MM0=0 MM1=0 MM2=0 MM3=0
Rank 3:  TGCGCGGGGTGTACTACTAC  eff=55.17  MM0=0 MM1=0 MM2=0 MM3=0
Rank 4:  CATGTCCACGAGCGTCAGGT  eff=54.76  MM0=0 MM1=0 MM2=0 MM3=0
Rank 5:  ATGCCGTACTCCACGTAGAC  eff=44.81  MM0=0 MM1=0 MM2=0 MM3=0

## Paper's guides in CHOPCHOP output
gRNA1 (ACAGATCACAAACTTCAAATG): NOT FOUND in 241 guides
  Reason: SNP between AGPv3 (paper) and AGPv4 (CHOPCHOP) eliminates NGG PAM
  context at this exact position. Guide is valid in AGPv3, invalid in AGPv4.

gRNA2 (AAGTGGGCGCAGATCCTGAG): Rank 135/241, efficiency 68.92
  AGPv4 version: AAGTGGGCGCAGATCCTCAGCGG (1-nt SNP: G->C at position 17)
  Paper version: AAGTGGGCGCAGATCCTGAGCGG
  Despite SNP, this is the same locus — different base in the reference genome.

## Critical finding
CHOPCHOP's #1 ranked guide (TTCAAGCTGCACTACCTGCG) was never used by the paper.
The paper's guides were not selected by efficiency ranking but by the experimental
constraint of overlapping PAM sites enabling direct Cas9/Cas12a comparison.
Guide RNA design is genome-build-dependent — a reproducibility concern.
