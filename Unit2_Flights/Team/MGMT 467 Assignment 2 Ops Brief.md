MGMT467 Group 7

Assignment 2 \- Ops Brief

# **Model A: Pre-Departure Diversion Risk — Baseline vs. Engineered**

**Objective.** Establish an early signal for flight diversion risk using only schedule-level (pre-departure) data; Model A serves as the no-real-time baseline (BigQuery ML LOGISTIC\_REG).  
**Class imbalance.** Diversions are rare (≈0.23%: 4,590 of \~1.96M). Any metric at a default 0.5 threshold will look “good” on accuracy but fail to surface true positives.

## **Baseline:**

* **Discrimination/Calibration:** ROC AUC **0.7919**; Log Loss **0.01586** → pre-departure signals carry real predictive power and probabilities are reasonably calibrated.  
* **Default 0.5 threshold:** Accuracy **0.9976** but **Precision 0.172**, **Recall 0.0055**, **F1 0.0107**. Confusion counts: **TP 7**, **FP 15**, **FN 938** → operationally unacceptable miss rate.  
* **Custom threshold 0.05 (ops-tuned):** **TP 34** (↑), **FP 362** (↑), **FN 941** (still high).  
  **Justification:** We trade extra false alarms for fewer costly misses because **FN ≫ FP** in operational cost (reactive scrambles, passenger disruption, regulatory risk). This threshold better aligns model behavior with real-world stakes, even if PPV drops.

## **Engineered Model:**

* **Discrimination/Calibration:** ROC AUC **0.7877**; Log Loss **0.01571**.  
  *Context:* This is **much higher than an earlier simple baseline (AUC 0.7097)** and **comparable to Model A (0.7919)**, indicating stronger foundational signal from feature engineering.  
* **Default 0.5 threshold:** **Precision 1.0**, **Recall 0.00327**, **F1 0.00652**, **Accuracy 0.9977** → extremely conservative: few alerts, but when it alerts, it’s right.

## **Takeaways for operations:**

* **Use probabilities, not hard 0.5.** Threshold tuning is mandatory under extreme imbalance. The **0.05** cut for Model A meaningfully increases actionable heads-ups, aligned with asymmetric costs.  
* **Engineered model has better “shape” for tuning.** With AUC \~0.79 and tighter log loss, it should yield **higher recall at acceptable FP** once we set an ops-driven threshold (e.g., optimize for expected disruption cost).

# **Model B: Day of ops uplift (global \+ engineered)** 

- **Goal:** quantify value of near-departure signals  
- **Uplift Drivers:**  
  - **Adding operational signals**   
    - Captures real-time flight conditions, providing actionable predictive power beyond static schedule features.  
  - **Creating Categorical dep\_delay\_bucket feature**   
    - Converts raw delay minutes into interpretable risk tiers (early/on-time/minor/moderate/major), helping the model learn nonlinear diversion risk.  
  - **Scaling numerical features**   
    - Helps the model converge better and reduces skew from large-delay outliers.  
- **Model Results:**  
  - **Confusion matrix shows the model is conservative**, predicting “diverted” only when highly confident (very few false positives, but many false negatives).  
  - **ROC AUC \~0.80**, indicating the model meaningfully ranks high-risk flights above low-risk ones despite the imbalance.  
- **Model B vs Model A Performance**  
  - **Model B adds operational delay features**, giving it more real-time predictive signal than Model A’s purely schedule-based inputs.  
  - **Higher precision in Model B**, meaning its positive predictions (diversions) are more accurate than Model A’s.  
  - **ROC AUC is higher in Model B**, indicating stronger ability to separate risky from non-risky flights.

**MODEL C \- Localized Model (Hub/Route Segment)**

**Goal:**  
 **Test the value of localized modeling on high-traffic operational hubs (ATL, ORD, JFK), where diversion risk may differ from the global average.**

**Uplift Drivers:**

* Focuses model learning on specific airport conditions (traffic, weather, routing complexity), testing if local specialization improves prediction accuracy.

* Retains operational signals and delay buckets to isolate the effect of localization rather than feature changes.

* Evaluates whether subgroup-specific distributions improve model calibration and threshold performance relative to global model behavior.

**Model Results:**

* ROC AUC \= 0.7666, slightly below Model B’s 0.7792 on the same ATL/ORD/JFK subset — indicating the global model generalizes slightly better.

* Confusion matrix shows extreme conservatism: zero positive predictions at threshold 0.5, resulting in high precision but very low recall (0.0049).

* Accuracy remains high (0.9978) due to the overwhelming majority of non-diverted flights, masking poor minority class detection.

**Model C vs Model B Performance:**

* Model B outperforms Model C in AUC and slightly lowers false negatives, suggesting global signal strength outweighs local specialization.

* Model C’s localized training reduces false positives (0 vs 1\) but increases false negatives (235 vs 199), reinforcing that the subgroup model under-predicts diversions.

* Calibration gap persists—neither model identifies positive cases effectively at the default threshold, implying the need for threshold tuning or resampling methods.

**Model D \- Threshold & Cost/Fairness Policy**

After comparing the performance metrics of the first three models, we identified the best-performing model for threshold optimization based on cost considerations. In this model, a False Positive (predicting a diversion that doesn’t occur) carries an estimated cost of $1,000, mainly due to unnecessary resource allocation and operational disruptions. A False Negative (failing to predict a diversion that does occur) is far more costly—approximately $6,000—because it involves unplanned gate assignments, passenger rebookings, compensation, and decreased customer satisfaction.

During our analysis, we observed that this selected model showed little to no fluctuation in False Negatives across different threshold values, while False Positives fluctuated significantly as the threshold changed. This pattern suggested that adjusting the threshold primarily impacted the number of False Positives rather than False Negatives. As a result, we determined that an optimal threshold of 0.92 minimizes total costs, resulting in an estimated total cost of $5,385,000.

