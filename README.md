# Lab 2 · Can one pre-race feature improve the top-10 prediction?

Pair copy of the Thursday v3 `Pipeline` notebook (Week 4). We test one candidate feature,
`estimated_grid_position = qualifying_position + grid_penalty`, in a controlled with/without comparison.

**Contributors:** Agustín Reyes Pereira · 

> Invented teaching dataset. Results say nothing about real Formula 1 performance.

## Files

| File | Purpose |
|---|---|
| `W04_Thu_Pipelines_Pair_v3.ipynb` | Our notebook. Sections 1–8 are the original; Sections 9–14 are the lab work. Saved with outputs from Restart & Run All. |
| `W04_Thu_Pipelines_Student_v3.ipynb` | Original notebook (unchanged). |
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

## Setup

Tested with Python 3.14.3, pandas 2.3.1, numpy 1.26.4, scikit-learn 1.8.0 on Windows 11.
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

