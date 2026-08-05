# Housing Prices – Kaggle Intermediate Machine Learning

Predicting home sale prices (Ames, Iowa dataset) using xgboost library and scikit-learn

## Problem
Regression: predict `SalePrice` from house features.

## Approach
- **Missing values** (`notebook-missing-values.ipynb`): numeric-only RandomForestRegressor baseline; compared dropping columns with missing values vs. `SimpleImputer` (mean/median/most_frequent)
- **Categorical variables** (`notebook-categorical-variables.ipynb`): compared dropping categorical columns vs. ordinal encoding vs. one-hot encoding (low-cardinality one-hot + ordinal for the rest)
- **Pipeline + cross-validation** (`notebook-pipeline.ipynb`): bundled numerical imputation and categorical encoding into a `ColumnTransformer`/`Pipeline`; added engineered features (`TotalSF`, `HouseAge`, `TotalBath`); used 5-fold CV to sweep `n_estimators` for RandomForestRegressor
- **XGBoost** (`notebook-xgboost.ipynb`): switched model to `XGBRegressor` with early stopping; dropped known Ames outliers (`GrLivArea` > 4000 & `SalePrice` < 300000); ordinal-encoded the Po/Fa/TA/Gd/Ex quality columns to preserve scale order; ran a CV ablation to pick engineered features (added `RemodAge`, `OverallQual × GrLivArea`, `GarageAge` on top of the original three); tuned `max_depth`, `min_child_weight`, `subsample`, `colsample_bytree` via repeated (5×5) CV

## Results
**Numbers:** best mae 13468.39213 for XGBoost, position 132 on leaderboard
**Struggled with:** defining best parameters for XGBRegressor, missing numerical variables and missing categorical variables in features (different missing in training and test data)


## Links
- [Course](https://www.kaggle.com/learn/intermediate-machine-learning)
- [Competition](https://www.kaggle.com/competitions/home-data-for-ml-course/leaderboard#)