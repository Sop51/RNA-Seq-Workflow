# Final project for BF528, a RNA-seq workflow #

This final project consists of an a RNA-seq workflow.
The dataset utilized consists of 6 samples: 3 WT and 3 KO derived from a human source.

## Overall Workflow ##
### Step 1 (QC): ###
1. Run fastqc (version 0.12.1-0)
2. Run multiqc (version 1.20)

### Step 2 (Alignment): ###
1. Download the genome sequence, primary assembly (GRCh38 version 45) and the corresponding GTF file (comprehensive gene annotation, GRCh48 version 45) from GENCODE 
2. Generate a STAR index using STAR (v2.7.11b)
3. Align the reads to the genome using STAR (v2.7.11b) using the default parameters

### Step 3 (Post Alignment QC): ###
1. Run samtools flagstat (version 1.19.2)

### Step 4 (Generating Count Data): ###
1. Run Verse (v0.1.5) with default parameters on each of the bam files
2. Concatenate the verse results into one file
3. Map ensembl ID to the gene name
4. Filter the read counts that have a value of 0

### Step 5 (Differential Expression): ###
1. Run DESeq2 (v1.42.1) using the default paramteres to compare WT vs KO 

### Step 6 (Sample-Sample Distance Plot): ###
1. Create a sample to sample distance plot to see a visual representation of the similarities or dissimilarities between samples based on their gene expression profiles.

### Step 7 (Histogram): ###
1. Create a histogram showing the distribution of log2FoldChanges of DE genes at a significance threshold of 0.1

### Step 8 (Volcano Plot): ###
1. Create a volcano plot that clearly distinguishes between significant and non-significant genes as well as whether those genes are up - or downregulated based on their log2foldchange

### Step 9 (GSEA): ###
1. Perform FGSEA (GSEA) using a ranked list of all genes in the experiment
2. Performing gene set enrichment using the list of statistically significant DE genes
   a. Utilize a threshold of 0.1 to determine significant genes

### Step 10 (DAVID): ###
1. Extract genes for an enrichment analysis using DAVID
   a. Utilize the genes significant at a level of 0.001
