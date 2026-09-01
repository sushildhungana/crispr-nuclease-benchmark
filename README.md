# crispr-nuclease-benchmark

Replicating and contrasting the gRNA-design and off-target methodology of:

> Lee K, Zhang Y, Kleinstiver BP, et al. (2019). *Activities and specificities of
> CRISPR/Cas9 and Cas12a nucleases for targeted mutagenesis in maize.*
> Plant Biotechnology Journal 17, 362–372. doi:10.1111/pbi.12982 (Open Access, CC BY 4.0)

## Objective

Independently design Cas9 and Cas12a guides against the same maize *glossy2* (*gl2*)
targets used in the paper, run them through the same class of tools the authors used,
and compare my numbers to theirs — where they match, where they diverge, and why.

## Reference numbers to reproduce (from the paper)

| | Target 1 | Target 2 |
|---|---|---|
| Cas9 on-target (% T0 with indel) | 100% | 90.3% |
| Cas12a on-target (% T0 with indel) | 60% | 0% |
| Cas9 predicted off-targets, Cas-OFFinder (≤6 mismatches) | 19,029 | 71,253 |
| Cas12a predicted off-targets, Cas-OFFinder (≤6 mismatches) | 1,193 | 173 |
| Cas9 CIRCLE-seq candidates (empirical, in vitro) | 18 | 67 |
| Off-targets confirmed in living T1 plants | 0 | 0 |

## Tools

- **CHOPCHOP** — https://chopchop.cbu.uib.no (gRNA design, on-target scoring, built-in off-target scan)
- **CRISPOR** — http://crispor.gi.ucsc.edu (design + MIT/CFD off-target scoring)
- **Cas-OFFinder** — http://www.rgenome.net/cas-offinder/ (the exact tool the paper used for genome-wide off-target prediction)

Gene: **GLOSSY2**, legacy ID `GRMZM2G098239` (B73 AGPv3/v4 — what the paper searched
against), current ID `Zm00001d002353` (B73 RefGen_v5 — what CHOPCHOP/CRISPOR will
default to today). If your off-target counts don't match the paper's, this genome-build
difference is the first thing to check.

## Workflow

### 1. Setup (~20 min)
- [ ] Bookmark the three tools above
- [ ] Skim `targets/maize_gl2_targets.fasta` — these are the paper's actual guide
      sequences, cross-checked against three separate mentions in the text

### 2. Design replication (~90 min)
- [ ] Search CHOPCHOP for `Zm00001d002353` (or paste `Target1_full_context...` /
      `Target2_full_context...` sequences directly) with the B73 genome selected
- [ ] Generate your own top-ranked Cas9 (NGG) and Cas12a (TTTV) guides at both loci
- [ ] Cross-reference CRISPOR's efficiency + specificity scores for the same guides
- [ ] Compare your top picks against the paper's actual `gRNA1/2` and `crRNA1/2` —
      did the tools converge on the same guides the authors used?

### 3. Off-target replication (~60 min)
- [ ] Run Cas-OFFinder on your guides (and the paper's own guides) against the maize
      genome, ≤6 mismatches, same setting the paper used
- [ ] Try to approximate: ~19,029 / ~1,193 (Target 1), ~71,253 / ~173 (Target 2)
- [ ] Note any divergence — genome build, mismatch threshold, or tool version are the
      usual suspects

### 4. Contrast write-up (~60 min)
- [ ] Fill in `results/comparison_table.md` — your guides vs. theirs, your off-target
      counts vs. theirs, what matched, what didn't, and your best explanation why

## Repo structure

```
crispr-nuclease-benchmark/
├── README.md
├── targets/
│   └── maize_gl2_targets.fasta
├── design/            <- CHOPCHOP / CRISPOR exports go here
├── offtarget/         <- Cas-OFFinder exports go here
└── results/
    └── comparison_table.md   <- fill in tomorrow, not pre-written
```
