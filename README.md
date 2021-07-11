# Pando <img src="man/figures/logo.png" align="right" width="180"/>

Pando leverages multi-modal singel-cell measurements to infer gene regulatory networks using a flexible linear model-based framework. By modeling the relationship between TF-binding site pairs with the expression of target genes, Pando simultaneously infers gene modules and sets of regulatory regions for each transcription factor.

## Introduction

The fate and state of a cell is regulated through complex circuits of transcription factors (TFs) converging at regulatory elements to enable precise control of gene expression. Modern single-cell genomic approaches allow the simultaneous profiling of gene expression and chromatin accessibility in individual cells, which opens up new opportunities for the inference of cell fate regulomes. Pando jointly utilizes scRNA-seq and scATAC-seq data to infer regulatory relationships between TFs and target genes.


## Installation

```r
devtools::install_github('quadbiolab/Pando')
```

## Quick start

If you have a `seurat_object` with transcriptomic and chromantin accessibility data, you can start right away with infering the regulatory network:

```r
# Load Packages
library(Pando)
library(Seurat)
library(BSgenome.Hsapiens.UCSC.hg38)

# Get motif data
data(motifs)

# Select variable features
seurat_object <- Seurat::FindVariableFeatures(seurat_object, assay='RNA')

# Initiate GRN object and select candidate regions
seurat_object <- initiate_grn(seurat_object)

# Scan candidate regions for TF binding motifs
seurat_object <- find_motifs(
    seurat_object,
    pfm = motifs,
    genome = BSgenome.Hsapiens.UCSC.hg38
)

# Infer gene regulatory network
seurat_object <- infer_grn(seurat_object)

# Print inferred coefficients
coef(seurat_object)

# Find gene and regulatory modules 
test_srt <- find_modules(test_srt)

# Print modules
NetworkModules(test_srt)
```

## More

Pando is actively being developed, an API reference and more vignettes are coming soon, stay tuned!





