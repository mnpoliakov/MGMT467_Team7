# ☀️ SolarPredict: UV Index Prediction & Analytics Pipeline

**Project Status:** Active  
**Primary Objective:** Real-time UV Index Forecasting

---

## 📖 Executive Summary & Business Goal

The core business objective of this project is to accurately **predict the UV Index** to drive operational utility and safety insights. By forecasting UV levels, we aim to provide actionable data for outdoor safety advisories, agricultural planning, or energy grid optimization.

To achieve this, we architected a robust data ecosystem that blends historical patterns with live environmental data to feed a predictive Machine Learning model.

---

## 🏗️ System Architecture

Our engineering approach utilizes a hybrid data pipeline to ensure both historical depth and real-time relevance:

### 1. Data Ingestion
* **Batch Processing:** We ingest comprehensive historical weather datasets from **Kaggle** to train our baseline models and identify long-term trends.
* **Streaming Pipeline:** We engineered a real-time ingestion layer connecting to the **Weatherstack API**. This pipeline streams live meteorological data to our warehouse, allowing for up-to-the-minute analysis.

### 2. Machine Learning
* **Model:** We developed an **XGBoost (Extreme Gradient Boosting)** tree model.
* **Target:** The model is tuned to predict **Utility/UV Index** with high accuracey, minimizing error rates against actual observed weather conditions.

### 3. Looker Studio
* **Dashboard** Constanly being updated by our streaming model. Allows for real time weather insights and easy comparissons between major cities.

---

## 📂 Repository Structure & Navigation

Below is a guide to the folder structure of this repository. Use this to locate specific codebases, documentation, and analysis.

### `Final_Project/`

* **`Individual/`**
    * Contains the individual DIVE analysis and contribution logs.(**Louis, Michael, Orion, Sean**).
* **`bq/`**
    * **`sql/`**: Hosted BigQuery SQL ML model.
* **`dashboards/`**
    * **`kpis.md`**: Documentation defining the Key Performance Indicators (KPIs) and metrics used in our reporting.
    * **`Looker Link`**: A provided link to our looker studio dashboard.
* **`docs/`**
    * **`Operational Excellence & Security.md`**: The governance document outlining security protocols, API key management, and operational controls.
    * **`blueprint.md`**: The technical architecture diagram and system blueprint.
    * **`Presentation`**: A slide deck that contains a highlevel overview of our project.
    * **`Video`**: Contains a live team demo of our project from batch to dashboard. https://youtu.be/uCGJEoPEeE0
* **`pipeline/`**
    * **`Batch/`**: Python scripts and logic for ingesting the Kaggle historical datasets.
    * **`Streaming/`**: The complete codebase for the Weatherstack API real-time streaming architecture.
* **`Readme.MD`**: Current project documentation.

---

## 🚀 Getting Started

1.  **View the Architecture:** Navigate to `docs/blueprint.md` to see the system topology.
2.  **Run the Pipeline:** Instructions for initializing the streaming or batch jobs can be found in `pipeline/readme.md`.
3.  **Check the Model:** The logic for the XGBoost training and prediction is located within the `bq/` and analysis folders.

---
