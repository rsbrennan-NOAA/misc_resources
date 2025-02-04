# Read groups

In sam/bam files, we have what are known as read groups. You can read the [GATK definition](https://gatk.broadinstitute.org/hc/en-us/articles/360035890671-Read-groups) of a read group here. 

In the most simple sense, a read group is meta data for your reads. That is, it identifies groups of reads. Here's an example:

```
@RG	ID:Sample1_Lane1_lib1	SM:Sample1	PU:FLOWCELL_lane1_Sample1	PL:ILLUMINA	LB:lib-1

```

The minimum requirements are:
- `ID`: ID for the group of reads (lane ID+sample+library, for example). This should be unique to the set of reads (i.e., a combination of other parameters)
- `SM`: the name of the sample
- `LB`: the name of the library (more about this below)
- `PL`: the sequencing platform
- `PU`: Platform Unit:  {FLOWCELL_BARCODE}.{LANE}.{SAMPLE_BARCODE}

We can set these using the `-R` option in `bwa mem`


#### What to use for LB? 

LB is primarily used for marking duplicates. Generally, we're only going to mark duplicates within a single sample and have separate bams/sample. We're most concerned about PCR duplicates, which arise during library prep. What this means is that we want to consider duplicates for one sample and one library. So we might have a multiplexed library `lib-1` for `Sample-1` and `Sample-2`. These samples could have been sequenced across two different lanes- `Lane-1` and `lane-2`. We would want to identify duplicates for `Sample-1` across both lanes, because they are the product of the same library process. But we would consider the two samples separately. 

So our read groups would look like:

```
@RG	ID:Sample1_Lane1	SM:Sample1	PU:FLOWCELL_lane1_Sample1	PL:ILLUMINA	LB:lib-1

@RG	ID:Sample1_Lane2	SM:Sample1	PU:FLOWCELL_lane2_Sample1	PL:ILLUMINA	LB:lib-1

@RG	ID:Sample2_Lane1	SM:Sample2	PU:FLOWCELL_lane1_Sample2	PL:ILLUMINA	LB:lib-1

@RG	ID:Sample2_Lane2	SM:Sample2	PU:FLOWCELL_lane2_Sample2	PL:ILLUMINA	LB:lib-1

```

If our libraries are all separated by sample, we can also just call `LB` the same as `SM`. In practice this will be treated the same for most (but not all!) things. For example, if you use [BSQR](https://gatk.broadinstitute.org/hc/en-us/articles/360035890531-Base-Quality-Score-Recalibration-BQSR) you should make sure to use library at the true level and not sample level. 

Because our bams are typically separated by sample until snp calling, in practice either approach should work for most cases. 


## useful references:

https://gatk.broadinstitute.org/hc/en-us/articles/360035890671-Read-groups

https://therkildsen-lab.github.io/user-guide/docs/gatk/#2-mapping-data-to-a-reference-genome

https://eriqande.github.io/eca-bioinf-handbook/alignment-of-sequence-data-to-a-reference-genome-and-associated-steps.html#read-groups
