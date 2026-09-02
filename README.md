# TransTEx expression groupings 
## (human · mouse)

A browser tool for looking up **TransTEx** transcript
expression-group classifications across **human tissues (GTEx)** and a **mouse
body map**, and downloading any filtered slice as CSV. The browser app reads
`TransTEx_dataset.parquet`. Cancer data will be added separately later.

Available: https://pallavisurana1.github.io/TransTEx_datasets/

## What's in it

The data comes from the TransTEx scoring method, which assigns every transcript
to one expression group per resource based on how many tissues it is reliably
expressed in.

**Normal tissues (human GTEx, mouse body map)** — five groups:

| Class | Meaning |
|---|---|
| `TSp` | Tissue-Specific — reliably expressed in a single tissue |
| `TEn` | Tissue-Enhanced — expressed in 2 tissues up to 50% of tissues |
| `Wide` | Widespread — expressed in more than 50% of tissues |
| `Low` | Low or less expression — below the specificity threshold, some expression |
| `Null` | No / minimal expression across all tissues |

Everything is at **transcript / isoform level**, mapped to genes.

## Using the browser tool

Choose any number of tissues from **Tissues** and expression groups from
**Categories**; then optionally
filter by species or transcript/gene. Leaving a multi-select empty means “all”.

Results and CSV downloads are collapsed to one row per transcript and species.
When the same transcript has more than one matching category or tissue,
the distinct values are shown as comma-separated lists. This keeps, for example,
multiple relevant tissues for the same transcript on one row.

## Schema

The Parquet file uses this schema before the browser aggregates matching
records for display and export:

`transcript, gene_id, gene_name, tissue, category, species`

- `tissue` — the tissue (e.g. `testis`, `liver`); it may be empty for
  non-tissue-specific categories
- `category` — the expression group (`TSp`/`TEn`/`Wide`/`Low`/`Null`)
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
| **Mouse Tissue** | Mouse Body Map (grouped via TSProm) |
  
