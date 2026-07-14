# Uber Fare Prediction

End-to-end Uber fare analytics and prediction project for New York City rides. The repository combines exploratory analysis, data cleaning, feature engineering, model training, model serialization, and an interactive Streamlit dashboard for business-facing insights.

## Project Overview

This project turns raw Uber trip records into a production-ready analysis workflow:

- Clean and validate trip, fare, passenger, coordinate, weather, traffic, and time-based features.
- Explore fare behavior across ride distance, airports, traffic, weather, passenger count, and temporal patterns.
- Train and tune a CatBoost regression model for fare prediction.
- Save the final trained pipeline as a reusable `joblib` artifact.
- Serve a polished Streamlit dashboard for non-technical users.

## Repository Contents

```text
.
|-- .streamlit/
|   `-- config.toml
|-- app.py
|-- utils.py
|-- Uber_Erd.ipynb
|-- Uber_model(2).ipynb
|-- catboost_fare_pipeline.joblib
|-- catboost_info/
|   `-- learn/
|       `-- events.out.tfevents
|-- .gitignore
`-- README.md
```

## Main Artifacts

| File | Purpose |
| --- | --- |
| `Uber_Erd.ipynb` | Full exploratory data analysis notebook covering business understanding, schema review, data quality checks, cleaning logic, feature analysis, and visual exploration. |
| `Uber_model(2).ipynb` | Modeling notebook with preprocessing, feature engineering, CatBoost training, randomized hyperparameter search, evaluation, and model export. |
| `catboost_fare_pipeline.joblib` | Serialized final pipeline containing preprocessing plus the tuned CatBoost model. |
| `app.py` | Streamlit dashboard entry point. |
| `utils.py` | Reusable data loading, cleaning, transformation, and Plotly visualization helpers. |
| `.streamlit/config.toml` | Dashboard theme configuration. |

## Data Pipeline

The cleaning workflow keeps the modeling and dashboard inputs consistent:

1. Load `final_internship_data.csv`.
2. Remove personal or high-cardinality fields that do not help prediction.
3. Drop rows with missing required coordinates.
4. Validate fare amount boundaries.
5. Restrict pickup and dropoff coordinates to a New York City bounding box.
6. Validate passenger counts and trip distances.
7. Add cyclical time features for hour, weekday, and month.
8. Encode weekend, night, rush-hour, car condition, and traffic condition signals.
9. Scale numerical features and one-hot encode weather categories.

## Modeling

The final model is a CatBoost regressor wrapped in a scikit-learn pipeline:

- Model: `CatBoostRegressor`
- Search strategy: `RandomizedSearchCV`
- Cross-validation: 5 folds
- Search size: 10 candidates, 50 total fits
- Objective: RMSE
- Hardware: GPU-enabled CatBoost on device `0`
- Serialized output: `catboost_fare_pipeline.joblib`

Best parameters from the latest executed notebook:

```text
depth: 8
iterations: 500
learning_rate: 0.1
l2_leaf_reg: 5
subsample: 0.8
```

Latest evaluation:

| Metric | Value |
| --- | ---: |
| MAE | 1.5824 |
| RMSE | 3.3470 |
| R2 | 0.8736 |
| Best CV RMSE | 3.7563 |

The modeling notebook was executed successfully on an NVIDIA GeForce RTX 3060 Laptop GPU. Full notebook execution took about 170 seconds on the local machine.

## Dashboard

The Streamlit app presents the analysis in a business-friendly format:

- Dataset overview and quality audit.
- Fare distribution and outlier behavior.
- Distance and airport-related fare patterns.
- Weather, traffic, passenger, and car-condition comparisons.
- Time-based ride behavior across hours, weekdays, months, and rush periods.
- Clean Plotly charts with cached data loading for faster local use.

Run locally:

```bash
pip install streamlit pandas numpy plotly scikit-learn catboost joblib
streamlit run app.py
```

## Dataset Note

The raw dataset `final_internship_data.csv` is intentionally not committed to Git because it is about 163 MB. GitHub blocks regular files over 100 MB, so the dataset should be stored separately or uploaded through Git LFS if the repository needs to version it.

Expected local placement:

```text
final_internship_data.csv
```

## Reproducing The Model

1. Put `final_internship_data.csv` in the project root.
2. Install the required Python packages.
3. Open `Uber_model(2).ipynb`.
4. Run all cells.
5. Confirm the generated artifact:

```text
catboost_fare_pipeline.joblib
```

## Current GitHub Status

The repository tracks the dashboard code, both notebooks, the trained model artifact, Streamlit config, and project documentation. The raw CSV and virtual environment are ignored by design.
