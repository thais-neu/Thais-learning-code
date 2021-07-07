Use dDocent pipeline on Discovery

> Note: Here we are assuming that the barcoding and adapters are already stripped off for this specific practice dataset (same dataset used in the "NCBI data retrieval post). Since it was a ddRAD library prep, we should be left with the DNA sequence of interest and the overhang sequence corresponding to the recognition sequence where the enzymes attached. In this study, the two enzymes they used were EcoRI and MspI. “EcoRI is a restriction enzyme that creates 4 nucleotide sticky ends with 5' end overhangs of AATT. The nucleic acid recognition sequence where the enzyme cuts is G/AATTC, which has a palindromic, complementary sequence of CTTAA/G. The / in the sequence indicates which phosphodiester bond the enzyme will break in the DNA molecule.” MspI overhang sequence is C/CGG and the palindromic complementary sequence is GGC/C. 

> Note: Actually, rather than assuming, this can be checked by looking at (some of) the sequence files. All the random sra_1.fastq files that I looked at start with the overhang sequence AATTC - meaning they correspond to the forward reads, cut with EcoRI - and the sra_2.fastq files start with the overhang CGG - meaning they correspond to the reverse reads, cut with MspI.

> Note: In the Lotterhos lab module, ddocent-2.7.8 was added to the conda environment “lotterhos-py38” within the anaconda3/L2020-03 module.

## The files need to be in the following format: PopID_filename.F.fq.gz and PopID_filename.R.fq.gz

# 1) Rename files to comply with the above naming convention required:

> My fastq files came out of NCBI in the following format: SRRxxxxxxxx.sra_1.fastq (forward reads) and SRRxxxxxxxx.sra_2.fastq (reverse reads).

> They need to be in the following format: PopID_SRRxxxxxxxx.F.fq.gz (forward reads) and PopID_SRRxxxxxxxx.R.fq.gz (reverse reads).

> Note: We do not have information on the Pop ID in this study so we will call them all Pop1. 

> Note: gz means the file is compressed.

You will need: request resources in Discovery and a code to batch-rename the files.

## Request Discovery resources

In terminal, login to Discovery and navigate to where your working fastq files are:

`cd /scratch/tbittar/`

Type one fo the the following codes to get access to resources: 

`srun -p debug -N1 --pty /bin/bash`

> This will give you 20 mins to work on a shared partition. Retype when needed. Use this to check your code is working on 1-2 files.

`srun -p lotterhos -N 1 --pty /bin/bash`

> This will give you 24h to work on the lotterhos partition (lotterhos users only). Use this if 20 min is not enough to rename and compress all files. 

*To use Lotterhos Lab resources, you need to ask Dr. L to be added as a user ahead of time. To check if you are a user type `groups $USER`. If you are successfully added to the group, you will see:

tbittar : users lotterhos 

## Script to batch-rename files (I could only come up with a two-step code (two for-loops) to batch-rename the files):

**1st step** - this will replace the extension .sra_1.fastq with an .F and the extension .sra_2.fastq with an .R in all files in the folder:

for f in *.sra_1.fastq; do 

mv "$f" "${f%.sra_1.fastq}.F"; 

done

for f in *.sra_2.fastq; do 

mv "$f" "${f%.sra_2.fastq}.R"; 

done

**2nd step** - this will add Pop1_ as a prefix to all file names; compress the file with gzip; and add the .fq as the extension in all files in the folder:

prefix=Pop1_

for name in SRR*; do

gzip < "$name" > "$prefix$name.fq.gz" 

done 

**Tip:** Keep the scratch folder open in Globus and use Refresh List to double-check that the file names are changing as expected and that the new files are smaller in size (because they are now compressed).

# 2) Load the module where dDocent is nested.

Login to Discovery and request resources using the lotterhos partition.

`srun -p lotterhos -N 1 --pty /bin/bash`

Load the module where Ddocent is nested and activate dDocent:

`module load lotterhos/2020-08-24`

`source activate ddocent2`

Start dDocent, type:

`dDocent`

**The interactive part:**

Confirm # of individuals - yes/no

Choose # of processors - 3

Limit memory use - 1

Quality trim? yes

Perform assembly? yes

What type of assembly? PE

New c-parameter? no

Map reads? yes

Adjust -A -B -O; new parameters? no

Use FreeBayes to call SNPs? yes

Enter email address to get a message when done - will this work on Discovery?

If all works, you get a plot of Unique Sequences vs Coverage; based on this graph, choose the data cutoff.

You get another plot of Unique Sequences vs Individuals, choose the data cutoff.

From here on, the pipeline should run on its own.

# Attempts at running the pipeline.

---
## 16-Sept-2020

**Attempt #1 - all settings as listed above under "4.2 the interactive part":**

Running dDocent on all 56 files (28 individuals) for which I have fastq files.
* cutoff chosen for unique seq vs coverage = 6
* cutoff chosen for unique seq vs #individuals = 6

ERROR: EXCEEDED JOB MEMORY LIMIT AT BWA TO MAP READS. 
 
**Attempt #2 - same as above, but changed "Limit memory use" to 10Gb:**

SAME ERROR: EXCEEDED JOB MEMORY LIMIT AT BWA TO MAP READS. 

**Attempt #3 - same as above, but changed "Limit memory use" to 0GB (based on dDocent user guide):**

SAME ERROR: EXCEEDED JOB MEMORY LIMIT AT BWA TO MAP READS. 

---
## 17-Sept-2020

Meeting with Katie - use seff to check memory usage and run less files to test the pipeline.

Running `seff JOBID` on yesterday's jobs tells me the job is using ~2Gb of memory.

**Attempt #4, same settings as above, except:**
* 10 files/5 individuals
* Choose # of processors - 5
* Limit memory use - 10Gb
* cutoff chosen for unique seq vs coverage = 6
* cutoff chosen for unique seq vs #individuals = 3


SAME ERROR: EXCEEDED JOB MEMORY LIMIT AT BWA TO MAP READS. 
Seff: tells me the job is using ~2Gb of memory.

**Attempt #5, same settings as above, except:**
* 4 files/2 individuals
* Choose # of processors - 3
* Limit memory use - 0Gb
* cutoff chosen for unique seq vs coverage = 6
* cutoff chosen for unique seq vs #individuals = 2

THIS WORKS and the pipeline runs all the way.
Seff: tells me memory utilized was 0Gb

---
## 18-Sept-2020

From here on, I'm incrementally increasing the number of files/individuals to see if/when I get the memory error.

**Attempt #6, same settings as above, except:**
* 8 files/4 individuals
* Choose # of processors - 3
* Limit memory use - 0Gb
* cutoff chosen for unique seq vs coverage = 6
* cutoff chosen for unique seq vs #individuals = 3

THIS WORKS and the pipeline runs all the way.
Seff: tells me memory utilized was 0Gb

**Attempt #7, same settings as above, except:**
* 16 files/8 individuals
* Choose # of processors - 3
* Limit memory use - 0Gb
* cutoff chosen for unique seq vs coverage = 6
* cutoff chosen for unique seq vs #individuals = 5

THIS WORKS and the pipeline runs all the way.
Seff: tells me memory utilized was 0Gb

**Attempt #8, same settings as above, except:**
* 32 files/16 individuals
* Choose # of processors - 3
* Limit memory use - 0Gb
* cutoff chosen for unique seq vs coverage = 6
* cutoff chosen for unique seq vs #individuals = 5

ERROR: EXCEEDED JOB MEMORY LIMIT AT BWA TO MAP READS.
Seff: tells me memory utilized was 2.17Gb

---
## 21-Sept-2020

**Attempt #9, same settings as above, except:**
* 20 files/10 individuals
* Choose # of processors - 3
* Limit memory use - 0Gb
* cutoff chosen for unique seq vs coverage = 6
* cutoff chosen for unique seq vs #individuals = 5

ERROR: EXCEEDED JOB MEMORY LIMIT AT BWA TO MAP READS.
Seff: tells me memory utilized was 1.97Gb out of 1.95Gb

**Attempt #10, same settings as above, except:**
* 18 files/9 individuals
* Choose # of processors - 3
* Limit memory use - 0Gb
* cutoff chosen for unique seq vs coverage = 6
* cutoff chosen for unique seq vs #individuals = 5

THIS WORKS and the pipeline runs all the way.
Seff: tells me memory utilized was 0Gb.

---

**Attempts 5-7 worked and the pipeline ran all the way through!!!!!!!!!!!!! :) - but with limited number of files**

Based on the 10 attempts listed above, it looks like the memory available in partition can handle 18 files (9 individuals) 
* how much data does that correspond to?

**There is a 2Gb memory limit in the partition, - or maybe it is a glitch and we should be able to request more memory?**

**Next steps: create a settings file for the interactive part of the pipeline and try to submit as a job so more memory is available.**

---
