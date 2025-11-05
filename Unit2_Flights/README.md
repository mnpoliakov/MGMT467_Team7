# ✈️ Unit 2: Flight Delay Prediction and Classification (BigQuery ML)

This project explores flight data using **BigQuery ML (BQML)** to address key operational questions related to resource planning and disruption response in air travel. We implement both **regression** and **classification** models, focusing on the Unit 2 skills of model training, evaluation, interpretation, and feature engineering.

-----

## 📚 Project Overview

**Alignment:** Labs 4–6 (Regression → Classification → Feature Engineering/Transform)
**Tools Used:** Google Colab, BigQuery SQL, BQML (`LINEAR_REG`, `LOGISTIC_REG`, `ML.EVALUATE`, `ML.PREDICT`, `ML.EXPLAIN_PREDICT`, `TRANSFORM` clause)

### 📊 Dataset

  * **Source:** `bigquery-public-data.faa.us_flights` or `bigquery-public-data.flights`
  * **Schema Note:** We utilize the table matching the Lab 4–6 schema, ensuring access to key fields like `carrier`, `dep_delay`, and `arr_delay`.

### ❓ Business Questions

1.  **Regression (Resource Planning):** Can we estimate **arrival delay minutes (`arr_delay`)** from operational signals to improve resource planning (e.g., gate assignments, staffing)?
2.  **Classification (Disruption Response):** Can we classify the probability a flight is **diverted** to improve disruption response (e.g., preparing ground crew, managing connecting flights)?

-----

## ✅ Required Scope and Deliverables

### 1\. Regression: Arrival Delay Estimation (`arr_delay`)

| Task | BQML Skill | Deliverables |
| :--- | :--- | :--- |
| **Model Training** | `CREATE MODEL` (`LINEAR_REG`) | Model using $\geq 5$ features (e.g., `dep_delay`, `distance`, `carrier`, `origin`, `dest`, `dayofweek`). |
| **Evaluation** | `ML.EVALUATE` | Report $\text{MAE}$ and provide a **business interpretation** of $\text{MAE}$ (how much our prediction is off, on average, in minutes). |
| **Interpretation** | `ML.EXPLAIN_PREDICT` | Show and interpret results for **two hypothetical flights**, highlighting the top features influencing the prediction. |

### 2\. Classification: Flight Diversion Prediction (`diverted`)

| Task | BQML Skill | Deliverables |
| :--- | :--- | :--- |
| **Model Training** | `CREATE MODEL` (`LOGISTIC_REG`) | Model to predict `diverted` (a $\text{BOOLEAN}$ field). |
| **Evaluation** | `ML.EVALUATE` | Report **precision, recall, and the confusion matrix**. |
| **Custom Threshold** | `ML.PREDICT` (with custom threshold logic) | Re-score the test set using a **custom threshold** (e.g., 0.75). **Justify** the choice from an operations (ops) perspective (e.g., cost of False Positives vs. False Negatives). |

### 3\. Feature Engineering (`TRANSFORM` Clause)

| Task | BQML Skill | Deliverables |
| :--- | :--- | :--- |
| **Retraining** | `CREATE MODEL` with `TRANSFORM` | Retrain the classification model incorporating a `TRANSFORM` clause that: <br> (a) **Creates a 'route'** (`origin || '-' || dest`). <br> (b) **Extracts `day_of_week`** from the flight date. <br> (c) **Bucketizes `dep_delay`** (e.g., early/on-time/minor/moderate/major). |
| **Comparison** | Metric Comparison | Compare the metrics (precision, recall, etc.) of the **baseline** vs. the **engineered** model. State if performance improved and provide a **justification (why)**. |

### 4\. Cost & Scale Management

  * **Dev Iterations:** Demonstrate the use of the **`LIMIT`** clause for quick, low-cost model development and iteration.
  * **Final Run Plan:** Document the approach for the "final" run (e.g., trade-offs between using a sample vs. the full table for training).

-----

## 📦 Deliverables Breakdown

### Individual Deliverables (60 points)

| File | Content | Focus |
| :--- | :--- | :--- |
| **`Unit2_<Name>_BQML.ipynb`** | Colab Notebook (in team GitHub) | **Regression** (Train/Evaluate/Explain), **Classification** (Train/Evaluate), **TRANSFORM** retrain + comparison table, **Short ops-oriented interpretation** (precision vs. recall). |
| **`Unit2_<Name>_Summary.md`** | 1-page Markdown Summary | What was learned, where the model failed, and the final classification threshold recommended for deployment. |

### Team Deliverables (40 points)

| File | Content | Focus |
| :--- | :--- | :--- |
| **Ops Brief (PDF)** | 2–3 page PDF document | **Regression:** How $\text{MAE}$ translates to staffing/gate planning. <br> **Classification:** Risk matrix (FP vs. FN) and justification for the chosen threshold. <br> **Future Work:** Feature engineering wins and future ideas. |
| **GitHub Repo** | Clean structure | Clean SQL files, a reproducible Colab environment, and this comprehensive `README.md`. |

-----

## 🛠️ Repository Structure (Recommended)

```
/Unit2_Flight_Delays
├── README.md                 <-- This file
├── /notebooks
│   └── Unit2_<Name>_BQML.ipynb  <-- Individual Colab notebooks
├── /sql
│   ├── regression_baseline.sql
│   ├── classification_baseline.sql
│   └── classification_transform.sql
└── /deliverables
    ├── Ops_Brief.pdf            <-- Team Deliverable
    └── Unit2_<Name>_Summary.md  <-- Individual Summaries
```
