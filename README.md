# Replicating Lee (2008): Randomized Experiments from Non-random Selection in U.S. House Elections

**Wenqiao Duan | ECON 5200 Midterm Replication Study | November 19, 2026**

Repository: https://github.com/WenqiaoDuan/econ5200-replication

## The paper and its headline claim

- **Paper:** Lee, D. S. (2008). Randomized experiments from non-random selection in U.S. House elections. *Journal of Econometrics*, 142(2), 675–697.
- **Identification strategy:** Sharp regression discontinuity design (RDD). Treatment is winning the previous election. In my replication, the running variable is the previous Democratic two-party vote share minus 0.5, with a cutoff of zero. Identification requires continuity of potential outcomes at the cutoff.
- **Headline claim:** Narrowly winning a U.S. House election increases the party's vote share in the next election by approximately 7.7 percentage points (Table 2, Column 1).
- **My replication:** **8.61 percentage points** (HC1 SE: 0.69 percentage points; N = 13,566), a difference of **+0.9126 percentage points (+11.85%)** relative to the original estimate.

| Statistic | Lee (2008) | My replication |
|---|---:|---:|
| RD estimate | 0.0770 | 0.086126 |
| Advantage (percentage points) | 7.70 | 8.61 |
| Standard error (vote-share units) | 0.0110 | 0.006908 (HC1) |
| Observations | 6,558 | 13,566 |
| Data coverage | 1946–1998 | 1948–1990 |

The baseline uses OLS with separate fourth-order polynomials on either side of the cutoff, a rectangular kernel, a bandwidth of 0.5, and HC1 heteroskedasticity-robust standard errors. I reproduce the direction of the original finding but not its exact magnitude. Differences in sample coverage, running-variable definitions, and inference methods limit direct comparability.

## Reproduce the headline table

From the repository root, set up the Python environment (Python 3.11 or newer, as specified in the repository template):

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

Reproduction command for Table 1:

```bash
jupyter nbconvert --to notebook --execute notebooks/01_positioning_and_replication.ipynb
```

- **Expected runtime:** approximately 25 seconds, as reported in Section 6 of the replication report.
- **Expected result:** RD estimate = 0.0861; HC1 SE = 0.0069; N = 13,566.
- **Environment:** Exact package versions are recorded in `requirements.txt`.

I tested the reproduction command after cloning my repository into an empty directory and installing the required packages. The results matched Table 1 in my report.

## Data: source and licence

- **Dataset:** `lmb-data.dta`, associated with Lee, Moretti, and Butler (2004), *Quarterly Journal of Economics*, 119(3), 807–859.
- **Source:** https://raw.githubusercontent.com/scunning1975/mixtape/master/lmb-data.dta
- **Sample:** U.S. House elections covering 1948–1990. I excluded 22 observations with missing `demvoteshare` or `lagdemvoteshare`, leaving 13,566 observations.
- **Availability:** The data are downloaded rather than committed to the repository. The `download_data.py` script retrieves the dataset from the source above. This avoids redistributing third-party data directly.
- **Licence:** The repository template identifies the upstream Mixtape repository as having an MIT-style licence. The underlying election data were collected by the original authors.

To download the data manually, the template provides:

```bash
python download_data.py --paper lee
```

The course dataset differs from Lee's original sample. In particular, 1952, 1962, 1972, and 1982 are missing within the replication period. The available data do not establish how much these differences explain the discrepancy in the headline estimates.

## Robustness and main findings

| Exercise | Result |
|---|---|
| MSE-optimal bandwidth (0.075) | 9.07 pp; conventional SE 0.57 pp; approximate 95% CI [7.95, 10.19] pp |
| Alternative bandwidths (0.25, 0.50, 1.00) | 9.53, 8.61, and 8.61 pp; robust p-values below 0.001 |
| Local quadratic model | 8.83 pp; reported SE 0.73 pp; p < 0.001 |
| Density test at zero | t = 0.603; p = 0.546 |
| Placebo cutoffs (−0.1, +0.1) | −0.64 pp (p = 0.471); −1.00 pp (p = 0.387) |
| Temporal heterogeneity | Estimates range from 1.96 to 15.18 pp across decades; the 1940s estimate is not statistically significant |
| Alternative outcome: Democratic victory | 42.50 pp; SE 2.53 pp; robust p < 0.001 |
| Covariate continuity checks | Approximately zero jumps for `lagdemvs2`, `lagdemvs3`, and `lagdemvs4`; variable definitions require confirmation |

Here, pp denotes percentage points.

## Does the finding hold?

Lee's main finding largely holds. The estimated incumbency advantage remains positive and statistically significant across the tested bandwidths and polynomial specifications. The density and placebo tests do not show statistically significant discontinuities, but they do not establish that all identifying assumptions are satisfied.

The magnitude varies across decades, although I did not formally test these differences. Incomplete sample coverage, different standard-error methods, and the small 1990s subsample also limit interpretation. The conclusion applies primarily to close elections near the cutoff, rather than all elections.

## Repository map

| Path | Description |
|---|---|
| `reproduce.py` | Full reproduction runner described in the repository template |
| `download_data.py` | Downloads the course dataset |
| `notebooks/01_positioning_and_replication.ipynb` | Sections 1 and 2: positioning, direct replication, comparison table, and discrepancy log. No AI assistance |
| `notebooks/02_robustness.ipynb` | Section 3: robustness and sensitivity exercises |
| `output/headline_table.csv` | Headline comparison table, as specified in the template |
| `output/` | Tables and figures used in the report |
| `report/` | Replication report |
| `ai-appendix.md` | P.R.I.M.E. entries, AI transcripts, and no-AI statement for Sections 1 and 2 |
| `AUDIT.md` | Peer-audit instructions described in the template |
| `requirements.txt` | Pinned Python package versions |

## Use of AI

Sections 1 and 2 were completed without AI assistance, as stated in the replication report.

The report identifies [`ai-appendix.md`](ai-appendix.md) as the location of the P.R.I.M.E. entries and full AI transcripts for Sections 3–6. Consult those entries for the specific tasks and extent of AI assistance in each section.

AI was also used to organize and edit this README based on the completed replication report. No new replication code or numerical results were generated during this documentation step.
