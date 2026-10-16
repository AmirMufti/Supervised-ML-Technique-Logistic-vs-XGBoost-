# Waze User Churn: Logistic Regression vs XGBoost

Predicting which Waze users will churn (stop using the app), using in-app behaviour such as sessions, drives and distance driven. The project compares an interpretable logistic regression with a gradient-boosted tree model, and is candid about how little either one can predict churn from this data.

**Dataset:** Waze user activity data from Kaggle (a fictional transportation app), 14,999 users, 13 columns. Target: `label`, either `retained` or `churned`.

## The class imbalance matters

| Label | Users | Share |
|---|---|---|
| retained | 11,763 | 82.3% |
| churned | 2,536 | 17.7% |

A model that predicts "retained" for every user scores **82.3% accuracy**, so accuracy alone says little here. Precision, recall and F1 on the churned class are the numbers that matter.

## Results (held-out test set)

| Model | Accuracy | Precision (churned) | Recall (churned) | F1 (churned) |
|---|---|---|---|---|
| Logistic Regression | 0.830 | 0.486 | 0.055 | 0.099 |
| XGBoost (tuned) | 0.813 | 0.360 | 0.134 | 0.195 |

- Logistic regression is more precise but finds only about 5% of churners.
- XGBoost finds about 13% of churners, at the cost of more false alarms and lower accuracy.
- Neither model is good enough to target retention efforts on its own. Both are far better than a random guess on the minority class, but both miss most churners.

The tuned XGBoost settings were learning rate 0.15, max depth 6, min child weight 6 and 400 estimators.

## Key insights

**Churn rate analysis.** Churned users show distinct behaviour from retained users. On average they had more drives, drove longer distances and spent more time on the road. Despite that higher activity, they were more likely to stop using the app.

**Averages vs medians.** The data has strong outliers, so medians are a more representative summary than means. On medians, churned users had higher engagement than retained users, for example more sessions per day.

**Outliers.** Outliers were removed before analysis. Without that step, the engagement results (drives and sessions) would have been skewed.

**Device.** iPhone and Android users churn at almost the same rate (about 18% and 18%), so platform does not appear to drive churn in this data.

**Interpretability vs accuracy.** Logistic regression is easier to explain and points to the factors behind churn. Tree-based XGBoost has somewhat better recall but still falls short of what a business decision would need.

## Recommendations

- **Feature engineering.** Deeper features, such as trends in usage over time or specific in-app actions, are likely to help more than tuning either model.
- **Better data.** Real-time interactions and full user journeys would give the models much more signal about why users leave.
- **Business framing.** Before deploying, decide what a false alarm costs (an unnecessary retention offer) versus a missed churner (lost user), and choose a decision threshold to match.

## Repository contents

| File | Purpose |
|---|---|
| `Waze Project.ipynb` | Full analysis: EDA, outlier handling, logistic regression, XGBoost tuning and evaluation |
| `Waze User Churn Report.docx` | Written project report |

## Reproduce

Open `Waze Project.ipynb`. Requires `pandas`, `numpy`, `scikit-learn`, `xgboost`, `matplotlib` and `seaborn`.
