# Differential Methylation Analysis

R Markdown script for differential methylation analysis of EPIC array data, developed as part of a Bachelor's thesis project.

The analysis identifies CpG sites and differentially methylated regions (DMRs) associated with a triple interaction between ADHD severity, socioeconomic status (SES), and ADHD polygenic scores (PGS).

---

## Analysis Overview

1. **Data loading & merging** — phenotypic data (targets) and ADHD polygenic scores are merged into a single table
2. **Preprocessing** — raw EPIC array data is normalised using `preprocessQuantile` (minfi)
3. **Differential methylation (DMPs)** — linear modelling with limma, testing the triple interaction term `ADHD * SES * PGS`
4. **Annotation** — significant CpGs are annotated using `IlluminaHumanMethylationEPICanno.ilm10b2.hg19`
5. **Gene Set Enrichment Analysis** — over-representation analysis of DMP and DMR genes using gprofiler2
6. **Differentially Methylated Regions (DMRs)** — region-level analysis using DMRcate

---

## Requirements

Install the following R packages before running:

**Bioconductor:**
```r
BiocManager::install(c(
  "limma", "minfi", "EpiSmokEr", "IlluminaHumanMethylationEPICanno.ilm10b2.hg19",
  "IlluminaHumanMethylationEPICmanifest", "DMRcate", "missMethyl",
  "FlowSorted.Blood.EPIC", "ChAMP", "Gviz", "ramwas"
))
```

**CRAN:**
```r
install.packages(c(
  "tidyverse", "ggpubr", "ggpmisc", "ggbeeswarm", "gplots",
  "openxlsx", "openxlsx2", "gprofiler2", "plotly",
  "RColorBrewer", "corpcor", "doParallel", "see",
  "compareGroups", "filematrix", "qvalue"
))
```

---

## Usage

1. Open `Differential_methylation_analysis.rmd` in RStudio
2. Set your file paths in the `user_paths` chunk at the top of the script:

```r
PATH_TO_PGS_DATA    <- "path/to/ADHD_PGSData_wide_unscaled.csv"
PATH_TO_TARGETS     <- "path/to/ProcessedData/targets.rds"
PATH_TO_EPIC_MERGED <- "path/to/ProcessedData/all_EPIC_merged.rds"
OUTPUT_FOLDER       <- "path/to/output/"
```

3. Run the script chunk by chunk or knit the document

---

## Input Data

| Variable | Format | Description |
|---|---|---|
| `PATH_TO_PGS_DATA` | `.csv` | ADHD polygenic scores per sample (wide format, unscaled) |
| `PATH_TO_TARGETS` | `.rds` | Preprocessed sample sheet with phenotypic variables |
| `PATH_TO_EPIC_MERGED` | `.rds` | Merged EPIC array data (RGChannelSet or similar) |

---

## Output Files

All output files are saved to `OUTPUT_FOLDER`:

| File | Description |
|---|---|
| `decideTests_summary_output.txt` | Summary of limma decision tests |
| `DMPs.xlsx` | Full table of differentially methylated positions |
| `gostplot_DMPs.pdf` | gprofiler2 enrichment plot for DMP genes |
| `gostres_DMPs.csv` | Full GSEA results for DMP genes |
| `gostres_DMPs_top10.csv` | Top 10 enriched terms for DMP genes |
| `DMRs_results.csv` | Differentially methylated regions |
| `gostres_DMRs.csv` | Full GSEA results for DMR genes |
| `DMRs_granges.csv` | DMRs as GRanges table |
| `cpg_plots.pdf` | Plots for four CpGs of interest |
| `combined_plot.png` | Exploratory plots for all significant CpGs |

---

## Author

Sophia Sedille
