# <h1 align="center">Cellranger-atac convert bcl file to fastq file</h1>

# Interpretation of bcl to fastq algorithm
[My previous notes](https://github.com/TingtingSsl2/scRNA-seq_LearningPage/blob/main/03_Convert%20bcl%20to%20fastq.md)

# Practice: convert bcl to fastq
[10X genomics](https://support.10xgenomics.com/single-cell-atac/software/pipelines/latest/using/mkfastq)

***
**Guildlines to download sample files from 10X genomics** 
- Download the tiny-bcl tar file.
- Untar the tiny-bcl tar file in a convenient location. This will create a new tiny-bcl subdirectory.
- Download the simple CSV layout file: cellranger-atac-tiny-bcl-simple-1.0.0.csv.
- Download the Illumina® Experiment Manager sample sheet: cellranger-atac-tiny-bcl-samplesheet-1.0.0.csv.
***

**1. Login to BWH supercomputing system ERISONE, which has cellranger-atac installed under request. Locate to the working dir.** 
```
cd /data/bioinformatics/projects/scATAC
```

**2. Load modules required for scATAC-seq analysis.**
```
module load cellranger-atac/2.0.0
module load bcl2fastq2/default # this version works
```

**3. Run mkfastq on sample file.**
```
cellranger-atac mkfastq \
--id=tiny-bcl \
--run=/data/bioinformatics/projects/scATAC/cellranger-atac-tiny-bcl-1.0.0 \
--csv=cellranger-atac-tiny-bcl-simple-1.0.0.csv
```

**4. Check output file.**

To "/outs" folder.
```
cd /data/bioinformatics/projects/scATAC/tiny-bcl/outs/
```
The converted fastq file could be found in a file named by gel code, e.g. HJN3KBCX2. Note that the undetermined fastq file are stored in fastq_path folder.
```
[tz949@eris1n2 outs]$ ls -hl fastq_path/
total 520M
drwxrwx---. 3 tz949 tz949 4.0K Jun 23 10:36 HJN3KBCX2
drwxrwx---. 3 tz949 tz949 4.0K Jun 23 10:36 Reports
drwxrwx---. 2 tz949 tz949 4.0K Jun 23 13:11 Stats
-rw-rw----. 1 tz949 tz949  40M Jun 23 10:36 Undetermined_S0_L001_I1_001.fastq.gz
-rw-rw----. 1 tz949 tz949 150M Jun 23 10:36 Undetermined_S0_L001_R1_001.fastq.gz
-rw-rw----. 1 tz949 tz949  76M Jun 23 10:36 Undetermined_S0_L001_R2_001.fastq.gz
-rw-rw----. 1 tz949 tz949 151M Jun 23 10:36 Undetermined_S0_L001_R3_001.fastq.gz
```
Look into fastq file folder.
```
[tz949@eris1n2 fastq_path]$ tree HJN3KBCX2/
HJN3KBCX2/
└── test_sample
    ├── test_sample_S1_L001_I1_001.fastq.gz
    ├── test_sample_S1_L001_R1_001.fastq.gz
    ├── test_sample_S1_L001_R2_001.fastq.gz
    └── test_sample_S1_L001_R3_001.fastq.gz

1 directory, 4 files
```
