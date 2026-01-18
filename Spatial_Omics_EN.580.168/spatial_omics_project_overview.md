# Visium HD & CODEX Integration Analysis
I was exploring spatially-resolved correlation between gene expression (Visium HD) and protein expression (CODEX imaging).

## Overview

This project integrates two high-resolution spatial technologies:
- **Visium HD**: Spatial transcriptomics at 2μm resolution (~640k bins)
- **CODEX**: Multiplexed protein imaging at single-cell resolution

I took this data from https://spatch.pku-genomics.org/#/dataset/visiumff. It was the ovarian cancer data ID28.


Citation:

Ren P, Zhang R, Meng Y, Zhang Z, Zeng Z et al. Systematic Benchmarking of High-Throughput Subcellular Spatial Transcriptomics Platforms Across Human Tumors. Nature Communications. 2025 Oct 17;16(1):9232. doi: 10.1038/s41467-025-64292-3. PMID: 41107232. https://www.nature.com/articles/s41467-025-64292-3

### Pipeline

#### 1. ***Visium & CODEX spatial alignment***
- Used STalign to align the adjacent slides of the Visium and CODEX data
- Note: I set up a virtual environment as STalign uses python 3.10 and I had a lot of dependency problems
- I tried to match the protein to the gene that codes directly for it (no regulatory genes), but don't trust me 

#### 2. **Data Aggregation** (`aggregate_visium_hd_bins`)
- I aggregated high-resolution Visium HD 2μm bins into larger spatial bins
- Reduces data size while preserving spatial structure
- This was done because the Visium HD has very sparce matrix

#### 2. **Correlation Analysis** (`plot_matched_pair_with_table`, `batch_analyze_correlations`)
- Spatially matches Visium spots to CODEX cells
- Calculates Spearman and Pearson correlations (I didn't look into the distibution of the data to see which was best to use)
- Normalization: CPM, log1p,  z-score (to put the gene and protien data on the same scale)

#### 4. **Filtered Comparisons** (`analysis_1_cell_type_comparison`, `analysis_2_spatial_cluster_comparison`)
- **Cell Type Analysis**: Tests if correlations are stronger in specific cell populations
  - Note: The cell annotations were done by the SPATCH manually
- **Spatial Cluster Analysis**: Tests if correlations vary across tissue regions.
  - Note: The spatial cluster (cellular nich) were done by SPATCH manually


