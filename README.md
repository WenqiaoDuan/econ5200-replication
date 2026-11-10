# Replicating Lee (2008), "Randomized Experiments from Non-random Selection in U.S. House Elections"

> **Template note, delete before you submit.** This is the ECON 5200 replication template.
> Replace every line that starts with `TODO:`. The grader clones this repository into an
> empty directory, builds the environment from `requirements.txt` and runs the one command
> below. The number this README claims must be the number that run produces.

## The paper and its headline claim

- **Paper:** Lee, D. S. (2008). Randomized experiments from non-random selection in U.S. House elections. *Journal of Econometrics* 142(2): 675–697.
- **Identification strategy:** sharp regression discontinuity on the Democratic margin of victory in the previous election, centred at 50 percent of the two-party vote. Treatment is having won that previous election.
- **Headline claim:** a party that narrowly wins a U.S. House election takes about 7.7 percentage points more of the two-party vote in the following election (Table 2, column 1).
- **My replication:** **8.61 percentage points** (HC1 s.e. 0.69, N = 13,566) against the paper's 7.7, a gap of **+11.9%**, exactly as `python reproduce.py` prints it.

## Reproduce the headline table

Python 3.11 or newer. From the repository root:

```bash
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python reproduce.py
```

`python reproduce.py` is the one command. Once `MY_PAPER` is set in `download_data.py`,
it downloads the data if `data/` does not have it, runs `notebooks/01_positioning_and_replication.ipynb` and then
`notebooks/02_robustness.ipynb` top to bottom in a fresh kernel, and prints the headline
table from `output/headline_table.csv`. Executed copies of the notebooks, with their
outputs, go to `output/executed/`.

- **Expected runtime:** about 5 seconds for the two notebooks once the environment is built (measured on a laptop from a clean clone); allow roughly a minute more for `pip install` and the 7 MB data download on the first run.


## Data: source and licence

- **Source:** `https://raw.githubusercontent.com/scunning1975/mixtape/master/lmb-data.dta`, downloaded by `download_data.py`. The file is the U.S. House elections panel compiled by Lee, Moretti and Butler (2004), *Quarterly Journal of Economics* 119(3): 807–859, from election returns for 1948–1990.
- **Included or downloaded:** **downloaded, not committed.** `.gitignore` keeps `data/*.dta` out of the repository, and `download_data.py` fetches the file on the first run. The mixtape repository is under an MIT-style licence that would permit committing the file with its notice, but it is 7 MB of third-party data and there is no need to carry it in version control; the download keeps the repository small and the provenance explicit. The command to fetch it by hand is `python download_data.py --paper lee`.


The template downloads by default: `.gitignore` excludes `data/*.dta`, and
`download_data.py` fetches the files on the first run. Two facts to check before you
decide:

- The five files from `scunning1975/mixtape` (castle, card, lee, hansen, abortion) are in a
  repository under an MIT-style licence that permits copies if its notice is kept. The
  underlying data were collected by the original authors.
- The Dehejia-Wahba files on `users.nber.org/~rdehejia` state no licence. Download them;
  do not commit them.

If you decide to include the data, delete the `data/*.dta` line from `.gitignore`, commit
the files with the licence notice, and say so above.

## Repository map

| Path | What it is |
|---|---|
| `reproduce.py` | The one command: runs the notebooks in name order, prints the headline table |
| `download_data.py` | Data URLs for the six papers; `python download_data.py --paper card` fetches one into `data/` |
| `notebooks/01_positioning_and_replication.ipynb` | Sections 1 and 2: positioning notes, the replication, the theirs-vs-mine table, the discrepancy log. **No AI.** |
| `notebooks/02_robustness.ipynb` | Section 3: four robustness exercises. AI allowed, logged in `ai-appendix.md` |
| `output/headline_table.csv` | The theirs-vs-mine table, written by notebook 01 |
| `output/` | Every table and figure the report uses |
| `report/` | The report PDF |
| `ai-appendix.md` | P.R.I.M.E. entries and full transcripts for Sections 3 to 6, and the no-AI statement for Sections 1 and 2 |
| `AUDIT.md` | How to run the peer audit you file on a classmate's repository |
| `requirements.txt` | Pinned package versions |

TODO: add a row for every file you add.

## Use of AI

Sections 1 and 2 were completed without AI. 

TODO: list the sections where you used AI (from 3, 4, 5 and 6), for what, and point to the
entries in [`ai-appendix.md`](ai-appendix.md). If you used none, say so.
