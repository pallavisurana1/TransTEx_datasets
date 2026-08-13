# TransTEx expression groupings 
## (human · mouse · cancer)

A browser tool for looking up **TransTEx** transcript
expression-group classifications across three resources — **human tissues
(GTEx)**, a **mouse body map**, and **solid-tumor cancers (TCGA solid tumors)** —
and downloading any filtered slice as CSV. The browser app reads the combined
`TransTEx_Cancer_dataset.parquet` file, which now contains both the normal-tissue
and cancer records.

Available: https://pallavisurana1.github.io/TransTEx_datasets/

## What's in it

The data comes from the TransTEx scoring method, which assigns every transcript
to one expression group per resource based on how many tissues (or cancers) it
is reliably expressed in.

**Normal tissues (human GTEx, mouse body map)** — five groups:

| Class | Meaning |
|---|---|
| `TSp` | Tissue-Specific — reliably expressed in a single tissue |
| `TEn` | Tissue-Enhanced — expressed in 2 tissues up to 50% of tissues |
| `Wide` | Widespread — expressed in more than 50% of tissues |
| `Low` | Low or less expression — below the specificity threshold, some expression |
| `Null` | No / minimal expression across all tissues |

**Solid-tumor cancers (TCGA datasets)** — the same logic applied
across cancer types, giving `CanSp`, `CanEn`, `CanWide`, `CanLow`, `CanNUll`,
plus the two cross-resource biomarker groups: `CanHigh` (high in cancer, lost in
normal — oncogenic-like ) and `NorHigh` (high in normal, lost in
cancer — Tumor suppresor: TSG-like).

Everything is at **transcript / isoform level**, mapped to genes.

## Using the browser tool

Choose any number of normal tissues from **Tissues** and cancer types from
**Cancer types**;
choose any number of expression groups from **Categories**; then optionally
filter by species or transcript/gene. Leaving a multi-select empty means “all”.

Results and CSV downloads are collapsed to one row per transcript and species.
When the same transcript has more than one matching category or tissue/cancer,
the distinct values are shown as comma-separated lists. This keeps, for example,
`Low, CanLow` for the same ENST on one row, and combines the relevant tissues
for a `TSp, CanSp` transcript.

## Schema

The combined Parquet file uses this schema before the browser aggregates matching
records for display and export:

`transcript, gene_id, gene_name, tissue, category, species`

- `tissue` — the tissue (e.g. `testis`, `liver`) or cancer type (e.g. `GBM`, `OV`);
  it may be empty for a pan-cancer/non-context-specific category
- `category` — the expression group (`TSp`/`TEn`/`Wide`/`Low`/`Null` for tissues;
  `CanSp`/`CanEn`/`CanWide`/`CanLow`/`CanNUll` for cancer)
- `species` — `human` or `mouse`

## Data Citations

If you use this dataset or the associated methodologies, please cite the following publications:

### 🔬 Methods & Frameworks

*   **TransTEx Method (Human Transcriptome)**
    > Surana P, Dutta P, Davuluri RV. **TransTEx: novel tissue-specificity scoring method for grouping human transcriptome into different expression groups.** *Bioinformatics* 2024;40(8):btae475. 
    > 🔗 [doi:10.1093/bioinformatics/btae475](https://doi.org/10.1093/bioinformatics/btae475)

*   **TSProm (Mouse Body-Map Groupings)**
    > Surana P, Dutta P, Papineni N, Sathian R, Zhou Z, Liu H, Davuluri RV. **TSProm: deep learning framework to predict tissue-specific regulatory logic.** *NAR Genomics and Bioinformatics* 2026;8(2):lqag050. 
    > 🔗 [doi:10.1093/nargab/lqag050](https://doi.org/10.1093/nargab/lqag050)

*   **STPCaT (Solid Tumors Pan-Cancer Transcriptome)**
    > Surana P, Obusan M, Davuluri RV. **Solid Tumors Pan-Cancer Transcriptome: Tissue/Cancer specific expression groups at the isoform level.** *bioRxiv* 2026. 
    > 🔗 [doi:10.64898/2026.05.04.722705](https://doi.org/10.64898/2026.05.04.722705) *(CC-BY-NC 4.0)*

---

### 🌐 Software & Databases

*   **TransTEx Database:** [Database Link](https://bmi.cewit.stonybrook.edu/transtexdb/)
*   **TransTEx R Package:** [GitHub Repository](https://github.com/pallavisurana1/TransTEx)

---

### 📊 Underlying Source Data

The datasets curated here are derived from the following foundational resources:

| Data Type | Source Resource |
| :--- | :--- |
| **Human Normal Tissue** | GTEx Consortium (Version 8) |
| **Cancer Tissue** | TCGA Solid Tumors (via UCSC Xena) |
| **Mouse Tissue** | Mouse Body Map (grouped via TSProm) |
  
