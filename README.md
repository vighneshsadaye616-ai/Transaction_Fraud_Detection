# FraudGuard — AI-Powered FinTech Fraud Detection

> Upload transaction CSVs and instantly detect fraud with ML-driven insights, SHAP explainability, and interactive analytics.

🔗 **Live Demo**: [https://fraudguard.vercel.app](https://fraudguard.vercel.app)

---

## Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| Frontend | React 18 + Vite | Fast, modern SPA |
| Styling | Tailwind CSS | Rapid dark-theme UI |
| Charts | Recharts | Animated, interactive visualizations |
| Backend | FastAPI (Python 3.11) | Async API, same language as ML |
| ML Pipeline | pandas, scikit-learn, XGBoost, SHAP | Fraud detection + explainability |
| Database | Supabase (PostgreSQL) | Auth + analysis history storage |
| Backend Deploy | Render.com | Free Python hosting |
| Frontend Deploy | Vercel | Instant GitHub deploys |

---

## How It Works

1. **Upload** — Drag & drop a transaction CSV file
2. **Clean** — Auto-handles 7 timestamp formats, 6 amount formats, 70+ city variants, corrupted categories
3. **Engineer** — 20 fraud-signal features computed per transaction
4. **Detect** — IsolationForest → XGBoost two-stage ML pipeline
5. **Explain** — SHAP values show why each transaction was flagged
6. **Visualize** — Interactive dashboard with 6 charts, sortable fraud table, data quality report

---

## Local Development

### Backend

```bash
cd fraudguard/backend
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # Mac/Linux
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

### Frontend

```bash
cd fraudguard/frontend
npm install
npm run dev
```

Open [http://localhost:5173](http://localhost:5173)

---

## Environment Variables

### Backend (`.env` in `backend/`)

| Variable | Description |
|----------|------------|
| `SUPABASE_URL` | Supabase project URL |
| `SUPABASE_SERVICE_KEY` | Supabase service role key (server-only) |

### Frontend (`.env` in `frontend/`)

| Variable | Description |
|----------|------------|
| `VITE_SUPABASE_URL` | Supabase project URL |
| `VITE_SUPABASE_ANON_KEY` | Supabase anon/public key |
| `VITE_BACKEND_URL` | Backend API URL (e.g., `https://fraudguard-api.onrender.com`) |

---

## ML Pipeline Standalone

```python
import pandas as pd
from pipeline.cleaner import DataCleaner
from pipeline.features import FeatureEngineer
from pipeline.model import FraudDetector

df = pd.read_csv('sample.csv')

cleaner = DataCleaner()
df_clean, quality = cleaner.clean(df)

fe = FeatureEngineer()
df_features = fe.engineer_features(df_clean)

detector = FraudDetector()
results = detector.detect(df_features)

print(f"Fraud: {results['fraud_count']} / {results['total_processed']}")
print(f"F1 Score: {results['f1_score']}")
```

---

## Team

| Name | Role |
|------|------|
| (Your name here) | Full Stack + ML |
| (Team member) | (Role) |

---

Built for **Nebulon 2026 Hackathon, Kalina** — 