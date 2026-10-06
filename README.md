# fldAIBC carrier plotting code

Reproducible plotting notebooks for the comparative-genomic and population-scale metagenomic study of bacterial `fldAIBC` carriers. Each manuscript figure has one notebook. 

## Repository layout

```text
.
├── notebooks/
│   ├── figure1.ipynb
│   ├── figure2.ipynb
│   ├── figure3.ipynb
│   └── figure4.ipynb
├── data/
│   ├── figure1/              # Component indicators, locus tables and iTOL inputs
│   ├── figure2/              # Population summaries, count matrix and map boundaries
│   ├── figure3/              # Disease and lineage association summaries
│   └── figure4/              # Prediction and community-context summaries
├── outputs/
│   ├── figure1/
│   ├── figure2/              # Includes regenerated source_data/ tables
│   ├── figure3/
│   └── figure4/
├── data_manifest.tsv         # Input sizes, SHA-256 checksums and original filenames
├── validation_report.json    # Packaging and clean-kernel execution checks
├── requirements.txt
├── .gitattributes            # Preserve input, notebook and output bytes
└── .gitignore
```


## Installation and execution

Python 3.9 is the tested environment. The plotting dependencies in `requirements.txt` are pinned to the versions loaded during validation: NumPy 1.21.6, pandas 1.4.3, Matplotlib 3.5.2, seaborn 0.11.2 and Pillow 9.2.0. Use a separate environment for these notebooks.

```bash
python -m pip install -r requirements.txt
python -m ipykernel install --user --name fld-plotting --display-name "Python (fld plotting)"
python -m jupyter lab
```

Open a notebook, select **Python (fld plotting)** and run every cell from top to bottom. The current working directory must be the repository root or `notebooks/`. When run from `notebooks/`, inputs resolve to `../data/figureN/` and exports to `../outputs/figureN/`. No original drive paths, external Python helper files or map downloads are required.

Alternatively, execute a notebook from the repository root:

```bash
python -m jupyter nbconvert --execute --to notebook --inplace --ExecutePreprocessor.kernel_name=fld-plotting --ExecutePreprocessor.timeout=300 notebooks/figure1.ipynb
```

Repeat with `figure2.ipynb`, `figure3.ipynb` and `figure4.ipynb`. Executing the notebooks replaces their generated panel files under `outputs/`; input files under `data/` are not modified.

## Figure and panel mapping

The order of the nonempty plotting cells in the supplied Figure 2, 3 and 4 notebooks defines final panels a, b, c and d. Historical labels inside comments, input names and export stems have been reconciled with that order.

| Notebook | Final panels | Content |
| --- | --- | --- |
| `figure1.ipynb` | b | Component co-occurrence |
| | c | FldBC phylogeny and iTOL annotations, rendered externally |
| | d | Accessory-gene positional frequencies and representative loci; exported as upper and lower components |
| `figure2.ipynb` | a–d | Global carrier prevalence; prevalence versus abundance; carrier-group abundance; within-sample composition, richness and dominance |
| `figure3.ipynb` | a–d | Disease association landscape; CRC cohort estimates; coarse-to-resolved carriage prevalence; lineage contrasts and carriage-definition robustness |
| `figure4.ipynb` | a–d | Prediction performance and permutation null; adjusted community associations; cross-study reproducibility; FastSpar correlations across contexts |

The Figure 1a schematic is intentionally excluded, as requested. Figure 3d retains the combined contrast and robustness plot from the fourth source plotting cell; it is not split into an additional panel. Figure 4a–d correspond to the source notebook's historically labelled b–e cells.

## Figure 1c: manual iTOL rendering

The notebook checks and documents these inputs but does not redraw the tree with Python:

1. Import `data/figure1/itol/tree_FldBC_concat.nwk` into [iTOL](https://itol.embl.de/).
2. Upload `01_labels.txt`, `02_tree_colors.txt`, `03_strip_phylum.txt`, `04_strip_family.txt` and `05_symbol_status.txt` from the same directory.
3. Configure the tree appearance and export it to `outputs/figure1/`.

`FldBC_concat_iqtree.treefile` is a byte-identical copy of the primary tree. Other supplied FastTree and IQ-TREE files are retained as supporting trees. The available files do not archive every iTOL layout setting, so exact reproduction of the final tree appearance requires those settings to be supplied separately. No automatic Figure 1c image is claimed here.

## Data and output scope

Figures 3 and 4 plot finalized summary tables; their upstream association models, prediction training, permutation testing and FastSpar inference are not rerun. Figure 2 retains the source notebook's count aggregation and regenerates four derived TSV files under `outputs/figure2/source_data/`. The package does not automatically assemble the separately exported panels into final composite manuscript figures.

Figures 1d, 2, 3 and 4 export SVG, PDF, PNG and TIFF. Figure 1b retains the original PDF/PNG-only exports. Raster dimensions and DPI follow the source plotting code.
The source font settings are retained. Arial is used where available; font substitution on another operating system can change text placement. Exact raster identity across operating systems and plotting-library versions is therefore not guaranteed. PDF metadata and generated SVG identifiers can also vary between executions.


The Figure 2 country boundaries are a packaged Natural Earth 1:110m asset. Natural Earth map data are in the public domain under its [terms of use](https://www.naturalearthdata.com/about/terms-of-use/). No map download is needed during execution.

## Validation

The four notebooks were executed from clean Python kernels using only the packaged relative inputs. Input copies were checked against their originals using SHA-256; syntax, notebook format, panel order, English comments and missing-file references were checked. `validation_report.json` records the final execution and file checks, and `data_manifest.tsv` provides portable input checksums without exposing local source-directory paths.

Data-sharing permissions and the choice of repository license are the responsibility of the authors.
