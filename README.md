# Data Management Guide for Genomic Data
A beginners guide to genomic data management

## Table of Contents

1. [Introduction](#introduction)
2. [Getting Started](#getting-started)
3. [Create a Project](#create-a-project)
4. [File Structure on Hydra](#file-structure-in-hydra-storage)
5. [Sample Names](#sample-names)
6. [A Project README File](#a-project-readme-file)
7. [The Master Metadata File](#the-master-metadata-file)
8. [Processed Data Files](#processed-data-files)
9. [Uploading your data to NCBI](#uploading-your-data-to-ncbi)
10. [Template README File](#template-readme-file)
11. [Example README File](#example-readme-file)

## Introduction

This guide is meant as an introduction to data management for the long term storage of genomic data and a practical guide for beginners. It also includes specific instructions for the storage and maintenance of genomic data generated at the Center for Conservation Genomics (CCG) at the Smithsonian National Zoo and Conservation Biology Institute (NZCBI). Genomic data generated at CCG must be notated and stored in the long term storage of the high-performance computing (HPC) cluster Hydra. For help accessing and navigating Hydra, please refer to the hydra wiki: <https://confluence.si.edu/display/HPC/Overview>.

Overall, when managing your data for a project, keep in mind what information would someone need to understand your data if you were not around to ask any questions.

And remember, data management is best done throughout the entire life cycle of a project. Don't wait until the end of a project to start your data management!

## Getting Started

### Requesting a hydra account

CCG members working with genomic data can request accounts on hydra and log in by following instructions on: <https://confluence.si.edu/display/HPC/Logging+into+Hydra>

Follow the link under "requesting access" for "Non-SAO users" to the online form to request access. When filling out the form, make sure in the text box that asks how you intend to use Hydra that you mention that you need to be added to the `nzp_ccg` group. This will ensure that all of your files on hydra will be associated with our data group at CCG and then we can better share files and manage your data in the long-term.  Once approved and processed you will receive an email to your SI email with specific instuctions on how to log into your account.

Note that hydra has a separate account and login than your SI Network account (and do NOT make your password the same for both accounts!). Also remember you need to change your password for hydra every 180 days (put this in your calendar). Please refer to the above link or contact Kira Long if you have additional questions on requesting an account on hydra or logging in. If you don't get a response to your hydra account request in about a week, let Kira know and she will investiagate on your behalf.

### Command-line Interface and Unix Commands

Please see the hydra github for a basic introduction to Unix command line and hydra use: <https://github.com/SmithsonianWorkshops/Hydra-introduction>

Throughout this guide, we will put specifc examples of the required commands, however, a full deep-dive into unix and shell scripting is beyond the scope of this guide. Please refer to the [online workshops](https://swcarpentry.github.io/shell-novice/index.html), [commands cheatsheet](https://www.geeksforgeeks.org/linux-unix/linux-commands-cheat-sheet/), and attend Kira Long's office hours on Wednesdays 1-3pm at CCG to learn more on unix command line, shell scripting, and hpcs.

## Create a Project

### Picking a Project Name

Project names must be informative and unique, but keep them short/brief. Do not put spaces or special characters in your project name. Ideally your project name will not just be the taxa you study as there are numerous projects that can occur over time on the same species. Similarly, for long-term storage, it is better to not just store data under the lead reseracher's name. Project names can include multiple identifiers such as `Species_MainAnalysis_Researcher`. For example, `GrasshopperSparrow_PopStructure_Fleischer` or `Mariana_Crow_PopGen_Structure` or `Amakihi_GRW4_Challenge_Transcriptome`.

The project name is the primary identifier and should be the name of the directory that will contain your data in hydra long-term storage. The path to the hydra CCG long-term storage is: `/store/nzp_ccg`. Once you have obtained a hydra account, you can create your project directory within the long-term storage directory using the command `mkdir <DIRECTORY_NAME>`, so as an example `mkdir Mariana_Crow_PopGen_Structure` will create an empty directory named `Mariana_Crow_PopGen_Structure`.

### Add your project to the CCG Long-term Data Storage Database

All genomic data generated at the CCG needs to be added to the`CCG_Long_Term_Data_Storage` list. CCG members can access our long term data storage list through the sharepoint link in the `Bioinfomatics` channel of the CCG Teams or by contacting Kira Long. If you need to be added to the CCG Teams, contact Nancy McInerney.

After selecting a project name, add your project to the appropriate tab. There are two tabs, the first tab is for published data, and the second tab is for unpublished data. Current/ongoing projects will go under the `Unpublished_Data` tab.

## File Structure in Hydra storage

In your project directory, you will need to create and mainatain the following directories: `RawData`, `ProcessedData`, and `MetaData`.

We recommend that as soon as you receive your sequencing data to store a copy of your raw `fastq` files in your project directory. Your path should generally look like the following: `/store/nzp_ccg/<YOUR_PROJECT>/RawData`

Example project directory structure:
```
[longk@login02 GRSP]$ ls
MetaData  ProcessedData  README.md  RawData
```
Note that there are 3 direcotries (MetaData, ProcessedData, RawData) and one file (README.md) in the main project directory. You can organize your subdirectories more tailored to your project under this main directory, but this is our suggested project directory organization (i.e. you may have multiple subdirectories in `RawData` for each type of sequencing like whole-genome versus RADseq versus mitogenomes).

### Permissions

Once you have data in hydra store, make sure you check your data/directory permissions. Briefly, permissions are in two parts: who has access and what can they do. First, who can access the files is split into 3 categories: the main user (you), the group (in our case CCG is our group, notated as `nzp_ccg`. If you are unsure if you are in the `nzp_ccg` group, run the command `groups <YOUR_USERNAME>` and the resulting list should contain `nzp_ccg`. If you don't see `nzp_ccg` listed, contact Kira Long and she will get you added), and then all other users. The three main categories of what can be done to the files is read (r), write (w), and execute (x). For further general information on permissions in a unix/linux system, see: <https://www.tutorialspoint.com/unix/unix-file-permission.htm>.

We need to ensure that all data uploaded to hydra from CCG in either the CCG `scratch` or `store` directories is correctly assigned to the `nzp_ccg` group and that file and directories are read/write/executable. You can check your file permissions using the command `ls -l` and look at the first column the command displays in your terminal.

```
[longk@login01 GRSP]$ ls -l
total 51
drwxrwxr-x 2 longk nzp_ccg    3 Jan  2 16:05 MetaData
drwxrwxr-x 9 longk nzp_ccg   10 Dec 16 16:44 ProcessedData
-rw-rwxr-x 1 longk nzp_ccg 2941 Jan 21 14:46 README.md
drwxrwxr-x 2 longk nzp_ccg   81 Jan 21 14:44 RawData
```

Here, we can see the permissions are written as `-rw-rwxr-x` or `drwxrwxr-x`. Directories have a `d` in the front of the permissions column, while files have `-`. Next, for the `README.md` file we have `-rw-rwxr-x` which, we read in groups of 3s after the directory designation. So to break this down, we have `-` designating this is a file and not a directory, `rw-` meaning "you" (the main user/creator) have read and write permissions but not excecute permissions, `rwx` the group has read write and execute permissions, and `r-x` means that all other users have read and execute permission. 

You can change the group permissions to `nzp_ccg` for all permissions using

```
# Set the group of your data directory to nzp_ccg
chgrp -R nzp_ccg <your data directory>

# Change the permissions to group level read, write, execute
chmod -R g=rwx <your data directory>
```
You can also set the permissions for "other" users to read-only so they can see and copy data, but not change the data in any way. Make sure you do NOT give other users write access.

```
# Change permissions for other users to read and execute but NOT write
chmod -R o=rx <your data directory>
```

## Sample Names

Sample names must be unique, informative, and sortable. Again, make sure to not use any special characters or spaces in your sample names. For sortability, I recommend using a consistent delimiter between various parts of your sample name, I often use an underscore.

## A Project README File

### What is a README?

A README is a text file that describes other files in a project or directory that has been typically used in software development and distribution. The README file contains information about the other files in a project directory or serves as and archive for computer software and is a form of documentation. README files are plain text files and are often saved as `README`, `README.txt`, or `README.md`. The `.md` file extension indicates that README, while still a plain text document, was written with Markdown formatting for easy HTML and/or PDF conversions of your README file. GNU coding standards encourage the use of README files as a "general overview" of a software package.

## The Master Metadata File

When specifying metadata, make sure to include any information that is relevant to keeping the dataset viable and usable in the future assuming that there is no one to talk to about the data 30 years from now. What information would be needed for another naive researcher to pick up the data and use it effectively? It is imperative that the raw genomic data files can be associated with the sample metadata (e.g. sample1.fastq is from INDIVIDUAL of SPECIES from YEAR at LOCATION). The more associated information with each raw fastq file the better, but include the minimum amount of data such as sample ID, species, year, and location of the sampling for every fastq file. Note that it is also helpful to keep sample names consistent across EVERYWHERE they appear in all data files and tables so that associated metadata is more easily searchable.

## Processed Data Files

Keep important processed data files such as alignments (Binary Alignment Map (BAM) files), raw forms of Variant Call Format (VCF) or Binary Call Format (BCF) files (recommended to keep variant and invariant VCFs), final/filtered VCFs, etc. This will vary dramatically between projects so add processed files as deemed fit per project. Make sure you think about which files are important to save, organize, and notate but also due to space constraints, do not save EVERY processed file, test file, or temporary file for long term storage. Prioritize storing raw forms of your processed data so that others in the future can better use your data for other purposes (e.g. a raw VCF file). In addition, for publications it is also best to save a final copy of the fully filtered and processed data that appears and is used in the manuscript for the final figures.

Add descriptions of your processed files, especially for less standard processed files. For example, if you have BAM files, specify which species and reference genome you used for the alignments (and always put the RefSeq accession number for the reference genome used).

Put reference for the software used to generate the files (and always put the software version!).

## Uploading your data to NCBI

Most publications and/or funding bodies in genomics require that sequencing data be made publically available. The National Center for Biotechnology Information [(NCBI)](https://www.ncbi.nlm.nih.gov/) hosts biomedical and genomic information for public access as well as tools such as BLAST. Sequence Read Archive (SRA) and GenBank are the NCBI databases that host the sequencing data. While many researchers wait to upload their sequences to NCBI until required for publication, we recommend uploading your raw sequencing data as soon as possible if you are able, as this creates an additional safe copy of your data in case of catastrophic accidents (i.e. you left your raw data in a scratch directory on an hpc and your data got scrubbed and you failed to notice until the data was no longer recoverable and/or your backup hard drive spontaneously fails).

For those at CCG, make sure when uploading your data to NCBI to add your data to the Center for Conservation Genomics group when you fill out the submitter tab. This will allow the CCG lab group to manage data uploaded to NCBI after members leave and ensure that we can update projects as needed in the future. If you need to be added to the Center for Conservation Genomics group, please contact Michael Campana.

## Template README File

Below is a template for a README file for unpublished genomic data. This README is meant to be kept in a project directory for genomic data. If there is additional information you deem necessary to keep with your data, add sections and labels as you see fit to the README file, this is only a suggested README to cover common information associated with genomic datasets. This README is quite detailed as it's purpose is to record all associated metadata for an *unpublished* project, and should be created at the start of a project and continuously updated up until publication. Your README will also aid in drafting a detailed methods section for your future publications, as most of the methods details should already be recorded or linked to in the README.

## Project: PROJECT_NAME

(Note: keep your project name consistent so it is searchable)

* Publication status: Unpublished Data (put published or unpublished)

## Project Description

2-3 sentence description of the project. Include what (e.g. taxa), where (e.g. location of sampling), how (e.g. protocol/type of sequencing etc.), and goal of project (e.g. to assess genetic diversity, effect of bottlenecks, inbreeding, translocations etc.).

### People

Name of person who generated data: <email@email.com> \
Name of PI overseeing project: <email@si.edu> \
Name of any other relevant people who may need to be contacted about data: <email@email.com>

### Year Data was generated

Put relevant years for your project: e.g. year samples were collected, years samples were sequenced.

### Associated Documents

If there are any associated documents for this dataset, put them here. Citations to published works are best and published datasets don't need as much detail in the below sections on funding and permits. However, for unpublished data, note if the dataset was used in a dissertation or a preprint or manuscript draft and who to contact about those unpublished or not publically available documents (can just put the name of someone listed in the 'People' section above).

### Funding

Especially for unpublished data, the original funding source could easily be forgotten and thus will be lost for future publications. Note the funding sources for the sampling, sequencing, and/or materials here.

### Permits

Especially for unpublished data, any IACUC or ACUC permit numbers or collecting permits associated with the sampling/dataset should be listed here so they are not dissociated from the sequencing data.

## Data description

### Raw Sequencing data

Raw data can be found in:

```text
Put the path to the raw data to where it is stored on hydra. Long term storage should be in hydra_NAS: /store/nzp_ccg/PROJECT_NAME/RawData
```

Specific file info:

``` text
If there are additional distinctions that must be made about the raw data, put the path to the file name here
```

Notes about specific raw data files

### Metadata Files

When specifying metadata, make sure to include any information that is relevant to keeping the dataset viable and usable in the future assuming that there is no one to talk to about the data 30 years from now. What information would be needed for another naive researcher to pick up the data and use it effectively? It is imperative that the raw genomic data files can be associated with the sample metadata (e.g. sample1.fastq is from INDIVIDUAL of SPECIES from YEAR at LOCATION). The more associated information with each raw fastq file the better, but include the minimum amount of data such as sample ID, species, year, and location of the sampling for every fastq file. Note that it is also helpful to keep sample names consistent across EVERYWHERE they appear in all data files and tables so that associated metadata is more easily searchable.

``` text
Path to where the metadata files are on hydra
/store/nzp_ccg/PROJECT_NAME/MetaData
```

### Data Generation

#### Samples

Put information here on the samples such as if the samples are from blood, fecal, buccal swabs etc. Specify if there were museum specimens or ancient samples used, and where and when they are from (which museum? From what years?) If DNA was collected from another, published project, notate that here. Ideally put summary of sample sizes here (e.g. what were the total number of individuals sequenced? Number per site? Number of ancient versus modern samples?)

#### DNA extraction

What was the method of DNA extraction used?

#### Library Prep

Note the protocol used to generate the library (e.g. whole genome sequencing, RADseq, Sequence capture, RNAseq, etc.). Note helpful protocol specifics such as which restriction enzyme used in a RADseq library. Any non-standard protocol changes note here as well.

#### Sequencing

Put the sequencing facility (e.g. University of Illinois Urbana-Champaign Core Sequencing Facility), machine (e.g. Illumina NovaSeq 6000), lane type (e.g. SP).

### Processed Data

Keep important processed data files such as alignments (BAM) files, raw forms of VCF/BCF files (recommended variant and invariant VCFs), final/filtered VCFs, etc. This will vary dramatically between projects so add processed files as deemed fit per project.

``` text
Path to where the processed files are on hydra
/store/nzp_ccg/PROJECT_NAME/ProcessedData
```

If needed, describe the processed file type (e.g. bam files from alignment to reference genome (put NCBI RefSeq accession number for the reference genome)). Put reference for the software used to generate the files (and always put the software version!).

## Associated databases and repositories

If there are databases or repositories associated with the dataset, link them here. For example: \
GitHub: link_to_GitHub_repo \
NCBI: Put BioProject numbers and/or SRA accession numbers etc. \
Figshare: link_to_Figshare \
Dryad: link_to_dryad_dataset

## Notes

Add any additional notes you feel should stay associated with your dataset. Feel free to add more subsections to the above sections to suit your specific project, these are a starting guideline. The more metadata you can keep with your dataset the better! Data management is best done AS YOU GO so fill in your README during your project, and before you move on to your next one!

## Example README file

Below is an example of a filled in README file for unpublished genomic data.

## Project: Grasshopper_Sparrows

* Publication status: Unpublished Data

## Project Description

Investigation of genomic divergence and gene flow in Grasshopper Sparrows (Ammodramus savannarum) from migratory North American and resident Caribbean populations. DNA were sequenced with whole genome "shotgun" sequencing from three resident populations in the Caribbean (Puerto Rico, Hispaniola, Jamaica), three migratory populations in North American (Maryland, Georgia, Kansas), and non-migratory birds in Florida. The objective was to assess introgression and gene flow between migratory and non-migratory populations as well as assess differentiation in general between the island populations.

### People

Kira M. Long: <email@email.edu> \
Robert Fleischer: <email@email.edu> \
Sara Kaiser: <email@email.edu>

### Year Data was generated

2023

### Associated Documents

Smithsonian James Bond Grant proposal (Proposal Title: Genomic divergence, gene flow and the genetics underlying migration behavior in Caribbean and North American grasshopper sparrow populations; year: 2024)

### Funding

Smithsonian James Bond funds

### Permits

With collaborator Sara Kaiser

## Data description

### Raw Sequencing data

Raw data can be found in:

``` text
hydra_NAS: /store/nzp_ccg/GRSP/RawData
```

There are 78 paired fastq files for 39 individuals from 7 populations.

### Metadata Files

``` text
Path to where the metadata files are on hydra:
/store/nzp_ccg/GRSP/MetaData
```

### Data Generation

#### Samples

DNA is from avian blood samples from Puerto Rico (N= 6), Hispaniola (N= 5), Jamaica (N= 6), Maryland (N= 6), Georgia (N= 5), Kansas (N= 6), and Florida (N= 5) for a total of 39 individuals.

#### DNA extraction

Qiagen DNA extraction kit

#### Library Prep

Whole genome short read library

#### Sequencing

Illumina NovaSeq 2 x 150

### Processed Data

``` text
Path to where the processed files are on hydra:
/store/nzp_ccg/GRSP/ProcessedData
```

## Associated databases and repositories

NA

## Notes

NA

---
This guide was written by Kira M. Long in 2024. For additional questions or guidance on data management, contact Kira M. Long, Data Scientist at CCG.
