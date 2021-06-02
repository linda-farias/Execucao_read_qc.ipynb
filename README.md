# Execucao_read_qc.ipynb
How to use metaWRAP within Google Colab

Summary

The recent pandemic caused by the infectious disease Sars-CoV2-2019 has restricted the population to collective isolation. With this, ways were sought to use technology in their favor so that the different areas of work would not suffer a great impact during this period. In the meantime, this work developed a mini-project in which the quality of the use of cloud programs for analyzing metagenomic research data was evaluated. However, there are challenges in this service that still need to be overcome, and a strategy is needed for its good handling and management. It is concluded that this platform can indeed be a mechanism that influences its remote use so that its development in code can be manipulated and shared with other users.

Objective

The purpose of this work was to develop a remote system that manages the pipeline without the need to house and overload the developer's computer. For this, two hypotheses were conducted, in which the first seeks to store the files and programs in a supportable computational service, but one that can use it remotely through any computer that has a connection with this service; the other hypothesis is to develop in a cloud package through a website that can develop it.

To formulate this project, a pipeline, metaWRAP, was used, through which we could assess the quality of its development in this type of system. The metaWRAP version for this study is the latest version: metaWRAP 1.3.2

Methodology

1. Implementation
To qualify and standardize the use of metaWRAP in the operating system, different terminals were used, as well as Windows 10 (through wsl), google collab and jupyter notebook (within linux), to understand the advantages and disadvantages proposed in these environments.

2. Installation
Manual installation was performed through the following steps:
Download the metaWRAP repository directly from Github https://github.com/bxlab/metaWRAP or clone it using the command in the Linux terminal: git clone https://github.com/bxlab/metaWRAP.git; If you are going to use database modules, configure their location in the config-metawrap file located in the metaWRAP bin folder;
Add metaWRAP's /bin directory to the system's $PATH to make metaWRAP executable; Create and activate an environment variable:

```
count create -y -n metawrap-env python=2.7
count activate metawrap-env
```

Install all metaWRAP dependencies through conda:

```
count config --add channels defaults
conda config --add channels conda-forge
count config --add channels bioconda
count config --add channels ursky
```


3. Download samples

For this study, a pair of human intestinal sequences collected from the European Nucleotide Archive (ENA) database were used. 
Thus, the first step will be to download these sequences. With this, we will use as a base the first pair of samples that are exemplified in the metaWRAP github link. 
Installation was done by the download tool, wget. Each pair represents a study gene, in which one is forward and the other reverses. 
The command line used after wget to download these samples were:

```
ftp.sra.ebi.ac.uk/vol1/fastq/ERR011/ERR011347/ERR011347_1.fastq.gz
ftp.sra.ebi.ac.uk/vol1/fastq/ERR011/ERR011347/ERR011347_2.fastq.gz 
```
4. MetaWRAP dependencies

Although metaWRAP has a package with several independent dependencies, this work was restricted to evaluating only the READ_QC module which represents one of the three modules in the pre-processing. 
He is characterized by preparing the sequences before being assembled and aligned. 
For this, the raw sequences with unfeasible reads will be cut, as well as those that contain some contamination error (btmagger). 
At the end, a report will be made comparing the quality of these sequences before and after being processed.

In order to use this module, it is necessary that the preference samples have been previously downloaded, then it is necessary to unpack the sequences that are normally in the qz model. 
So that it can be run in metaWRAP. The command line for its execution is as follows:

```
metawrap read_qc [execution options] -1 first_part_of_sample -2 second_part_of_sample -o output_directory
```

Note 1: If these samples have not been downloaded with emphasis, you can alternatively use the following command:
```
metawrap read_qc --skip-bmtagger -1 RAW_READS/ERR011347_1.fastq -2 RAW_READS/ERR011347_2.fastq -t 24 -o READ_QC/ERR011347
```
Note 2: The ```--skip-bmtagger``` option flag is used to skip the step of the bmtagger hg38 module. 
With the command executed, the processing results will be saved in the ```READ_QC/ERR011347``` folder
Note 2: The ```--skip-bmtagger``` option flag is used to skip the step of the bmtagger hg38 module. 
With the command executed, the processing results will be saved in the ```READ_QC/ERR011347``` folder

