# 🐢 Sea Turtle Rescue: Forecast Challenge (Zindi)

Forecast the weekly number of turtles caught per capture site along the Kenyan coast to help **Local Ocean Conservation (LOC)** plan their staff schedules and budgets more efficiently.

---

## 📘 Overview

Since 1998, **Local Ocean Conservation (LOC)** has worked with local fishers to rescue endangered sea turtles caught as bycatch.  
Each time a turtle is captured, LOC records the event, measures the animal, and releases it safely.  

This challenge aims to **forecast the number of turtles caught per week for each capture site in 2019**, using historical data from 1998–2018.

Accurate forecasts will help LOC:
- Plan staff schedules
- Manage budgets
- Improve the rescue program’s operational efficiency

---

## 📂 Dataset Description

| File | Description | Usage |
|------|--------------|--------|
| **`train.csv`** | Historical turtle rescue data (1998–2018). Each row represents one turtle capture event, including date, capture site, and other variables. | ✅ Main training dataset |
| **`Sample_sub.csv`** | Template submission file with all required IDs for 2019 (format: `CaptureSite_<ID>_<YYYYWW>`). | 📄 Use as reference for your `submission.csv` |
| **`variable_definitions.csv`** | Column descriptions for `train.csv`. | 🔍 Reference only |
| **`CaptureSite_category.csv`** | Metadata mapping each site to its category and type (geographic/hidden groupings). | 🧭 Optional — can be merged for extra features |

---

## 🎯 Objective

Predict:

> The number of turtles caught **per week per capture site** during **2019**.

### Target variable
Weekly count of turtles per `(CaptureSite, Week, Year)`.

### Evaluation metric
Zindi typically used **Mean Absolute Error (MAE)** — lower is better.

---

## 🧠 Approach Summary

1. **Aggregate** `train.csv` to weekly counts per capture site (1998–2018).  
2. **Feature Engineering**:
   - Lag features (1, 2, 3, 4, 52 weeks)
   - Rolling means (4, 8, 12, 52 weeks)
   - Calendar features (week of year sine/cosine)
   - Site category/type from `CaptureSite_category.csv`
3. **Modeling**:
   - Poisson Regression or Gradient Boosting on `log1p(count)`
   - Blocked time-series cross-validation (train ≤2017 → validate on 2018)
4. **Forecasting**:
   - Predict weekly counts for all sites in 2019
   - Format output to match `Sample_sub.csv`

---

## Set up the Environment

### WindowsOS type the following commands :
Install the virtual environment and the required packages by following commands.

For PowerShell CLI :

`pyenv local 3.11.3`

`python -m venv .venv`

`.venv\Scripts\Activate.ps1`

`python -m pip install --upgrade pip`

`pip install -r requirements.txt`



