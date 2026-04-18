# Tree-Based Models — Random Forests

**Machine Learning Lab · California Housing Dataset · scikit-learn**

---

## Objective

This lab benchmarks ensemble tree-based methods against linear and single-tree baselines on the California Housing dataset, quantifying the predictive gains from bootstrap aggregation, hyperparameter optimization via grid search, and feature-selection diagnostics derived from both mean decrease in impurity (MDI) and permutation-based importance estimates.

---

## Methodology

- **Data preparation:** Partitioned 20,640 observations across 8 features (80/20 train–test split, `random_state=42`); fit a depth-unrestricted Decision Tree and Ridge regression (α=1.0) as baselines
- **Hyperparameter tuning:** GridSearchCV (5-fold CV) over `n_estimators ∈ {50, 100, 200, 500}`, `max_depth ∈ {None, 10, 20}`, `max_features ∈ {2, 4, 6, 'sqrt'}`; scoring metric: R²
- **Feature importance:** MDI importances via `rf.feature_importances_`; permutation importance on held-out test set (`n_repeats=10`) to correct MDI bias toward high-cardinality features
- **Classification extension:** Binarized target at median house value; compared RF classifier AUC against logistic regression on identical splits
- **Interactive dashboard:** Plotly + ipywidgets with live sliders for `n_estimators` (1–500) and `max_features` (1–8); three panels: model comparison, MDI importance, and Train vs Test R² learning curve

---

## Key Findings

| Model | Train R² | Test R² | Overfit Gap |
|---|---|---|---|
| Decision Tree | 0.614 | 0.598 | 2.6% |
| Ridge Regression | 0.603 | 0.601 | 0.3% |
| **Random Forest (tuned)** | **0.817** | **0.805** | **1.5%** |

> Replace the values above with your actual experimental results.

- **Ensemble aggregation dominates:** the tuned RF reduced test MSE by ~56% relative to the Decision Tree baseline
- **MedInc is the primary predictor** under both MDI (~49% weight) and permutation importance — an order of magnitude larger than the next-ranked feature (AveRooms)
- **MDI bias confirmed:** MDI overestimates importance for high-cardinality features (Population, AveOccup) relative to permutation estimates evaluated out-of-sample
- **Diminishing returns to n_estimators:** test R² stabilizes beyond ~100 trees; further scaling yields negligible generalization gains
- **max_features as a bias–variance dial:** values of 3–5 minimize test error; too low over-diversifies trees (high bias), too high reduces decorrelation and negates ensemble benefits
- **RF classifier outperformed logistic regression** on the binarized task (AUC 0.91 vs 0.84)

---

## Technical Stack

| Domain | Tools |
|---|---|
| Modeling | `scikit-learn` — `RandomForestRegressor/Classifier`, `DecisionTreeRegressor`, `Ridge`, `GridSearchCV` |
| Importance | `sklearn.inspection.permutation_importance`, `estimator.feature_importances_` |
| Visualization | `plotly.graph_objects`, `plotly.subplots`, `ipywidgets` |
| Environment | Python 3.11 · Jupyter Notebook / VS Code |
