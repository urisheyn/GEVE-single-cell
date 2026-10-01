# GEVE single-cell transcriptomics: manuscript figures and tables

Code and derived data for the single-cell RNA-seq analyses in:

> Sheyn U\*, Heery R\*, Erazo-Garcia MP\*, Xu L, Craig RJ, de Mendoza A#, Aylward FO#.
> **A chimeric infection program and epigenetic conflict underpin endogenous giant virus latency.** (in preparation)

The notebook `GEVE_manuscript_figures.ipynb` regenerates every single-cell figure and all eight
supplementary tables from the QC-filtered count data. The two notebooks in `upstream/` show how that
count data was produced from the split-pipe output.

## Repository layout

```
GEVE_manuscript_figures.ipynb   main notebook: figures + Supplementary Tables S1–S8
environment.yml                 conda environment (Python 3.11, scanpy 1.11)
data/
  Chlamy_GEVE_gene_annotation.xlsx          GEVE gene annotation (506 canonical genes; sheet GEVEv2_full_ano)
  GEVE_promoters/fimo.tsv                   FIMO hits of the STREME-1 NCLDV late-promoter motif
  GEVE_promoters/late_promoter_fimo_q05.txt 105 genes with a FIMO hit at q < 0.05
  virion_proteome/                          virion proteome, derived from Erazo-Garcia et al. 2025 (see its README)
figures/                        notebook output: every figure as .png, .pdf and .svg
tables/                         notebook output: TableS1–S8 as CSV + GEVE_supplementary_tables.xlsx
upstream/
  01_QC.ipynb                   split-pipe count matrices -> adata_all_qc.h5ad
  03_clustering.ipynb           adata_all_qc.h5ad -> adata_hi4_hvg_geve_umap.h5ad (UMAP, cluster_hi4)
```

## Input data

The notebook reads two AnnData files from `adata/` (or from the folder named in `GEVE_ADATA_DIR`).
They are not stored in this repository.

| File | Contents | Source |
|---|---|---|
| `adata_all_qc.h5ad` | 22,421 QC-filtered cells, all genes, raw counts | NCBI GEO [GSE347098](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE347098) |
| `adata_hi4_hvg_geve_umap.h5ad` | GEVE > 4 cells with UMAP coordinates and `cluster_hi4` | Zenodo, doi:10.5281/zenodo.XXXXXXX |

## Running

```bash
conda env create -f environment.yml
conda activate geve-sc
python -m ipykernel install --user --name sctrans --display-name scTrans

mkdir adata    # put the two .h5ad files here, or: export GEVE_ADATA_DIR=/path/to/h5ad
jupyter nbconvert --to notebook --execute --inplace \
    --ExecutePreprocessor.kernel_name=sctrans GEVE_manuscript_figures.ipynb
```

Run it from the repository root. A full run takes about one minute and writes to `figures/` and `tables/`.

## Where each manuscript item is made

All items below come from `GEVE_manuscript_figures.ipynb`. The notebook's section headers use the same names.

| Manuscript item | Output file(s) |
|---|---|
| Figure 2. GEVE transcriptional dynamics and single-cell developmental trajectory | `figures/Fig2_GEVE_transcriptional_dynamics.*` |
| Figure 3. Transcriptomic composition by GEVE activity state | `figures/Fig3_transcriptomic_composition.*` |
| Figure S2. Pairwise co-occurrence of six binary GEVE genomic features | `figures/FigS2_feature_cooccurrence_upset.*` |
| Figure S3. GEVE expression heatmap, virocells vs top-21 High-GEVE latent cells | `figures/FigS3_virocell_GEVE_expression_heatmap.*` |
| Appendix Figure 3. Volcano plot of GEVE gene differential expression | `figures/AppFig3_GEVE_detection_volcano.*` |
| Appendix Figure 4. Differential detection of GEVE virion protein genes | `figures/AppFig4_virion_protein_detection.*` |
| Appendix Figure 5. GEVE genomic feature category enrichment | `figures/AppFig5_feature_category_enrichment.*` |
| Appendix Figure 6. Data-driven cell-state boundaries | `figures/AppFig6_cell_state_thresholds.*` |
| Appendix Figure 7. Median library depth per sample | `figures/AppFig7_library_depth_per_sample.*` |
| Appendix Figure 8. Single-cell GEVE transcriptomes on the viral genome | `figures/AppFig8_single_cell_GEVE_genome_map.*` |
| Appendix Figure 9. Detection-rate comparison, Active GEVE Expressing Cells vs High-GEVE | `figures/AppFig9_detection_GEVE_active_vs_High_GEVE.*` |
| Appendix Figure 10. Most-variable GEVE genes across the 39 High-GEVE cells | `figures/AppFig10_High_GEVE_variable_gene_heatmap.*` |
| STAR Methods: lytic and latent module definition | `figures/Methods_lytic_latent_module_definition.*`, `tables/Methods_lytic_latent_modules_506.csv` |
| Supplementary Tables S1–S8 | `tables/TableS1_…csv` … `tables/TableS8_…csv`, `tables/GEVE_supplementary_tables.xlsx` |

Figures 1 and 4–7, Figures S1 and S4–S8, and Appendix Figures 1–2 (genome, methylation, nanopore and
EM-seq analyses) are not made here.

## Upstream processing

`upstream/01_QC.ipynb` builds `adata_all_qc.h5ad` from the split-pipe v1.1.2 `DGE_filtered/` matrices
(set `GEVE_PARSE_DIR`). `upstream/03_clustering.ipynb` builds `adata_hi4_hvg_geve_umap.h5ad`. Both are
included for transparency. Their saved outputs come from the original runs, and the deposited
h5ad files are the ones those runs produced. To re-run them, start from the `upstream/` folder.

## License

Code: MIT (see `LICENSE`). Data, figures and tables (`data/`, `figures/`, `tables/`): CC BY 4.0.
`data/virion_proteome/` is derived from Erazo-Garcia *et al.* 2025, *Science*, doi:10.1126/science.ads6303. Please cite that article when reusing it.
