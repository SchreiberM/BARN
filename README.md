# BARN

### Analysis of the BARN data
The project consists of six different barley tissues across 200 genotypes. For each tissue type the following pipeline is run individually.

To use the snakemake pipeline a few files have to be prepared.
1. config.yaml
2. samples.csv
3. reference folder:  
 genome fasta file  
 transcriptome fasta file  
 coordinates for transcriptome on genome  
 adapter.fasta file for trimming  
 coordinates for spliting the genome for parallel freebayes run

Following files/documents are already prepared:
1. snakemake
2. the conda environment folder (envs)


## Running snakemake
Used the barley (_Hordeum vulgare_) Barke genome in the split chromosome version. Chromosomes 1-7 were split at centromere location, resulting in 14 "chromosomes" plus the unassigned chromosome.

Star mapping and index building needed at least 48Gb.
Salmon mapping in decoy mode needed 56Gb for indexing and each individual sample takes around 31Gb of memory.

Snakemake was run using the follwoing parameters:
```
snakemake -j --cores=16 --use-conda
```

### DAG strcuture from snakemake for two example input files

![DAG snakemake output](https://github.com/SchreiberM/BARN/blob/master/Pipeline/rulegraph.svg)

## Folder structure

```
├── README.md
├── LICENSE.md
├── workflow
├    ├── report
├    ├── results
├    ├    ├── trimmedReads
├    ├        ├ unpairedReads
├    ├    ├── star
├    ├        ├── firstPass
├    ├        ├── secondPass
├    ├    ├── picard
├    ├    ├── salmon
├    ├    ├── freebayes
├    ├    ├── rseqc
├    ├        ├── bam_stats
├    ├        ├── junction_annotation
├    ├        ├── geneBody_coverage   
├    ├── logs
├    ├── envs
├    ├── indeces
├    ├    ├── genome
├    ├    ├── transcriptome
├    ├── references
├        ├── genome
├        ├── transcriptome
├        ├── annotation
├        ├── adapter
├── config
├    ├── config.yaml
├    ├── samples.csv
├── Snakefile
```


