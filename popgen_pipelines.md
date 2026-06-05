# Population Genomics Pipelines

A non-exhaustive collection of useful pipelines for various data types.

---

## Pipelines

For lcWGS data intended for **ANGSD**, BAMs should be indel-realigned and overlap-clipped.

| Pipeline | Data Type | Indel Realignment | Overlap Clipping | Output | Notes |
|---|---|---|---|---|---|
| [snpArcher](https://onlinelibrary.wiley.com/doi/full/10.1111/mec.17362) | High-coverage, non-model organisms | no | no (GATK handles internally) | VCF | GATK best practices; not ANGSD-ready |
| [grenepipe](https://academic.oup.com/mbe/article/42/12/msaf282/8340576) | General WGS | no | yes | VCF + BAMs | Not suitable for lcWGS to ANGSD |
| [PopGLen](https://github.com/zjnolen/PopGLen) | lcWGS, historical DNA | yes (GATK IndelRealigner) | yes (BamUtil) | ANGSD-ready BAMs | Flexible filtering |
| [locopipe](https://github.com/locopipe) | lcWGS | — | — | BAMs | Good reference implementation |
| [mega-non-model-wgs-snakeflow](https://github.com/eriqande/mega-non-model-wgs-snakeflow) | lcWGS | yes | yes | ANGSD-ready BAMs | — |

---

## Notes & Considerations

- **snpArcher vs grenepipe:** grenepipe may offer more flexibility for some use cases; snpArcher stops at VCF and follows GATK best practices but doesn't produce ANGSD-ready BAMs.
- **PopGLen** is a strong choice for lcWGS or historical DNA with flexible filtering and full ANGSD-ready output.

---

## pixy Alternative

- [clam](https://cademirch.github.io/clam/) — alternative to pixy for computing pi, dxy, and Fst
