# CRISPOR Results — Target 2, Cas9 gRNA2
Tool: CRISPOR v5.2 (crispor.gi.ucsc.edu)
Genome: Zea mays (faZmB735)
Input: TTTCAACAAGTGGGCGCAGATCCTGAGCGG (30bp)
PAM: NGG / SpCas9

## Result
Guide: AAGTGGGCGCAGATCCTGAG CGG (position 28, forward strand)
Warning: Query sequence not found in faZmB735 genome (build difference from paper)

## Scores
MIT Specificity Score: 24    (RISKY — below 50 threshold)
CFD Specificity Score: 85    
Doench 2016 efficiency: --   (insufficient flanking sequence, need >100bp input)
Moreno-Mateos: --            (same reason)
Doench RuleSet3: --          (same reason)

## Off-target profile (<=4 mismatches)
Pattern: 0-1-14-363-3702 (0mm, 1mm, 2mm, 3mm, 4mm)
Total: 4,080 off-target sites
Color classification: YELLOW (lower specificity — caution)

## Key observation
MIT score 24 independently confirms Cas-OFFinder's 71,253 predicted sites.
Two completely different algorithms, same conclusion: gRNA2 is less specific.
Low MIT score is a WARNING, not a verdict — paper found zero confirmed
off-target mutations in living plants despite this score.
