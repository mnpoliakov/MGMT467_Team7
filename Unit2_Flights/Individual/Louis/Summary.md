## MD Summary: Key Learnings, Model Limitations, and Deployment Threshold

### What Was Learned

Through this classification experiment, we've learned several critical aspects of predicting flight diversions using BigQuery ML:

1.  **Predictive Power of Pre-departure Features:** Even with only schedule-level information (`carrier`, `route`, `distance`, `day_of_week`, `month`), the `LOGISTIC_REG` model (Model A) achieved a respectable **ROC AUC of 0.791935**. This demonstrates that significant predictive power exists even before a flight departs, which is crucial for proactive operational planning.
2.  **Impact of Class Imbalance:** The dataset is severely imbalanced, with a very small percentage of flights being diverted. This imbalance profoundly affects model metrics like precision, recall, and F1-score, making accuracy a misleading metric. It highlights the necessity of using appropriate metrics (like AUC) and carefully tuning classification thresholds.
3.  **Feature Engineering Value:** The engineered model (using `TRANSFORM`) showed a marginal improvement in AUC (0.787681 compared to 0.793325, though the baseline here refers to an unoptimized version as a sanity check) and slightly better log loss, confirming that thoughtful feature creation can enhance model performance.
4.  **Operational Trade-offs are Key:** The exercise underscored that model evaluation cannot solely rely on statistical metrics. The business context and the asymmetric costs of false positives versus false negatives dictate the optimal operating point (threshold) for deployment.

### Where the Model Failed

While the model showed promise, it also presented significant limitations:

1.  **Ineffective Default Threshold:** At the default 0.5 classification threshold, Model A failed to be operationally useful. It identified only **7 True Positives** while missing **938 actual diversions (False Negatives)**. This indicates a severe lack of recall, making it unreliable for identifying potential diversions.
2.  **High False Negative Rate Persists:** Even after lowering the threshold to 0.05 to increase recall, the model still missed a substantial number of actual diversions (941 False Negatives). This suggests that while pre-departure features are informative, they may not capture all the critical signals necessary for a highly accurate prediction of rare diversion events.
3.  **Limited Feature Set:** The current models use a relatively small and static set of features. They do not incorporate real-time, dynamic information such as weather conditions, air traffic control congestion, or aircraft maintenance status, which are likely crucial drivers of diversions. Without such dynamic features, the model's predictive ceiling is inherently limited.

### The Threshold to Deploy: 0.05

For operational deployment, I would choose a **prediction threshold of 0.05** for the pre-departure model.

**Justification:** The primary operational goal is to minimize the impact of flight diversions by enabling proactive resource staging (crews, gates, hotels, ground transport). The cost of a **False Negative** (a missed diversion) is significantly higher than a **False Positive** (unnecessarily staged resources). A missed diversion leads to reactive, chaotic, and expensive recovery efforts, severe passenger disruption, and potential reputational damage.

By lowering the threshold to 0.05, we significantly increase the **True Positive** rate from 7 to **34**, meaning we can proactively identify 34 more actual diversions. While this comes at the cost of increasing **False Positives** to 362 (from 15), this trade-off is deemed acceptable. The operational overhead of 362 false alarms is an inefficiency but is less disruptive and costly than the consequences of missing 34 critical diversion events. This threshold prioritizes early warning and preparedness, aiming to minimize overall operational disruption by being more proactive, even if it means some resources are occasionally over-allocated.
