# ✈️ MGMT467\_Team7 – Unit 2: Flight Delay Prediction and Classification (BigQuery ML)

Welcome to our team repository for **Unit 2: BigQuery ML Modeling**.

This project implements machine learning models directly within **BigQuery (BQML)** to solve two key operational challenges in aviation: **predicting arrival delays (Regression)** and **classifying flight diversions (Classification)**. We focus heavily on model interpretation, feature engineering using the `TRANSFORM` clause, and operational justification for model choices.

-----

## 📚 Project Overview

The primary goal of this assignment is to:

  * **Train, evaluate, and interpret** BQML models (`LINEAR_REG` and `LOGISTIC_REG`) for both resource planning and disruption response.
  * Demonstrate proficiency with BQML tools, including `ML.EVALUATE`, `ML.PREDICT`, and **`ML.EXPLAIN_PREDICT`**.
  * Improve model performance through **Feature Engineering** using the **`TRANSFORM` clause** (creating `route`, extracting `day_of_week`, and `bucketizing` delays).
  * Synthesize findings into an **operations-oriented brief**, justifying the choice of metrics and thresholds (e.g., MAE, precision/recall trade-off).

### 🛠️ Tools and Dataset

  * **Tools:** Google Colab, BigQuery SQL, BQML (`LINEAR_REG`, `LOGISTIC_REG`, `TRANSFORM` clause).
  * **Dataset:** `bigquery-public-data.faa.us_flights` or `bigquery-public-data.flights`.

-----

## 💻 Individual Analysis (Focus: Execution and Interpretation)

Each team member is responsible for a complete, reproducible BQML workflow, documented in a single Colab notebook.

  * **Folder:** Individual work is contained within the `/individual/[name]/` folder.
  * **Notebook:** `Unit2_<Name>_BQML.ipynb`
      * One complete **Regression** experiment (`arr_delay`): Training, `ML.EVALUATE`, and **`ML.EXPLAIN_PREDICT`** (with interpretation for two hypothetical flights).
      * One complete **Classification** experiment (`diverted`): Training, Evaluation (precision, recall, confusion matrix), and **re-scoring with a custom threshold**.
      * **Feature Engineering:** Retraining the classification model with the **`TRANSFORM` clause** and comparing baseline vs. engineered metrics.
  * **Summary File:** `Unit2_<Name>_Summary.md` (1 page)
      * Reflections on what was learned.
      * Analysis of where the model **failed** (e.g., poor predictions, metric weaknesses).
      * Justification for the **final classification threshold** recommended for deployment.

-----

## 🤝 Team Deliverables (Focus: Operational Strategy)

Team deliverables synthesize the individual findings, providing a collective, actionable report from an operations management perspective.

  * **Folder:** Located in the `/team/` folder.
  * **Ops Brief (2–3 pages PDF):**
      * **Regression Impact:** How the model's **MAE** translates directly to **staffing or gate planning** decisions (business terms).
      * **Classification Strategy:** Detailed **risk matrix** (FP vs FN costs) and a justification for the team's chosen deployment threshold.
      * **Feature Engineering:** Summary of **wins** from using the `TRANSFORM` clause and concrete **future feature ideas**.
  * **Repository Structure:**
      * Clean and well-commented **SQL files** (e.g., separate files for the baseline and TRANSFORM models).
      * A reproducible **Colab** environment.
      * This organized **`README.md`**.

-----
