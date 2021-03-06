# Fastlnc: Preprocessing Workflow

Workflow for identifying lincRNA data to use for training the machine learning model.

# Installation

Install Nextflow in the local directory (requires Java 8)

```
make install
```

Download reference data

```
make ref
```

Build `preprocessing` Docker container

```
cd ../containers
make test VAR=preprocessing
```

# Run

```
make run
```

# Data Reqiurements

- reference genome .fasta (e.g. `Gallus_gallus-5.0_genomic.fasta`)

- reference genome annotations .gff (e.g. `Gallus_gallus-5.0_genomic_cleaned.gff`)

- reference proteome .fasta (e.g. `uniprot-proteome_gallus_gallus_AUP000000539.fasta`)

- SRA identifier for research sample(s) (e.g. `sra.tsv`)

# Workflow Description

Processing steps that will be performed by the Nextflow pipeline

## Setup Steps

- create HiSat2 indexes for reference genome fasta

- create BLAST databases & indexes for proteome fasta

## Analysis Steps

- align SRA reads with `hisat2`

- sort aligned reads with `sambamba`

- assemble transcripts with `stringtie`

- filter low coverage transcripts

- extract fasta sequences for transcripts with `gffread`

- filter fasta transcripts for sequences >200bp

- query transcript fasta sequences against proteome database with `blastx` to identify protein coding transcripts

-
