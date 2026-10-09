# Lab 2 · Can one pre-race feature improve the top-10 prediction?

Pair copy of the Thursday v3 `Pipeline` notebook (Week 4). We test one candidate feature,
`estimated_grid_position = qualifying_position + grid_penalty`, in a controlled with/without comparison.

**Contributors:** Agustín Reyes Pereira · Andy Villarroel

> Invented teaching dataset. Results say nothing about real Formula 1 performance.

## Files

| File | Purpose |
|---|---|
| `W04_Thu_Pipelines_Pair_v3.ipynb` | Our notebook. Sections 1–8 are the original Week 4 student notebook (unchanged); Sections 9–14 are the lab work. Saved with outputs from Restart & Run All. |
| `w04_race_weekends_synthetic_v3.csv` | Synthetic data: 18 weeks × 20 drivers = 360 rows. |

## Split (not changed)

| Period | Weeks | Rows | Use |
|---|---|---|---|
| Train | 1–10 | 200 | Fit every pipeline and the dummy |
| Validation | 11–14 | 80 | Compare candidates (balanced accuracy) |
| Reserved test | 15–18 | 80 | **Sealed. Not scored in this lab.** |

## Result

| Model | Validation balanced accuracy |
|---|---|
| Week 4 dummy baseline (`most_frequent`) | 0.5000 |
| Pipeline without feature | 0.8625 |
| Pipeline with `estimated_grid_position` | 0.8625 |

**Decision: reject.** 0 of 80 validation predictions changed. The feature is an exact linear sum of two
inputs the logistic regression already has, so it adds no information. Details in notebook Section 12.

## Contributions

| Member | Work |
|---|---|
| **Andy Villarroel** | Feature proposal and pre-race availability check (Section 9); `estimated_grid_position` creation with leakage assertions (Section 10); reproducibility runbook and package versions (Section 14); this README. |
| **Agustín Reyes Pereira** | Controlled with/without comparison, dummy baseline and coefficient check (Section 11); decision and limitations (Section 12); AI recommendation audit (Section 13). |

Both of us reviewed the final notebook after Restart & Run All and agreed on the decision.

## Setup

Tested on Windows 11 (Python 3.14.3, pandas 2.3.1, numpy 1.26.4, scikit-learn 1.8.0) and on macOS
(Python 3.14.6, pandas 3.0.6, numpy 2.5.3, scikit-learn 1.9.1) with the same scores. The saved outputs come
from the macOS run; with numpy 2 some printed numbers show as `np.float64(...)`, same values.
Other recent versions should work; scores could differ slightly with a different scikit-learn.

```bash
# from this folder
python -m venv .venv
# Windows:  .venv\Scripts\activate      macOS/Linux:  source .venv/bin/activate
pip install pandas numpy scikit-learn jupyter
```

## Run

**Option A — Jupyter (interactive)**

```bash
jupyter notebook W04_Thu_Pipelines_Pair_v3.ipynb
```

Then choose **Kernel → Restart & Run All**.

**Option B — headless (same as Restart & Run All)**

```bash
python -m nbconvert --to notebook --execute --inplace W04_Thu_Pipelines_Pair_v3.ipynb
```

The notebook must sit in the same folder as the CSV, or the first code cell raises `FileNotFoundError`.

## How to check it worked

1. All code cells ran in order (execution counts 1–12), with no errors.
2. Section 11 prints a three-row table: **0.5000 / 0.8625 / 0.8625**.
3. Section 11 prints `Validation rows where the two pipelines disagree: 0 of 80` and
   `Reserved test rows scored in this lab: 0`.
4. Section 14 prints the package versions used.

All models use `random_state=42`. Nothing else is random, so the scores should repeat exactly.

