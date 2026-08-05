# ML Journey — Learning Log

My daily learning notes and theory reference while training as an ML/AI engineer.

## ML Intro - practice folder 01-housing-prices/
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


## Pandas - practice folder 02-housing-eda/
Pandas, DataFrame & Series, Index-based selection, Label-based selection → [Pandas](#2026-07-25)

---

## 2026-07-25
**Topics:** Pandas, DataFrame & Series, Index-based selection, Label-based selection
**Did:** analyse housing data using pandas library

### Pandas
Python library for data analysis

### DataFrame & Series
**DataFrame** - a table, built from an object whose keys are column names and whose values are arrays; the array's indexes are the table's row indexes, and its values are the values of that column:

`pd.DataFrame({'Yes': [50, 21], 'No': [131, 2]})`

|   | Yes | No  |
|---|-----|-----|
| 0 | 50  | 131 |
| 1 | 21  | 2   |

Array indexes can be assigned strings: `pd.DataFrame({'Yes': [50, 21], 'No': [131, 2]}, index=['A', 'B'])`

|   | Yes | No  |
|---|-----|-----|
| A | 50  | 131 |
| B | 21  | 2   |

**Series** - indexed list with name
`pd.Series([30, 35, 40], index=['2015 Sales', '2016 Sales', '2017 Sales'], name='Product A')`

| Index      | Value |
|------------|-------|
| 2015 Sales | 30    |
| 2016 Sales | 35    |
| 2017 Sales | 40    |

*Name: Product A, dtype: int64*

We can think of **Series** as a single-column snapshot of a **DataFrame**, and of **DataFrame** as a bunch of **Series**

### Index-based selection (iloc[:,0])
selecting data based on its numerical position in the data, row - first, column - second; the first element of the range is included and the last one excluded

### Label-based selection (loc[:, ['column1']])
selecting data based on data index value, row - first, column - second, all elements of the range included, use when string indexes

**Next:** [Intermediate ML](https://www.kaggle.com/learn/intermediate-machine-learning)

---

## Intermediate ML - practice folder /03-improved-housing-prices
Dealing with missing values, Categorical Variables, Pipelines, Cross-validation, XGBoost (extreme gradient boosting), Data Leakage
 → [Intermediate ML](#2026-08-05)

---

## 2026-08-05
**Topics:** Dealing with missing values, Categorical Variables, Pipelines, Cross-validation, XGBoost (extreme gradient boosting), Data Leakage

**Did:** Applied learned terms to improve prediction of housing prices model. Received the model with better mae.

### Dealing with missing values
1. A Simple Option: Drop Columns with Missing Values
   The simplest approach is to drop columns with missing values entirely. This way the model loses potentially important data, so it's only a good option if most of the data in that column is missing.

2. A Better Option: Imputation (SimpleImputer from scikit-learn lib)
   Fill the missing values with some number, for example the mean value. This will be inaccurate for some rows, but the model will still be more accurate than if the columns were dropped entirely.

3. An Extension To Imputation
   Impute the values as before, but also add a new column marking which rows had missing values (True) and which did not (False). This can lead to better predictions.


### Categorical Variables (CV)
Variables that accept only a particular list of values — categories — for example car brands (Lexus, Toyota, Tesla, etc.)

1. Drop CV — the easiest way; works okay for columns that don't bring a lot of value to the dataset.

2. Ordinal Encoding (OrdinalEncoder from scikit-learn lib) — each unique value gets its own integer. Sometimes the categories can be assigned integers logically, e.g. Yes - 1, No - 0; "Never" (0) < "Rarely" (1) < "Most days" (2) < "Every day" (3). This type of CV is called an Ordinal Variable.

3. One-Hot Encoding (OneHotEncoder from scikit-learn lib) — works well for variables that cannot be put in order (Nominal Variables) and that have fewer than 15 categories. Each category from the column becomes a new column; rows that had that value get 1, and the rest get 0.

**Cardinality** - the number of unique values in a column

### Pipelines
A way to bundle preprocessing, validation, and modeling steps into a single build, so the whole thing can be used as one step.

Benefits of using pipelines:

1. Automatically keeps track of training and validation data at each step, which helps keep **code cleaner**
2. Reduces the risk of misapplying or skipping a preprocessing step, leading to **fewer bugs**
3. Makes it easier to deploy the model at scale
4. Provides more options for model validation

Building the pipeline:

1. Define preprocessing steps:
    e.g. impute missing values in numerical data, and impute missing values and apply one-hot encoding to categorical data;
    use ColumnTransformer from scikit-learn to bundle these together as one preprocessing step
2. Define the model
    e.g. define a random forest model with the RandomForestRegressor class from scikit-learn
3. Create and evaluate the pipeline
    e.g. use the Pipeline class from scikit-learn to bundle the preprocessing and modeling steps together

### Cross-validation
In **cross-validation**, the modeling process is run on different subsets of the data to get multiple measures of model quality.

For example, we can start by dividing the data into 5 pieces, each 20% of the full dataset. In this case, we say we have broken the data into 5 "folds".
We then run 5 experiments: in the first, we use fold 1 as the validation (holdout) set and everything else as training data; in the second, fold 2 is used as the validation (holdout) set and the rest as the training set; and we repeat this until every fold has served as the validation (holdout) set.

**When to use this approach?**
For small datasets, where the extra computational cost isn't a big deal, you should run cross-validation.

Using cross-validation yields a much better measure of model quality, with the added benefit of cleaning up our code: note that we no longer need to keep track of separate training and validation sets. So, especially for small datasets, it's a good improvement!

### XGBoost (extreme gradient boosting) - xgboost lib
Most effective ensemble method for structured data

**Ensemble methods** — modeling methods that combine the predictions of several models (e.g. several trees, in the case of random forests)

**Gradient boosting steps:**

0. Define the rules for stopping the loop.
1. Start with a naive model, for example based on a single decision tree.
2. After the first prediction is made, calculate the error (e.g. mean squared error).
3. Use the error information to train the next model in the loop, which is added to the ensemble. Model parameters are chosen so that adding this new model reduces the loss. (Learning Rate (α) — a small multiplier, typically between 0.01 and 0.1, used at this step to avoid **overfitting**. XGBoost sets learning_rate=0.1 by default.)
4. Make the next prediction and repeat from step 2, looping until the condition set in step 0 is met.

Step 0 — ways to set the exit rules:
1. The most common stop condition is a hard limit on the number of iterations. You define a parameter called n_estimators (typical values range from 100–1000, depending a lot on the Learning Rate parameter). The loop runs exactly that many times — once the last tree is built and added, the loop stops and the ensemble is complete.

2. Because adding too many trees causes overfitting, data scientists use Early Stopping (**early_stopping_rounds**). You split your data into a Training Set (used to build the trees) and a Validation Set (hidden data used only to test the model's accuracy after each step).
As you add trees, the error on both sets drops. Eventually, the model starts overfitting: the training error keeps dropping, but the validation error stops improving or starts increasing again.
You can configure the model to stop if the validation error doesn't improve for a set number of rounds, using **early_stopping_rounds**. You also need to set aside data for calculating the validation scores — this is done via the **eval_set** parameter.

3. You can set a rule that specifies a target error tolerance: if the remaining errors (residuals) become so small that adding another tree would yield no noticeable benefit, the algorithm stops early because the problem is effectively "solved." (TODO: clarify which tools support this)

### Data Leakage
Happens when information the model shouldn't have access to during training "leaks" in — either data that won't exist yet at prediction time, or data from the test/validation set. The model looks accurate during evaluation, but performs poorly in the real world.

Types of leakage:

1. **Target Leakage** 
    Happens when your training data includes a "cheat code" feature that would not actually exist in the real world when making a prediction. It contains information about the final outcome that you only find out after the event has already happened.

    Examples:
    - Training a model to detect fraudulent transactions:
    The transaction data includes a "customer service complaint" column with "yes"/"no" values. A complaint of "yes" means the customer already reported the fraud, which only happens after the fraudulent transaction has occurred — at the time a new transaction is made, this column is always "no". So the model would learn that only transactions marked "yes" are fraudulent, and it would fail to catch suspicious transactions before a complaint is filed. Fix: remove this column, and train only on data available at the moment the transaction request is made.

    - Training a model to predict which patients will need to return to the hospital within 30 days of being discharged:
    The data includes a "yes"/"no" column for whether a follow-up prescription was discontinued. "Yes" means the patient has already been readmitted. A model trained with this column would fail to flag at-risk patients before they're readmitted, since the column's value is only known after readmission. To train this model correctly, only use data recorded during the patient's stay, plus "static" data like age — any decision made after the patient leaves the hospital will contaminate the model.

    - Training a model to predict whether a customer currently browsing a product will buy it:
    The data includes the view count for the "purchase successful" page, which a customer only sees after completing a purchase. Before the purchase, this value is always 0, so the model would learn to predict that the customer will never buy the product. Including this "final checkout confirmation" feature breaks the prediction for this model.

    How to find **target leakage**:
    Ask yourself: **Will this exact piece of information already be available at the moment the model needs to make a prediction?** If the answer is **no**, remove this feature to avoid the leakage.

2. **Train-Test Contamination**
    Happens when the training pipeline is exposed to validation or testing data. Validation should be done on data the model has not seen yet.

    Example:
    - Medical diagnosis from X-rays:
        Randomly shuffle and split the X-ray image data: 80% for training, 20% for testing.
        Result: the same patient's X-rays end up in both the training set and the test set, so the model's predictions are no longer based on the medical data — it just recognizes that particular patient.
        Fix: split the data by Patient ID, not by individual X-ray. Ensure each patient's data is either 100% in the training set or 100% in the test set.

    To avoid **train-test contamination**, remember the rule: **Test set must remain completely invisible until the model is fully built. Exclude the validation data from any type of fitting, including the fitting of preprocessing steps**

3. **Temporal Leakage**
    Happens when your model accidentally uses information from the future to predict the past.
    To avoid temporal leakage, ask yourself: **If I went back in a time machine to the exact day this prediction is happening, would this data exist yet?** If the answer is no, it is temporal leakage.

**Next:** get familiar more with how to work on features selection for modeling https://www.kaggle.com/learn/feature-engineering

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