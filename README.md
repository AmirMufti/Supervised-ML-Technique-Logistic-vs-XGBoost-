Churn Rate Analysis: 
Churned users exhibit distinct behavioral patterns compared to retained users. Churned users, on average, had more drives, drove longer distances, and spent more time on the road than retained users. Despite their higher activity, these users were more likely to stop using the app.

Average User Behavior:A key insight is that the median values were more representative due to the presence of outliers in the data, which made the median a better measure than the mean. This revealed that churned users had higher engagement metrics (e.g., more sessions per day) than retained users.

Outliers Impact: Identifying and removing outliers was critical to ensure accurate analysis. Without addressing these outliers, the results might have been skewed, particularly regarding user engagement metrics like drives and session frequency.

Device Comparisons: No significant differences were found between iPhone and Android users in terms of churn and retention. This indicates that platform choice is not a driving factor for churn in this case.

Model Performance: Logistic Regression had a reasonable accuracy (83%) but struggled with recall (0.06), meaning it was not effective at predicting which users would churn. XGBoost showed some improvement in recall (0.13), but overall performance remained insufficient for making critical business decisions.

Model Interpretation and Predictive Power: Logistic regression was easier to interpret, highlighting key factors influencing churn. However, tree-based models like XGBoost demonstrated better predictive capabilities, though they still fell short in terms of overall accuracy and recall.
Recommendations for Data and Model Improvements:

Feature Engineering: Further enhancements to the models could be achieved through deeper feature engineering, including data on specific user interactions within the app or drive-level data.

Data Collection: Collecting more detailed data, such as real-time interactions or user journeys, would likely improve the model's performance by offering better insights into churn behavior.
