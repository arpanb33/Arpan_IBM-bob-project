# Car Sales Analysis

End-to-end car sales analytics dashboard with KMeans segmentation, PCA
visualisation, RFE feature selection, and price prediction.

---

## Project Structure

```
.
├── data/
│   └── Updated_Car_Sales_Data.csv   ← place dataset here
│
├── models/
│   ├── train_models.py              ← training script (run once before server)
│   ├── kmeans_model.pkl             ← trained KMeans (k=2)
│   ├── minmax_scaler.pkl
│   ├── label_encoders.pkl
│   ├── price_regressor.pkl          ← GradientBoosting price predictor
│   ├── pca_model.pkl
│   ├── rfe_features.pkl
│   ├── cluster_labels.pkl
│   ├── numeric_columns.pkl
│   └── feature_order.pkl
│
├── backend/
│   └── app.py                       ← Flask REST API
│
├── frontend/
│   ├── index.html                   ← main dashboard page
│   └── static/
│       ├── css/style.css
│       └── js/dashboard.js
│
├── templates/                       ← Jinja2 templates (optional)
├── requirements.txt
└── README.md
```

---

## Quick Start

### 1. Install dependencies
```bash
pip install -r requirements.txt
```

### 2. Place the dataset
Copy `Updated_Car_Sales_Data.csv` into the `data/` folder.

### 3. Train the models
```bash
python models/train_models.py
```
This generates all `.pkl` artifacts in `models/`.

### 4. Start the Flask server
```bash
python backend/app.py
```
Server runs at `http://localhost:5000`.

---

## API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/health` | Liveness check |
| GET | `/api/summary` | Dataset stats (rows, cols, distributions, descriptive stats) |
| GET | `/api/distributions` | Value-count distributions for all columns |
| GET | `/api/cluster-insights` | KMeans cluster profiles |
| GET | `/api/correlation` | Pearson correlation matrix |
| POST | `/api/predict` | Predict price & segment for a vehicle |
| POST | `/api/retrain` | Re-train all models from raw CSV |

### POST `/api/predict` — example request body
```json
{
  "Year":         2020,
  "Mileage":      45000,
  "Fuel Type":    "Hybrid",
  "Transmission": "Automatic",
  "Accident":     "No",
  "Condition":    "Used",
  "Car Make":     "Toyota",
  "Car Model":    "Camry",
  "Color":        "Blue"
}
```
