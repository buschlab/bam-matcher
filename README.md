# BAM-match #

A tool for determining whether two BAM files were sequenced from the same sample or patient. 

## Installation ##

```
cd /directory/path/where/bam-matcher/is/to/be/installed/
git clone https://bitbucket.org/sacgf/bam-matcher.git
```

Either include the path to BAM-matcher to the environment variable PATH, or move ```bam-matcher.py```, ```bam-matcher.conf``` and ```bam_matcher_html_template``` to a directory that is in the PATH already.


## Dependencies ##

**Python** 

(version 2.7)

**Python libraries**

* PyVCF
* HTSeq
* ConfigParser
* Cheetah

**Variant Callers**

(Require at least one)

* GATK (requires Java)
* VarScan2 (requires Java and Samtools)
* Freebayes

## Configuration ##

BAM-matcher requires a configuration file. If the default configuration file is missing, a template can be generated by the ```--generate-config (-G)``` function. 

```
BAM-matcher.py --generate-config path_to_file_to_be_generated
```


The configuration file contains these sections:

```
[VariantCallers]
# file paths to variant callers and other binaries
GATK:      GenomeAnalysisTK.jar
freebayes: freebayes
samtools:  samtools
varscan:   VarScan.jar
java:      java

[ScriptOptions]
DP_threshold:    15
filter_VCF:      False
number_of_SNPs:  1500
# enable --targets option for Freebayes, faster but more prone to Freebayes errors
# set to False will use --region, each variant is called separately
fast_freebayes: True
VCF_file: variants_noX.vcf

[VariantCallerParameters]
# GATK memory usage in GB
GATK_MEM: 4
# GATK threads (-nt)
GATK_nt:  1
# VarScan memory usage in GB
VARSCAN_MEM: 4

[GenomeReference]
# default reference fasta file
REFERENCE: hg19.fasta

# Reference fasta file, with no chr in chromosome name (e.g. Broad19.fasta)
REF_noChr: Broad19.fasta

# Reference fasta file with 'chr' in chromosome names
REF_wChr:  genome.fa

[BatchOperations]
CACHE_DIR:  cache_dir

[Miscellaneous]
```

Most configuration settings can also be overridden at run time.

**[VariantCallers]**

Paths to variant callers and their required components (Java, Samtools)

**[ScriptOptions]**

Settings for BAM-matcher comparison.

* **DP_threshold**: the minimum read depth required for both BAM files to make a genotype comparison at any given site. (Recommended: 15 for WES-WES comaprison).

* **filter_VCF**: When set to True, will filter out variants which are not SNPs and have 1KG_AF values outside of 0.45-0.55. (Recommended: False. Generally, easier to just pre-select the variants positions to be compared, and not use this option).

* **number_of_SNPs**: The maximum number of variant sites to compare, even if the the input VCF file contains more variants. 

* **fast_freebayes**: When using Freebayes for genotype calling, by default, each position is called separately (with --region). This is less efficient, but as Freebayes' --targets sometimes fails in our testing, this is a safer option. Set this option to "True" will enable using "--targets" during when running Freebayes. (Recommended: False. Slower but safer).

* **VCF_file**: If you are using the same VCF file most of the time, then just set this option here, then you won't need to specify the VCF path every time you run BAM-matcher.



**[VariantCallerParameters]**

Set memory requirements (Java VM) and number of processing threads (GATK only).

**[GenomeReference]**

* **REFERENCE**
* **REF_noChr**
* **REF_wChr**



**[BatchOperations]**



## Running BAM-matcher ##









## Running tests ##


* Summary of set up
* Configuration
* Dependencies
* Database configuration
* How to run tests
* Deployment instructions

### Contribution guidelines ###

* Writing tests
* Code review
* Other guidelines

### Who do I talk to? ###

* Repo owner or admin
* Other community or team contact