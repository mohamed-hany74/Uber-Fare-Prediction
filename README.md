# 🚕 Uber NYC Ride Study Dashboard

A professional, high-performance, and user-friendly Streamlit dashboard for exploring and analyzing **500,000 Uber ride records** in New York City. The project translates complex exploratory data analysis (EDA) and pipeline steps from a Jupyter Notebook into clean, interactive, and jargon-free insights suitable for everyday users.

---

## 🎯 What We Did
- **Data Pipeline Modularization**: Migrated the data-cleaning notebook cells into a robust, cached, and step-by-step pipeline in `utils.py` (handling invalid coordinate boxes, null values, standard passenger caps, and trip distances).
- **Interactive Visualizations**: Implemented **11 dynamic charts** using Plotly Express, grouped under intuitive tabs to study pricing drivers, peak hours, airport flat-rate regulations, and categorical influences.
- **User-Centric Narrative**: Replaced complex data science jargon (like OLS regression, skewness, and correlation coefficients) with simple, practical takeaways.
- **Tailored UI/UX**: Injected a clean, modern design featuring custom metric cards, grid structures, and a deep-gradient sidebar layout.

---

## 🛠️ Tech Stack & Libraries
- **Core Language**: Python 3.11
- **UI Framework**: Streamlit (with custom CSS styling & `@st.cache_data` for lightning-fast loads)
- **Data Wrangling**: Pandas & NumPy (manual OLS regression computation for dependency-free trendlines)
- **Interactive Plots**: Plotly Express & Plotly Graph Objects

---

## 📂 Project Structure
```bash
├── .streamlit/
│   └── config.toml      # App theme styling (colors & fonts)
├── app.py               # Main Streamlit layout & page routing
├── utils.py             # Data loader, cleaning steps, and Plotly charts
├── Uber_test.ipynb      # Original exploratory analysis notebook
├── .gitignore           # Git ignore file (prevents uploading raw csv datasets)
└── README.md            # Project documentation
```

---

## 🚀 How to Run Locally

1. **Install dependencies**:
   ```bash
   pip install streamlit pandas numpy plotly
   ```

2. **Place the dataset**:
   Ensure `final_internship_data.csv` is placed in the root directory.

3. **Launch the dashboard**:
   ```bash
   streamlit run app.py
   ```
