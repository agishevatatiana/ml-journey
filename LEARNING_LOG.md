# ML Journey — Learning Log

My daily learning notes and theory reference while training as an ML/AI engineer.

## ML Intro
Decision Tree, training data, prediction target (y), features (X), steps to building and using a model, model validation, mean absolute error (MAE), overfitting & underfitting, Random Forests  → [ML Intro](#2026-07-24)

---

## 2026-07-24
**Topics:** Decision Tree, training data, prediction target (y), features (X), steps to building and using a model, model validation, mean absolute error (MAE), overfitting & underfitting, Random Forests 
**Did:** build and validate model to evaluate the SalePrice of houses

### Decision Tree
Model ...

### Training data
Data that is used to train (fit) the model to predict some target

### Prediction target (y)
The column of the data table that we want to predict

### Features (X)
Columns of the data table that are fed into the model and help it make predictions based on them. The target column should not be among the features.

### Steps to building and using a model:
- Define:
choose the type of model for the task, and decide what the features and the prediction target are
- Train (Fit):
capture patterns from the provided data
- Predict
- Evaluate:
check the accuracy of the model

### Model validation
Answer the question: "Will the model's predictions be close to what actually happens in reality?" To train the model and validate it properly, we should split the training data into data that goes into the model and validation data (train_test_split). There are many metrics used to define model quality — one of them is Mean Absolute Error (MAE), described below.

### Mean Absolute Error (MAE)
Define the error for each row as: error = actual - predicted, take the absolute value of each error, then take the average of those absolute errors. (mean_absolute_error)

### Overfitting & Underfitting
Overfitting: the model follows the points from the training data too precisely and captures spurious patterns that most likely don't exist in other datasets, so when it sees validation data or new data it makes significant errors.

Underfitting: the model fails to capture important patterns and distinctions in the data; this usually happens when it's trained on a small amount of data.

Overfitting and underfitting always exist, and the goal is to find the sweet spot.

For models based on Decision Trees, the sweet spot lies in the correct number of leaf nodes.

### Random Forests
A model that uses many trees and makes predictions by averaging each component tree's prediction (RandomForestRegressor)

**Next:** Pandas

---


## Topic Index
<!-- Add one line per concept as you write it. Links jump to that day's entry. -->
Concept names → [Mon DD](#yyyy-mm-dd)

---

## YYYY-MM-DD
**Topics:** comma-separated list of what this entry covers
**Did:** one line — course, lessons, project worked on.

### Concept name
Explanation in my own words. Two to four lines.
Include the key syntax or parameter if there is one.
*Interview answer:* two sentences I could say out loud under pressure.

### Another concept
Same shape.

**Numbers:** any scores, metrics, or leaderboard results from today.
**Struggled with:** what stayed unclear — this is my review queue.
**Next:** where I pick up tomorrow.

---

## Topic Index
<!-- Add one line per concept as you write it. Links jump to that day's entry. -->
Concept names → [Mon DD](#yyyy-mm-dd)

---

## YYYY-MM-DD
**Topics:** comma-separated list of what this entry covers
**Did:** one line — course, lessons, project worked on.

### Concept name
Explanation in my own words. Two to four lines.
Include the key syntax or parameter if there is one.
*Interview answer:* two sentences I could say out loud under pressure.

### Another concept
Same shape.

**Numbers:** any scores, metrics, or leaderboard results from today.
**Struggled with:** what stayed unclear — this is my review queue.
**Next:** where I pick up tomorrow.

---