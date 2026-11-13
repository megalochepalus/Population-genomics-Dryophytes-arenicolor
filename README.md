## Pipeline Summary & Workflow

This repository contains the code and data pipelines for the population genomics and transcriptomic analysis of the work entitled "**Genetic diversity, population structure and signatures of divergent selection in the canyon treefrog (*Dryophytes arenicolor*)**". Below is an overview of the methodological workflow:

### 1. RNA Extraction & Sequencing
* **Sampling:** Whole brains extracted from 76 individuals across three populations (Gosner stage 42; Hernández-Herrera et al., 2024) preserved in RNAlater at -20°C.
* **Extraction & Quality:** Total RNA extracted using the RNeasy Mini Kit with DNase I treatment; quantified via NanoPhotometer N120 and assessed via agarose gel electrophoresis.
* **Pooling & Sequencing:** Equimolar pooling (300 ng/individual) performed to account for individual variation. Paired-end mRNA libraries (2×150 bp) sequenced on an Illumina NovaSeq 6000 by Novogene Inc. (NCBI BioProject: **PRJNA1477984**).

### 2. Quality Control & Transcriptome Assembly
* **Preprocessing:** Read quality assessed with FastQC v0.11.9. Adapters and low-quality bases trimmed using Trimmomatic v0.39 and cutadapt v3.5.
* **Assembly & Annotation:** *De novo* transcriptomes assembled using Trinity v2.13.2 and evaluated for completeness via BUSCO v5.8.2. Open reading frames (ORFs) predicted via TransDecoder v5.7.1, annotated against the *Xenopus laevis* reference proteome (v10.1) using BLASTP, and collapsed to the longest isoform per gene.

### 3. Read Alignment & SNP Calling
* **Alignment:** Reads indexed and aligned to the reference transcriptome using Bowtie2 v2.5.4 in end-to-end mode.
* **Variant Calling:** Processed with SAMtools and BCFtools v1.22; variant calling executed via FreeBayes v0.9.14 in pooled-continuous mode.
* **Filtering:** Filtered using BCFtools and VCFtools ($\text{depth} \ge 10\times$, $\text{QUAL} \ge 25$, missing data $\le 40\%$, $\text{MAF} \ge 0.03$).

### 4. Population Genomics
* **Structure & Clustering:** LD pruning performed; global variant distribution assessed via Principal Component Analysis (PCA) in PLINK v1.9, and genetic clustering evaluated using LEA v3.22.0 ($K = 1$ to $5$, cross-entropy criterion).
* **Genetic Diversity & Differentiation:** VCFtools utilized to calculate pairwise $F_{ST}$, observed ($H_o$) and expected ($H_e$) heterozygosity, nucleotide diversity ($\pi$), $F_{IS}$, Tajima's D, and allele frequency spectra.

### 5. Selection & Functional Enrichment
* **Outlier Detection:** Putatively adaptive loci identified using an $F_{ST}$ outlier approach ($\ge 99\text{th}$ percentile).
* **Functional Annotation & Networks:** GO enrichment evaluated via STRING db (*X. laevis* reference) with Benjamini-Hochberg FDR correction. Redundant GO terms summarized using ClusterProfiler and SimplifyEnrichment. Protein-protein interaction (PPI) networks analyzed to identify top hub genes based on combined degree and betweenness centrality scores.

---

### Code & Documentation
Specific scripts and reproducible workflows can be found at the project website: [Population Genomics - Dryophytes arenicolor](https://megalochepalus.github.io/Population-genomics-Dryophytes-arenicolor/)
