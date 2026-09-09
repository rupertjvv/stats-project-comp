# STA 244 — AF Regression Project 2026

Multiple linear regression model that predicts second-hand vehicle **price** (ZAR)
from a vehicle's characteristics, for an online marketplace's automated pricing tool.

**[View the report (PDF)](https://github.com/rupertjvv/stats-project-comp/blob/main/S244_Regression_Project_2026.pdf)** —
if the inline preview doesn't load, use the
[raw download](https://raw.githubusercontent.com/rupertjvv/stats-project-comp/main/S244_Regression_Project_2026.pdf).

## Contents

| File | Description |
|------|-------------|
| `S244_Regression_Project_2026.Rmd` | Full analysis (EDA → model building → diagnostics → interpretation → predictions). Knit to PDF. |
| `S244_Regression_Project_2026.pdf` | Knitted submission (≤ 6 pages). |
| `competition_predictions.csv` | Test-set price predictions for the competition. |
| `Assignment Information and Data sets-20260907/` | Project brief and the train/test data. |

## Approach (v1)

- Response modelled on the **log scale** (price is right-skewed; stabilises variance,
  linearises age/mileage effects, keeps predictions positive).
- Dropped `listing_id` (identifier), `model_year` (collinear with `vehicle_age`), and
  `colour` + `warranty_months` (not significant).
- **80/20 train/validation split** (`set.seed(244)`) with RMSE as the primary metric.
- Final model: reduced additive model + quadratic `vehicle_age` & `mileage`
  + `segment × age` interaction, with log-normal back-transform correction.
- Validation RMSE ≈ **R33,822** (median price ≈ R141,500).

## Reproducing

Requires R (≥ 4.6) with `dplyr`, `ggplot2`, `ggpubr`, `scales`, `car`, `nortest`, `leaps`.
Open in RStudio and **Knit**, or:

```r
rmarkdown::render("S244_Regression_Project_2026.Rmd")
```
