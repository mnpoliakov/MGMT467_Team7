# Titanic Survival Analysis Summary

This analysis explores the factors influencing survival rates during the Titanic disaster using the `v_titanic_cleaned` dataset in BigQuery.

## Data Preparation

Before conducting the analysis, the data underwent a cleaning process. This involved creating a cleaned view of the original Titanic dataset (`v_titanic_cleaned`) in BigQuery. While the specific steps of the cleaning process are not detailed in this notebook, the analysis was performed on this pre-processed data, which is assumed to have handled missing values and inconsistencies relevant to the columns used in the analysis (passenger class, sex, age, and survival status).

## What was found:

Based on the analysis of survival rates across different passenger demographics, the key findings are:

*   **Passenger Class Disparity:** A significant difference in survival rates was observed based on passenger class. First-class passengers had the highest survival rate (approx. 63%), followed by second-class (approx. 47%), and then third-class passengers (approx. 24%). This highlights the strong impact of socio-economic status on survival likelihood.
*   **Gender Bias in Survival:** There was a stark difference in survival rates between sexes, with female passengers having a significantly higher survival rate (approx. 74%) compared to male passengers (approx. 19%). This aligns with the "women and children first" protocol.
*   **Age Influence on Survival:** Age also played a role in survival. Children (under 18) had the highest survival rate (approx. 54%), followed by adults (18-59, approx. 36%), and then the elderly (60+, approx. 27%). This suggests a prioritization of younger individuals during rescue efforts.

## What changed after validation:

The initial hypotheses generated with AI assistance were validated by executing SQL queries on the dataset. The findings from the queries confirmed the significant influence of passenger class, sex, and age on survival rates as initially hypothesized. The use of a window function in the sex-based analysis provided an additional perspective by explicitly ranking the survival rates, further emphasizing the significant difference between male and female survival. The SQL queries were refined based on the prompts to Gemini to ensure they accurately calculated the average survival rates for the defined groups.

## What is proposed:

While this is a historical dataset, the insights gained can inform hypothetical recommendations for emergency situations:

1.  **Prioritization of Vulnerable Groups:** Future emergency and evacuation protocols should explicitly prioritize vulnerable populations, including women, children, and individuals who might have limited access or resources.
2.  **Equitable Access and Communication:** Ensuring clear, accessible communication and evacuation routes for all individuals, regardless of their social or economic standing, is crucial.
3.  **Targeted Preparedness:** Implementing targeted safety briefings and drills that consider the diverse needs and potential challenges of different demographics can enhance overall preparedness and survival chances in emergency scenarios.

These findings and recommendations underscore the importance of considering social, gender, and age factors in emergency preparedness and response planning.
