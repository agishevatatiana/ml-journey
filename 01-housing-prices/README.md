# Housing Prices – Kaggle Intro to ML

Predicting home sale prices (Ames, Iowa dataset) using scikit-learn.

## Problem
Regression: predict `SalePrice` from house features.

## Approach
- Data exploration with pandas
- Baseline: DecisionTreeRegressor
- Tuned tree depth to reduce overfitting
- Improved with RandomForestRegressor

## Results
**Numbers:** forest 16461.72616255708 (16255.47473 on Kaggle) and position 528 on leaderboard
**Struggled with:** features to include: missing values issue of the RandomForestRegressor fixed by rewriting to median values


## Links
- [Kaggle notebook](https://www.kaggle.com/code/tanyaagisheva/exercise-machine-learning-competitions)
- [Competition](https://www.kaggle.com/competitions/home-data-for-ml-course/leaderboard#)