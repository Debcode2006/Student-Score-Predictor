# Student Math Score Predictor

An end-to-end tabular machine learning project that predicts a student's Math Score from demographic and academic features. The repository includes a modular preprocessing/training pipeline, model comparison, persisted artifacts, and a Flask web application for inference.

## Problem

Given a student's demographic information, preparation status, and reading/writing scores, predict the student's mathematics score on a 0–100 scale.

### Input Features

- Gender
- Race/ethnicity
- Parental level of education
- Lunch type
- Test preparation course
- Reading score
- Writing score

### Output

**Predicted Math Score**

## ML Pipeline

```text
Raw Dataset
    ↓
Data Ingestion
    ↓
Train / Test Split
    ↓
Categorical Encoding + Numerical Scaling
    ↓
Model Comparison
    ↓
Best Model + Preprocessor
    ↓
Flask Inference API / Web UI
```

### Preprocessing

The project uses separate numerical and categorical pipelines:

- Median imputation + standardization for numerical features
- Most-frequent imputation + one-hot encoding + scaling for categorical features
- A `ColumnTransformer` combines the two pipelines
- The fitted preprocessor is serialized for inference

### Model Comparison

The training component evaluates multiple regression algorithms:

- Random Forest Regressor
- Decision Tree Regressor
- Gradient Boosting Regressor
- Linear Regression
- XGBoost Regressor
- CatBoost Regressor
- AdaBoost Regressor

The best candidate is selected using the project's model-evaluation utility and persisted as the final model artifact.

## Web Application

The Flask application provides:

- A form for entering student information
- Prediction through the persisted preprocessing/model pipeline
- A rendered prediction result

Run locally with:

```bash
pip install -r requirements.txt
python app.py
```

Then open the local Flask address shown in the terminal.

## Repository Structure

```text
.
├── src/
│   ├── components/       # Ingestion, transformation, and model training
│   ├── pipeline/         # Prediction pipeline
│   ├── logger.py         # Logging
│   ├── exceptions.py     # Custom exceptions
│   └── utils.py          # Serialization and evaluation helpers
├── artifacts/            # Persisted model and preprocessing artifacts
├── notebook/             # Exploratory/training notebooks
├── templates/            # Flask HTML templates
├── app.py                # Flask application
├── requirements.txt
└── setup.py
```

## Tech Stack

**Python · Scikit-learn · CatBoost · XGBoost · Pandas · NumPy · Flask · Matplotlib · Seaborn**

## Notes

This project focuses on demonstrating a reusable end-to-end tabular ML workflow rather than presenting a benchmark study. The repository does not currently document a final reproducible benchmark in the README, so no performance figure is claimed here.

## Author

Debanjan Sarkar