# ⚡ Real-Time Weather Streaming Pipeline

**Status:** Operational  
**Source:** Weatherstack API  
**Destination:** Google BigQuery (via Pub/Sub)

---

## 📖 Overview
This directory contains the logic for the **Real-Time Streaming Pipeline**. It acts as the data **Producer**, simulating a Cloud Function that ingests live weather data from 12 global cities, normalizes the JSON payload, and publishes it to the Google Cloud ecosystem.

### 🏗️ Architecture Flow
1.  **Ingest:** Python script requests live data from `api.weatherstack.com`.
2.  **Publish:** Data is serialized and sent to the Pub/Sub topic `weatherstack-data`.
3.  **Process:** Google Cloud Pub/Sub streams the messages directly into BigQuery.
4.  **Store:** Data lands in `weather_data_dataset.new_weather_data` for immediate analysis.

---

## 🔑 API Key & Monthly Usage

**⚠️ Important:** The current implementation uses a **Weatherstack Standard API Key**.

* **Security:** While the key is present in the codebase for the prototype, for production deployment, it must be moved to **Google Secret Manager**.
* **Rate Limiting:** The pipeline includes a forced delay of `1.1 seconds` between requests to strictly adhere to the API's "per-second" request limits.
* **Monthly Quota:** Please refer to `docs/Operational Excellence & Security.md` for the specific monthly call limits and cost alerts associated with this key. **Do not modify the polling frequency** without checking the remaining monthly quota.

---

## ⚙️ Configuration & Constants

To run this pipeline successfully, ensure the following constants are configured:

| Variable | Value | Description |
| :--- | :--- | :--- |
| **GCP Project ID** | `finalproject-480220` | The host project for BigQuery/PubSub |
| **Topic ID** | `weatherstack-data` | The Pub/Sub topic entry point |
| **Dataset ID** | `weather_data_dataset` | The BigQuery Dataset |
| **Table ID** | `new_weather_data` | The final destination table |

---

## 🛠️ Setup & Usage

### 1. Prerequisites
Ensure you have the Google Cloud SDK installed and the following Python libraries:
```bash
pip install google-cloud-pubsub google-cloud-bigquery requests
