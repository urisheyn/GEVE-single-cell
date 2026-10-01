# GEVE virion proteome (derived from Erazo-Garcia et al. 2025)

`GEVE_virion_proteins_ErazoGarcia2025.csv` is derived from the supplementary data of:

> Erazo-Garcia M. P. *et al.* (2025). *Science*. doi:10.1126/science.ads6303

| Column | Source |
|---|---|
| `protein_ids`, `start_in_complete_contig_536`, `end_in_complete_contig_536` | Data S1, sheet `viralrecall_anno` (ViralRecall protein IDs and coordinates on contig_536) |
| `detected_in_virion_proteome` | `True` if the protein is listed in Data S5, sheet `filt_data` (LC-MS/MS of isolated GEVE virions; 43 proteins) |
| `virion_functional_cat` | Data S5 `functional_cat` |

The notebook maps these proteins to GEVEv2 gene models by matching the start (or, failing that, the end) coordinate, which gives 42 virion structural protein genes. The original xlsx files are not redistributed here; download them from the *Science* article page.
