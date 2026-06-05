# Population Genomics Pipelines

A non-exhaustive collection of useful popgen pipelines for various data types.

---

## Pipelines

For lcWGS data intended for ANGSD, BAMs should be overlap-clipped (definitely) and indel-realigned (perferred).

| Pipeline | Data Type | lcWGS Suitable | Indel Realignment | Overlap Clipping | Output | Notes |
|---|---|---|---|---|---|---|
| [snpArcher](https://snparcher.readthedocs.io/en/latest/index.html) | High-coverage, non-model organisms | no | no | no (GATK handles internally) | BAM + VCF | GATK best practices; not ANGSD-ready |
| [grenepipe](https://github.com/moiexpositoalonsolab/grenepipe/wiki) | General WGS | no | no | yes | VCF + BAMs | Not suitable for lcWGS to ANGSD |
| [PopGLen](https://github.com/zjnolen/PopGLen) | lcWGS, historical DNA | yes | yes (GATK IndelRealigner) | yes (BamUtil) | ANGSD-ready BAMs | Flexible filtering |
| [mega-non-model-wgs-snakeflow](https://github.com/eriqande/mega-non-model-wgs-snakeflow) | lcWGS | yes | yes | yes | ANGSD-ready BAMs | — |
| [WGSfqs-to-genolikelihoods](https://github.com/letimm/WGSfqs-to-genolikelihoods) | lcWGS | yes | no | yes | ANGSD-ready BAMs + genotype likelihoods | SLURM HPC only; goes through ANGSD to produce beagle files |

### Analysis pipelines

| Pipeline | Input | lcWGS Suitable  | Notes |
| [locopipe](https://github.com/locopipe) | mapped and filtered bams | yes | ANGSD for GL, PCA, and FST. Ohana for admixture; local PCA. useful for hierarchical structure analyses because re-estimates GLs using group-specific depth and missing data filters automatically for each different grouping of individuals |


---

## Notes & Considerations

- **snpArcher vs grenepipe:** grenepipe may offer more flexibility for some use cases; snpArcher follows GATK best practices but doesn't produce ANGSD-ready BAMs.
- **PopGLen** is a strong choice for lcWGS or historical DNA with flexible filtering and full ANGSD-ready output.

---

## pixy Alternative

- [clam](https://cademirch.github.io/clam/) — alternative to pixy for computing pi, dxy, and Fst
