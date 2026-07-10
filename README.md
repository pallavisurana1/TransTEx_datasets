# TransTEx-related expression groupings 
## (human · mouse · cancer)

A browser tool for looking up **TransTEx** transcript
expression-group classifications across three resources — **human tissues
(GTEx)**, a **mouse body map**, and **solid-tumor cancers (TCGA solid tumors)** —
and downloading any filtered slice as CSV.

Available: https://pallavisurana1.github.io/TransTEx_related_datasets/

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
across cancer types, giving `CanSp`, `CanEn`, `CanWide`, `CanLow`, `CanNull`,
plus the two cross-resource biomarker groups: `CanHigh` (high in cancer, lost in
normal — oncogenic-like ) and `NorHigh` (high in normal, lost in
cancer — Tumor suppresor: TSG-like).

Everything is at **transcript / isoform level**, mapped to genes.

## Schema

One row = one transcript × one context (tissue or cancer type):

`transcript_id, gene_id, symbol, species, domain, context, class, value`

- `domain` — one of `human_tissue`, `mouse_tissue`, `cancer`
- `context` — the tissue (e.g. `testis`, `liver`) or cancer type (e.g. `GBM`, `OV`)
- `class` — the expression group (`TSp`/`TEn`/`Wide`/`Low`/`Null` for tissues;
  `CanSp`/`CanEn`/`CanWide`/`CanLow`/`CanNull` for cancer)
- `value` — mean expression (TPM/nTPM) for that transcript in that context

> Adjust these columns to match your actual grouping tables. If you also carry
> transcript biotype (`protein_coding`, `lncRNA`, …) or the `CanHigh`/`NorHigh`
> flags, add them as extra columns — the app will pick up any column for
> display and filtering with a small edit.

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
  
