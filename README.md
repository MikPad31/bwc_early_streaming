# BWC Early Streaming Iteration 7

- [BWC Early Streaming Iteration 7](#bwc-early-streaming-iteration-7)
  - [Background](#background)
  - [Data](#data)
  - [Setup](#setup)
  - [Model development](#model-development)
    - [Feature selection](#feature-selection)
    - [Hyperparameters](#hyperparameters)
    - [Evaluation on test set (BWC batches 201 and onwards)](#evaluation-on-test-set-bwc-batches-201-and-onwards)
  - [Inference](#inference)

## Background

Iteration 6 and all past iterations only considered data points from trainees that have passed BWC. Data points from trainees that did not pass BWC were NOT considered. The model from iteration 6 achieved extremely poor performance as a result.

Iteration 7 hence includes data points from all BWC trainees, regardless of whether they passed or failed. There is now a **2-stage binary classification**:

1. Predict whether a trainee will pass or fail BWC.
2. Among the predicted passes, predict whether a trainee will get streamed to a fighter or non-fighter AWC course.

In contrast, iteration 6 simply did a binary classification to predict whether a trainee will get streamed to a fighter class.

## Data

Refer to [README_DATA.md](docs/README_DATA.md) for more detailed information.

## Setup

This section details how to set up your Python virtual environment using `venv` and how to download and install the necessary Python packages using `pip`. My Python version is `Python 3.12.3` but any other Python version should work as long as `scikit-learn` supports it.

1. In this project's root folder, open a terminal.
2. Run the following commands:

- i. To create a virtual environment using `venv`:

   ```bash
   # If you are on Windows:
   python -m venv .venv

   # If you are on MacOS/Linux/WSL2:
   # you might need to run sudo apt install python python3-pip python3-venv
   python3 -m venv .venv
   ```

- ii. To activate the virtual environment:

   ```bash
   # If you are on Windows:
   .venv\Scripts\activate

   # If you are on MacOS/Linux/WSL2:
   source .venv/bin/activate
   ```

- iii. To download and install the required packages:

   ```bash
   python -m pip install --upgrade pip  # Upgrade pip if necessary
   pip install -r requirements.txt
   ```

Ensure that you have activated your virtual environment before running any code in the notebooks.

## Model development

Both models were initially developed using BWC pilot trainee data from batches 160 to 190.

Data from batches 191 to 200 were set aside as a validation set and used for feature selection and hyperparameter tuning. Once the modelling approach was finalised, each model was retrained on the full development dataset comprising batches 160 to 200.

For final evaluation, BWC pilot trainee data from batches 201 onward were reserved as a held-out, completely unseen test set. As of 2026-04-01, this test set includes some trainees up to batch 206.

### Feature selection

Using `EMP_EVAL_SCORE` for `LESSON_NUMBER`s belonging to modules 1 to 3 alone achieved the best results.

Other features that were tried include:

- Overriding `EMP_EVAL_SCORE` with `ADJUSTED_SCORE` where available
- Missingness indicators
- Fail indicators based on content in `EMP_EVAL_COMMENTS`
- Zero imputation of missing values

### Hyperparameters

Iteration 7 tried and tested Random Forest and Logistic Regression. Random Forest performed the best.

```Python
stage1_best_model = RandomForestClassifier(
    n_estimators=500,
    max_depth=10,
    min_samples_split=5,
    min_samples_leaf=1,
    class_weight="balanced",
    random_state=42,
    n_jobs=-1
)

stage2_best_model = RandomForestClassifier(
    n_estimators=100,
    max_depth=10,
    min_samples_split=10,
    min_samples_leaf=2,
    class_weight="balanced",
    random_state=42,
    n_jobs=-1
)
```

### Evaluation on test set (BWC batches 201 and onwards)

```markdown
Stage 1: Predict pass or fail BWC
              precision    recall  f1-score   support

         0.0     0.9412    0.8889    0.9143        18
         1.0     0.9535    0.9762    0.9647        42

    accuracy                         0.9500        60
   macro avg     0.9473    0.9325    0.9395        60
weighted avg     0.9498    0.9500    0.9496        60

ROC-AUC: 0.9577
Confusion Matrix:
TN: 16, FP: 2
FN: 1, TP: 41
```

```markdown
Stage 2: Among predicted passes, predict streamed to fighter or not
              precision    recall  f1-score   support

         0.0     0.8205    0.8889    0.8533        36
         1.0     0.8095    0.7083    0.7556        24

    accuracy                         0.8167        60
   macro avg     0.8150    0.7986    0.8044        60
weighted avg     0.8161    0.8167    0.8142        60

ROC-AUC: 0.8958
Confusion Matrix:
TN: 32, FP: 4
FN: 7, TP: 17
```

## Inference

Use [`inference.ipynb`](inference.ipynb) to run inference on unseen data.

Both models were initially trained on BWC pilot trainee data from batches 160 to 190.
