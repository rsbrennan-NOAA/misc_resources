# Population Genomics Pipelines

A non-exhaustive collection of useful popgen pipelines for various data types.

---

## Pipelines

| Pipeline | Data Type | lcWGS Suitable | Indel Realignment | Overlap Clipping | Output | Notes |
|---|---|---|---|---|---|---|
| [snpArcher](https://snparcher.github.io/) | High-coverage, non-model organisms | no | no | no (GATK handles internally) | BAM + VCF | GATK best practices; not ANGSD-ready |
| [grenepipe](https://github.com/moiexpositoalonsolab/grenepipe/wiki) | General WGS | no | no | yes | VCF + BAMs | Not suitable for lcWGS to ANGSD |
| [PopGLen](https://zjnolen.github.io/PopGLen/latest/) | lcWGS, historical DNA | yes | yes | yes (BamUtil) | ANGSD-ready BAMs | Flexible filtering |
| [mega-non-model-wgs-snakeflow](https://github.com/eriqande/mega-non-model-wgs-snakeflow) | lcWGS | yes | yes | yes | ANGSD-ready BAMs | — |
| [WGSfqs-to-genolikelihoods](https://github.com/letimm/WGSfqs-to-genolikelihoods) | lcWGS | yes | no | yes | ANGSD-ready BAMs + genotype likelihoods | SLURM HPC only; No indel realignment |

### Analysis pipelines

| Pipeline | Input | lcWGS Suitable  | Notes |
|---|---|---|---|
| [locopipe](https://github.com/sudmantlab/loco-pipe/blob/main/manual/README.md) | mapped and filtered bams | yes | ANGSD for GL. Runs PCA, FST, admixture, diversity. useful for hierarchical structure analyses because re-estimates GLs using group-specific depth and missing data filters automatically for each different grouping of individuals |
| [PopGLen](https://zjnolen.github.io/PopGLen/latest/) | raw reads or mapped and filtered bams | yes | angsd based. ROH, Fst, diversity, PCA, admixture, etc.  |


---

## General recommendations

- High coverage data:
    - grenepipe may offer more flexibility, can choose what method at many steps: trimming, mapping, BaseRecalibrator;
    - snpArcher uses bwamem and GATK best practices and scatter-by-intervals approach (but can choose bcftools, and others). Also some filtering options.
- Low coverage data:
    - For lcWGS data intended for ANGSD, BAMs should be overlap-clipped (definitely) and indel-realigned (preferred).
    - PopGLen is a good choice for lcWGS or historical DNA bc very flexible filtering and  ANGSD-ready output.
    - mega-non-model-wgs-snakeflow should work well to get angsd ready bams
    - WGSfqs-to-genolikelihoods gets angsd ready bams, but no indel realignment. Can use -baq 1 flag to to deal with indel problems [see here](https://doi.org/10.1093/bioinformatics/btr076)
- Pop gen analysis:
    - locopipe useful for core pop gene analyses regardless of low or high coverage.
    - PopGLen also does a variety of popgen analyses regardless of low or high cov.
    - These are both focused on low coverage data. 

---

## pixy Alternative

- [clam](https://cademirch.github.io/clam/) — alternative to pixy for computing pi, dxy, and Fst
