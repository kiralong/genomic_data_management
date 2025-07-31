# Project: PROJECT_NAME
(Note: keep your project name consistent so it is searchable)

* Publication status: Unpublished Data (put published or unpublished)

## Project Description

2-3 sentence description of the project. Include what (e.g. taxa), where (e.g. location of sampling), how (e.g. protocol/type of sequencing etc.), and goal of project (e.g. to assess genetic diversity, effect of bottlenecks, inbreeding, translocations etc etc.).

### People:
Name of person who generated data: email@email.com \
Name of PI overseeing project: email@si.edu \
Name of any other relevant people who may need to be contacted about data: email@email.com

### Year Data was generated:
Put relevant years for your project: e.g. year samples were collected, years samples were sequenced.

### Associated Documents:
If there are any associated documents for this dataset, put them here. Citations to published works are best and published datasets don't need as much detail in the below sections on funding and permits. However, for unpublished data, note if the dataset was used in a dissertation or a preprint or manuscript draft and who to contact about those unpublished or not publically available documents (can just put the name of someone listed in the 'People' section above).

### Funding
Especially for unpublished data, the original funding source could easily be forgotten and thus will be lost for future publications. Note the funding sources for the sampling, sequencing, and/or materials here.

### Permits
Especially for unpublished data, any IACUC or ACUC permit numbers or collecting permits associated with the sampling/dataset should be listed here so they are not dissociated from the sequencing data.

## Data description:
### Raw Sequencing data

Raw data can be found in:
```
Put the path to the raw data to where it is stored on hydra. Long term storage should be in hydra_NAS: /store/nzp_ccg/PROJECT_NAME/RawData
```
Specific file info:
```
If there are additional distinctions that must be made about the raw data, put the path to the file name here
```
Notes about specific raw data files

### Metadata Files

When specifying metadata, make sure to include any information that is relevant to keeping the dataset viable and usable in the future assuming that there is no one to talk to about the data 30 years from now. What information would be needed for another naive researcher to pick up the data and use it effectively? It is imperative that the raw genomic data files can be associated with the sample metadata (e.g. sample1.fastq is from INDIVIDUAL of SPECIES from YEAR at LOCATION). The more associated information with each raw fastq file the better, but include the minimum amount of data such as sample ID, species, year, and location of the sampling for every fastq file. Note that it is also helpful to keep sample names consistent across EVERYWHERE they appear in all data files and tables so that associated metadata is more easily searchable.

```
Path to where the metadata files are on hydra
/store/nzp_ccg/PROJECT_NAME/MetaData
```
### Data Generation
#### Samples
Put information here on the samples such as if the samples are from blood, fecal, buccal swabs etc. Specify if there were museum specimens or ancient samples used, and where and when they are from (which museum? From what years?) If DNA was collected from another, published project, notate that here. Ideally put summary of sample sizes here (e.g. what were the total number of individuals sequenced? Number per site? Number of ancient versus modern samples?)

#### DNA extraction
What was the method of DNA extraction used?

#### Library Prep
Note the protocol used to generate the library (e.g. whole genome sequencing, RADseq, Sequence capture, RNAseq, etc). Note helpful protocol specifics such as which restriction enzyme used in a RADseq library. Any non-standard protocol changes note here as well.

#### Sequencing
Put the sequencing facility (e.g. University of Illinois Urbana-Champaign Core Sequencing Facility), machine (e.g. Illumina NovaSeq 6000), lane type (e.g. SP). 

### Processed Data

Keep important processed data files such as alignments (bams), raw forms of vcf/bcf files (recommend variant and invariant vcfs), final/filtered vcfs, etc. This will vary dramatically between projects so add processed files as deemed fit per project.

```
Path to where the processed files are on hydra
/store/nzp_ccg/PROJECT_NAME/ProcessedData
```

If needed, describe the processed file type (e.g. bam files from alignment to reference genome (put RefSeq accession number for the reference genome)). Put reference for the software used to generate the files (and always put the software version!).

## Associated databases and repositories:
If there are databases or repositories associated with the dataset, link them here. For example: \
Github: link_to_Github_repo \
NCBI: Put Bioproject numbers and/or SRA accession numbers etc \
Figshare: link_to_figshare \
Dryad: link_to_dryad_dataset


## Notes
Add any additional notes you feel should stay associated with your dataset. Feel free to add more subsections to the above sections to suit your specific project, these are a starting guideline. The more metadata you can keep with your dataset the better! Data management is best done AS YOU GO so fill in your README during your project before you move on to your next one!

For additional questions or guidance on data management, contact Kira M. Long at longk@si.edu.

This template was written by Kira M. Long in markdown (.md) format in 2024.
