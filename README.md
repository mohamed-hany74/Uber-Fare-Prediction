# 🚕 Uber Fare Prediction – NYC

A production-ready machine learning pipeline and web application for predicting Uber fares in New York City.

## 📌 Overview
This project predicts Uber fares based on user-selected pickup/dropoff locations, datetime, weather, and traffic conditions. It uses **CatBoost** and a **Scikit-learn Pipeline** served via a **Flask** backend, with a sleek Leaflet map frontend.

### 🚀 Key Features
- **Zero Training/Serving Skew**: The exact same feature engineering pipeline (`feature_engineering.py`) is used for both training and inference.
- **Robust Validation**: Enforces strict geographical bounds (NYC) and temporal bounds (2009–2015 model training period) on both the client (JS) and server (Python).
- **Interactive UI**: Dark-themed, responsive frontend using Leaflet.js and OpenStreetMap.

---

## 🛠️ Tech Stack
- **Backend**: Python, Flask, Pandas
- **Machine Learning**: CatBoost, Scikit-learn
- **Frontend**: HTML5, Vanilla CSS, Vanilla JS, Leaflet.js

---

## ⚙️ Setup & Installation

```bash
# 1. Create & activate virtual environment
python -m venv venv
# Windows: venv\Scripts\activate | Linux/Mac: source venv/bin/activate

# 2. Install dependencies
pip install -r requirements.txt
```

---

## 💻 Usage

### Running the App (Inference)
Start the Flask development server:
```bash
python app.py
```
*Access the app at http://127.0.0.1:5001*

### Training the Model
To re-train the CatBoost model from scratch (generates `catboost_fare_pipeline.joblib`):
```bash
python train.py          # Standard training
python train.py --tune   # Hyperparameter tuning via RandomizedSearchCV
python train.py --gpu    # GPU-accelerated training
```

---

## 🔧 Recent Engineering Fixes (v1.1)
- **Resolved Skew & Inference Crashes**: Removed residual notebook debug statements in `app.py` that caused `NameError` exceptions during production inference.
- **Hardened Validation**: Implemented strict 2009–2015 datetime bounds. Fixed an issue where the HTML form bypassed native browser validation (due to `novalidate` and AJAX intercepts) by adding explicit JavaScript boundary checks before the `fetch` request.
- **Developer Experience**: Enabled Flask auto-reloading (`debug=True`) by default for smoother local development.

---
*Developed for Cellula Technologies.*
