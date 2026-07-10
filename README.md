# Expression Specificity Atlas — static DuckDB-WASM explorer

A single-page site that lets anyone (no coding) filter gene/protein
expression-specificity classifications across **human tissue**, **mouse
tissue**, and **cancer**, then download the filtered set as CSV. All querying
runs in the visitor's browser via [DuckDB-WASM](https://duckdb.org/docs/api/wasm/overview)
reading one Parquet file. No server, no backend, free to host.

## Files
| file | what it is |
|---|---|
| `index.html` | the web app (loads DuckDB-WASM from a CDN, queries the parquet) |
| `atlas.parquet` | the data — one tidy long table, columns below |
| `make-data.py` | regenerates `atlas.parquet` (pyarrow); swap in your real Excel here |

Schema (one row = one gene × one context):
`gene_id, symbol, species, domain, context, specificity_class, value`

## Run locally
Browsers block `fetch`/WASM on `file://`, so serve the folder over http:
```bash
cd this-folder
python3 -m http.server 8000
# open http://localhost:8000
```

## Deploy free on GitHub Pages
1. Put `index.html` and `atlas.parquet` in a repo (root, or a `/docs` folder).
2. Repo **Settings → Pages → Build and deployment → Deploy from a branch**.
3. Source: your branch, folder `/root` (or `/docs`). Save.
4. Visit `https://<you>.github.io/<repo>/`.

That's the whole hosting story — $0, no account beyond GitHub.

## Using your real data
1. `pip install pandas pyarrow`
2. In `make-data.py`, replace the dummy block with
   `df = pd.read_excel("your_atlas.xlsx", sheet_name="long")` — keep the same
   seven column names.
3. `python make-data.py` → overwrites `atlas.parquet`. Commit and push.

If your file grows past ~30–50 MB, don't commit it into the repo. Attach it as
a **GitHub Release asset** and change the `PARQUET` constant near the top of the
`<script>` in `index.html` to the release download URL.

## Note on the bundled parquet
`atlas.parquet` here was produced by a minimal fallback encoder (uncompressed,
PLAIN) because the machine that built it had no pyarrow and no network. It is
valid and DuckDB reads it. For anything real, regenerate with `make-data.py`
so you get compression and the standard toolchain.
