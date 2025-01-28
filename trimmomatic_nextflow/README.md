

```bash

nextflow run trimmomatic.nf \
  --input_dir '241129_NOA015_PanTrop_WGS,241129_NOA016_PanTrop_WGS' \
  --outdir trimmed_trimmomatic \
  --adapter_file NexteraPE_NT.fa -profile trimmomatic

```
